---
title: Funzionamento di Azure RMS | Azure Information Protection
description: Descrizione del funzionamento di Azure RMS, dei controlli crittografici usati e dei diagrammi dettagliati del funzionamento di questo processo.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d704751bcc7a968c204d0bab0dc55776411d9593
ms.openlocfilehash: 0ff5deaaea73b7354d2b251c3ce9c768debd2269


---


# <a name="how-does-azure-rms-work-under-the-hood"></a>Funzionamento di Azure RMS: dietro le quinte

>*Si applica a: Azure Information Protection, Office 365*

Una cosa importante da comprendere sul funzionamento di Azure RMS è che tramite il servizio Rights Management (e Microsoft) non vengono visualizzati o archiviati dati come parte del processo di protezione delle informazioni. Le informazioni protette non vengono mai inviate o archiviate in Azure, a meno di archiviarle in modo esplicito in Azure o di usare un altro servizio cloud che le archivia in Azure. Azure RMS rende i dati di un documento semplicemente illeggibili a chiunque, eccetto gli utenti e i servizi autorizzati:

-   I dati vengono crittografati a livello di applicazione e includono un criterio che definisce l'uso autorizzato del documento.

-   Quando un documento protetto viene usato da un utente legittimo o viene elaborato da un servizio autorizzato, i dati contenuti nel documento vengono decrittografati e vengono applicati i diritti definiti nei criteri.

A livello generale, è possibile vedere il funzionamento del processo nell'immagine seguente. Un documento contenente la formula segreta viene protetto e quindi aperto da un utente o un servizio autorizzato. Il documento è protetto da una chiave simmetrica (la chiave verde nell'immagine), che è univoca per ogni documento e viene inserita nell'intestazione del file, dove è protetta dalla chiave radice del tenant di Azure Information Protection (la chiave rossa nell'immagine). La chiave del tenant può essere generata e gestita da Microsoft oppure direttamente dall'utente.

Durante il processo di protezione, mentre Azure RMS crittografa e decrittografa, autorizza e applica restrizioni, la formula segreta non viene mai inviata ad Azure.

![Protezione di un file con Azure RMS](../media/AzRMS_SecretColaFormula_final.png)

Per una descrizione dettagliata delle operazioni eseguite, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo utilizzo, protezione del contenuto, uso del contenuto](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) di questo argomento.

Per informazioni tecniche sugli algoritmi e sulle lunghezze delle chiavi usate in Azure RMS, vedere la sezione successiva.

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Controlli crittografici usati in Azure RMS: Algoritmi e lunghezze delle chiavi
Anche se non è necessario conoscere personalmente il funzionamento di RMS, è possibile che vengano richieste informazioni sui controlli crittografici usati, per garantire che la protezione sia conforme agli standard del settore.


|Controlli crittografici|Uso in Azure RMS|
|-|-|
|Algoritmo: AES<br /><br />Lunghezza della chiave: 128 e 256 bit [[1]](#footnote-1)|Protezione della documentazione|
|Algoritmo: RSA<br /><br />Lunghezza della chiave: 2048 bit|Protezione della chiave|
|SHA-256|Firma del certificato|

###### <a name="footnote-1"></a>Nota 1 

La lunghezza di&256; bit viene usata dal client Azure Information Protection e dall'applicazione di condivisione Rights Management per la protezione generica e la protezione nativa quando il file ha estensione PPDF o è un file di testo o di immagine protetto, ad esempio con estensione PTXT o PJPG.

Modalità di archiviazione e protezione delle chiavi crittografiche:

- Per ogni documento o messaggio di posta elettronica protetto da Azure RMS, viene creata una singola chiave AES ("chiave simmetrica") e tale chiave viene incorporata nel documento e viene salvata in modo permanente nelle diverse edizioni del documento. 

- La chiave simmetrica viene protetta dalla chiave RSA dell'organizzazione ("chiave del tenant di Azure Information Protection") nell'ambito dei criteri del documento e i criteri vengono anche firmati dall'autore del documento. Questa chiave del tenant è comune a tutti i documenti e a tutti i messaggi di posta elettronica protetti da Azure RMS per l'organizzazione e la chiave può essere modificata solo da un amministratore di Azure Information Protection se l'organizzazione usa una chiave del tenant gestita dai clienti, nota come chiave di tipo BYOK ("Bring Your Own Key"). 

    La chiave del tenant è protetta nei servizi online di Microsoft, in un ambiente a controllo elevato e sotto attento monitoraggio. Quando si usa una chiave del tenant gestita dai clienti (BYOK), la sicurezza è ottimizzata mediante l'uso di una matrice di moduli di protezione hardware di qualità elevata in ogni area di Azure. Le chiavi non possono essere estratte, esportate o condivise in alcuna circostanza. Per altre informazioni sulla chiave del tenant e su BYOK, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

- Le licenze e i certificati inviati a un dispositivo Windows sono protetti tramite la chiave privata del dispositivo del client, che viene creata al primo utilizzo di Azure RMS sul dispositivo da parte di un utente. La chiave privata è a sua volta protetta mediante DPAPI sul client, che protegge questi segreti usando una chiave derivata dalla password dell'utente. Nei dispositivi mobili le chiavi vengono usate solo una volta. Non essendo archiviate nei client, queste chiavi non devono essere quindi protette nel dispositivo. 



## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Procedura dettagliata del funzionamento di Azure RMS: primo utilizzo, protezione del contenuto, uso del contenuto
Per comprendere in modo più dettagliato il funzionamento di Azure RMS, viene illustrato un flusso tipico dopo l'[attivazione del servizio Azure Rights Management](../deploy-use/activate-service.md) e quando un utente usa per la prima volta il servizio Rights Management nel proprio computer Windows (un processo definito a volte **inizializzazione dell'ambiente utente** o bootstrap), **protegge il contenuto** (un documento o un messaggio di posta elettronica) e quindi **utilizza** (apre e modifica) il contenuto protetto da altri.

Dopo aver inizializzato l'ambiente utente, l'utente può quindi proteggere i documenti o utilizzare documenti protetti su quel computer.

> [!NOTE]
> Se l'utente passa a un altro computer Windows o un altro utente usa lo stesso computer Windows, il processo di inizializzazione viene ripetuto.

### <a name="initializing-the-user-environment"></a>Inizializzazione dell'ambiente utente
Prima che un utente sia in grado di proteggere contenuto o utilizzare contenuto protetto in un computer Windows, è necessario preparare l'ambiente utente sul dispositivo. Questo è un processo unico e si verifica automaticamente senza l'intervento dell'utente quando un utente tenta di proteggere o utilizzare contenuto protetto:

![Flusso di attivazione client RMS - passaggio 1, autenticazione del client](../media/AzRMS.png)

**Cosa avviene nel passaggio 1**: il client RMS nel computer si connette prima di tutto al servizio Azure Rights Management e autentica l'utente usando il relativo account Azure Active Directory.

Quando l'account dell'utente è federato con Azure Active Directory, l'autenticazione avviene automaticamente e all'utente non vengono richieste le credenziali.

![Attivazione del client RMS - passaggio 2, i certificati vengono scaricati nel client](../media/AzRMS_useractivation2.png)

**Cosa avviene nel passaggio 2**: dopo l'autenticazione dell'utente, la connessione viene reindirizzata automaticamente al tenant di Azure Information Protection dell'organizzazione, che emette i certificati per consentire all'utente di autenticarsi al servizio Azure Rights Management in modo da utilizzare il contenuto protetto e proteggere il contenuto offline.

Una copia del certificato dell'utente viene archiviata in Azure, in modo che se l'utente passa a un altro dispositivo, i certificati vengono creati usando le stesse chiavi.

### <a name="content-protection"></a>Protezione del contenuto
Quando un utente protegge un documento, il client RMS esegue le azioni seguenti su un documento non protetto:

![Protezione del documento RMS - passaggio 1, il documento viene crittografato](../media/AzRMS_documentprotection1.png)

**Cosa avviene nel passaggio 1**: il client RMS crea una chiave casuale (la chiave simmetrica) e crittografa il documento usando questa chiave con l'algoritmo di crittografia simmetrica AES.

![Protezione del documento RMS - passaggio 2, viene creato il criterio](../media/AzRMS_documentprotection2.png)

**Cosa avviene nel passaggio 2**: il client RMS crea quindi un certificato che include un criterio per il documento, in base a un modello o indicando i diritti specifici per il documento. Questo criterio include i diritti per utenti o gruppi diversi e altre limitazioni, ad esempio una data di scadenza.

Il client RMS usa quindi la chiave dell'organizzazione, ottenuta al momento dell'inizializzazione dell'ambiente utente, per crittografare i criteri e la chiave simmetrica. Il client RMS firma anche i criteri con il certificato dell'utente ottenuto al momento dell'inizializzazione dell'ambiente.

![Protezione del documento RMS - passaggio 3, i criteri vengono incorporati nel documento](../media/AzRMS_documentprotection3.png)

**Cosa avviene nel passaggio 3**: infine, il client RMS incorpora i criteri in un file con il corpo del documento crittografato in precedenza, che insieme costituiscono un documento protetto.

Questo documento può essere archiviato ovunque o condiviso usando qualsiasi metodo. I criteri rimangono sempre incorporati nel documento.

### <a name="content-consumption"></a>Utilizzo del contenuto
Quando un utente vuole utilizzare un documento protetto, il client RMS avvia la richiesta per l'accesso al servizio Azure Rights Management:

![Uso del documento RMS - passaggio 1, l'utente viene autenticato e ottiene l'elenco dei diritti](../media/AzRMS_documentconsumption1.png)

**Cosa avviene nel passaggio 1**: l'utente autenticato invia i criteri del documento e i certificati dell'utente al servizio Azure Rights Management. Il servizio decrittografa e valuta i criteri e compila un elenco di diritti (se presenti) di cui l'utente dispone per il documento.

![Uso del documento RMS - passaggio 2, il contratto di licenza con l'utente finale viene restituito al client](../media/AzRMS_documentconsumption2.png)

**Cosa avviene nel passaggio 2**: il servizio estrae quindi la chiave simmetrica AES dai criteri decrittografati. Questa chiave viene quindi crittografata con la chiave pubblica RSA dell'utente ottenuta con la richiesta.

La chiave simmetrica nuovamente crittografata viene quindi incorporata in un contratto di licenza con l'utente finale crittografato con l'elenco dei diritti utente, che viene quindi restituito al client RMS.

![Uso del documento RMS - passaggio 3, il documento viene decrittografato e i diritti vengono applicati](../media/AzRMS_documentconsumption3.png)

**Cosa avviene nel passaggio 3**: infine, il client RMS accetta il contratto di licenza con l'utente finale crittografato e lo decrittografa con la propria chiave privata utente. In questo modo il client RMS decrittografa il corpo del documento quando è necessario e ne esegue il rendering sullo schermo.

Il client decrittografa anche l'elenco di diritti e li passa all'applicazione, che li applica nell'interfaccia utente dell'applicazione.

> [!NOTE]
> Quando gli utenti esterni all'organizzazione usano il contenuto che è stato protetto, il flusso di utilizzo è lo stesso. In questo scenario viene modificata soltanto la modalità di autenticazione dell'utente. Per altre informazioni, vedere [Quando condivido un documento protetto con qualcuno all'esterno della mia azienda, come viene autenticato questo utente?](../get-started/faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)


### <a name="variations"></a>Varianti
Le procedure dettagliate precedenti riguardano scenari standard, ma esistono alcune varianti:

-   **Dispositivi mobili**: quando i dispositivi mobili proteggono o utilizzano file con il servizio Azure Rights Management, i flussi del processo sono molto più semplici. I dispositivi mobili non vengono prima sottoposti al processo di inizializzazione utente, perché ogni transazione (di protezione o utilizzo del contenuto) è invece indipendente. Come con i computer Windows, i dispositivi mobili si connettono al servizio Azure Rights Management ed eseguono l'autenticazione. Per proteggere il contenuto, i dispositivi mobili inviano i criteri e il servizio Azure Rights Management invia una licenza di pubblicazione e la chiave simmetrica per proteggere il documento. Per utilizzare il contenuto, quando i dispositivi mobili si connettono al servizio Azure Rights Management ed eseguono l'autenticazione, inviano i criteri del documento al servizio Azure Rights Management e richiedono una licenza d'uso per utilizzare il documento. In risposta, il servizio Azure Rights Management invia le chiavi e le restrizioni necessarie ai dispositivi mobili. Entrambi i processi usano TLS per proteggere lo scambio di chiavi e altre comunicazioni.

-   **Connettore RMS**: quando il servizio Azure Rights Management viene usato con il connettore RMS, i flussi del processo rimangono invariati. L'unica differenza è che il connettore opera come un relè tra i servizi locali, ad esempio Exchange Server e SharePoint Server, e il servizio Azure Rights Management. Il connettore stesso non esegue alcuna operazione, ad esempio l'inizializzazione dell'ambiente utente, né crittografia o decrittografia. Inoltra semplicemente la comunicazione indirizzata solitamente a un server AD RMS, gestendo la conversione tra i protocolli usati su ogni lato. Questo scenario consente di usare il servizio Azure Rights Management con i servizi locali.

-   **Protezione generica (pfile)**: quando il servizio Azure Rights Management protegge un file in modo generico, il flusso è fondamentalmente quello della protezione del contenuto, con la differenza che il client RMS crea i criteri che concedono tutti i diritti. Quando si usa il file, questo viene decrittografato prima di essere passato all'applicazione di destinazione. Questo scenario consente di proteggere tutti i file, anche se non supportano RMS in modo nativo.

-   **PDF protetto (ppdf)**: quando il servizio Azure Rights Management protegge in modo nativo un file di Office, crea anche una copia del file e lo protegge nello stesso modo. L'unica differenza è che la copia del file è nel formato di file PPDF, che il visualizzatore del client Azure Information Protection e l'applicazione RMS sharing sono in grado di aprire solo per la visualizzazione. Questo scenario consente di inviare allegati protetti tramite posta elettronica, sapendo che il destinatario di un dispositivo mobile sarà sempre in grado di leggerli, anche se il dispositivo mobile non dispone di un'app che supporta i file di Office protetti in modo nativo.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul servizio Azure Rights Management, vedere gli altri articoli della sezione **Comprendere ed esplorare**, ad esempio [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md), in cui viene spiegato come integrare le applicazioni esistenti in Azure Rights Management per fornire una soluzione di protezione delle informazioni. 

Rivedere l'argomento [Terminologia di Azure Information Protection](../get-started/terminology.md) per acquisire familiarità con i termini relativi alla configurazione e all'uso del servizio Azure Rights Management. Prima di iniziare la distribuzione, esaminare anche le informazioni riportate in [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). Per approfondire e affrontare un'esercitazione pratica, usare l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Se si è pronti a iniziare la distribuzione della protezione dati per l'organizzazione, usare la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md) per i passaggi di distribuzione e i collegamenti alle istruzioni d'uso.

> [!TIP]
> Per altre informazioni e indicazioni, usare le risorse e i collegamenti riportati in [Informazioni e supporto per Azure Information Protection](../get-started/information-support.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


