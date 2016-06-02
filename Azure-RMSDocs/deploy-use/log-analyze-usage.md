---
# required metadata

title: Registrazione e analisi dell'utilizzo di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Registrazione e analisi dell'uso di Rights Management di Windows Azure

*Si applica a: Azure Rights Management, Office 365*

Le informazioni riportate in questo argomento consentono di comprendere l'uso della funzionalità di registrazione dell'utilizzo di Azure Rights Management (Azure RMS). Il servizio Azure Rights Management è in grado di registrare qualsiasi richiesta eseguita per l'organizzazione, incluse le richieste provenienti dagli utenti, le azioni eseguite dagli amministratori di Rights Management nell'organizzazione e quelle eseguite da operatori Microsoft a supporto della distribuzione di Azure Rights Management.

È poi possibile usare i log di Azure Rights Management per supportare gli scenari aziendali seguenti:

-   **Analisi per ottenere informazioni aziendali accurate**

    I log generati da Azure Rights Management possono essere importati in un repository scelto dall'utente, ad esempio un database, un sistema di elaborazione analitica online (OLAP) o un sistema MapReduce, per analizzare le informazioni e generare report. È possibile, ad esempio, identificare gli utenti che accedono ai dati protetti da RMS e determinare quali dati protetti vengono visualizzati, da quali dispositivi e da quali postazioni. È inoltre possibile stabilire se gli utenti possono leggere correttamente il contenuto protetto. È infine possibile identificare gli utenti che hanno letto un importante documento protetto.

-   **Monitoraggio per evitare eventuali abusi**

    Le informazioni fornite dalla funzionalità di registrazione di Azure Rights Management sono disponibili quasi in tempo reale e consentono un monitoraggio continuo dell'uso di Rights Management da parte della società. Il 99,9% dei log sono disponibili entro 15 minuti dall'inizio di un'azione avviata da RMS.

    È possibile, ad esempio, scegliere di ricevere un avviso nel caso in cui si verifichi un improvviso picco di accessi a dati protetti da RMS al di fuori del normale orario di lavoro. Un picco di questo tipo potrebbe indicare che un utente malintenzionato sta raccogliendo informazioni da vendere alla concorrenza. È possibile anche scegliere di ricevere un avviso se uno stesso utente sembra accedere ai dati da due indirizzi IP differenti nell'arco di un breve periodo di tempo. Questo evento può indicare infatti che un account utente è stato compromesso.

-   **Eseguire analisi forensi**

    Se si verifica una perdita di informazioni, è probabile che all'amministratore vengano richiesti i nominativi degli utenti che hanno avuto accesso a specifici documenti e l'indicazione delle informazioni visualizzate di recente da una persona sospetta. Se si usa Azure Rights Management e la relativa funzione di registrazione, è possibile rispondere a questo tipo di domande. Gli utenti che usano contenuto protetto, infatti, devono sempre ottenere una licenza di Rights Management per aprire immagini e documenti protetti con Azure Rights Management, anche se i file vengono spostati tramite posta elettronica o copiati in unità USB o altri dispositivi di archiviazione. Questo significa che, quando i dati vengono protetti con Azure Rights Management, è possibile usare i log di Azure Rights Management come fonte certa di informazioni per l'esecuzione di analisi a scopo legale.

> [!NOTE] Se si è interessati solo alla registrazione delle attività amministrative di Azure Rights Management e non all'utilizzo del servizio da parte degli utenti, è possibile usare il cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) di Windows PowerShell per Azure Rights Management.
> 
> È possibile anche usare il portale di Azure classico per report generali sull'utilizzo, tra cui **Riepilogo per RMS**, **Utenti attivi RMS**, **Piattaforme dispositivi RMS** e **Utilizzo applicazioni RMS**. Per accedere a questi report dal portale di Azure classico, fare clic su **Active Directory**, selezionare e aprire una directory e quindi fare clic su **REPORT**.

Per altre informazioni sulla funzionalità di registrazione dell'utilizzo di Azure Rights Management, vedere le sezioni seguenti.

## Come abilitare la funzionalità di registrazione dell'utilizzo di Azure Rights Management
A partire da febbraio 2016, la funzionalità di registrazione dell'utilizzo di Azure Rights Management è abilitata per impostazione predefinita per tutti i clienti. Questa impostazione è applicabile ai clienti che hanno attivato il servizio Azure RMS prima di febbraio 2016 e ai clienti che attivano il servizio dopo il mese di febbraio 2016. 

> [!NOTE] Non sono previsti costi aggiuntivi per l'archiviazione dei log o per il funzionamento della funzionalità di registrazione.
> 
> A differenza della situazione attuale, per usare la funzionalità di registrazione dell'utilizzo di Azure RMS prima del mese di febbraio 2016 occorreva avere una sottoscrizione di Azure e risorse di archiviazione sufficienti in Azure.



## Come accedere e usare i log dell'utilizzo di Azure Rights Management
Azure Rights Management scrive i log nell'account di archiviazione di Azure sotto forma di una serie di BLOB. Ciascun blob contiene uno o più record di log in formato W3C esteso. I nomi dei blob sono numeri e corrispondono all'ordine di creazione. La sezione [Come interpretare i log dell'utilizzo di Azure Rights Management](#how-to-interpret-your-azure-rights-management-usage-logs) più avanti in questo argomento contiene altre informazioni sui contenuti dei log e sulla relativa creazione.

In seguito a un'azione di Azure Rights Management, la visualizzazione dei log nell'account di archiviazione può richiedere un po' di tempo. La maggior parte dei log viene visualizzata entro 15 minuti. È consigliabile scaricare i log in uno spazio di archiviazione locale, ad esempio una cartella o un database, oppure in un repository MapReduce.

Per scaricare i log dell'utilizzo, verrà usato il modulo di amministrazione di Azure RMS per Windows PowerShell. Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md). Se il modulo Windows PowerShell è stato scaricato in precedenza, eseguire il comando seguente per verificare che la versione in uso sia almeno la versione **2.4.0.0**: `(Get-Module aadrm -ListAvailable).Version` 

### Per scaricare i log dell'utilizzo con PowerShell

1.  Avviare Windows PowerShell con l'opzione **Esegui come amministratore** e usare il cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) per connettersi al servizio Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    
2.  Eseguire il comando seguente per scaricare i log per una data specifica: 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    Ad esempio, dopo avere creato una cartella denominata Logs sull'unità E:
    
    * Per scaricare i log per una data specifica, ad esempio 01/02/2016, eseguire il comando seguente: `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Per scaricare i log per un intervallo di date, ad esempio da 01/02/2016 a 14/02/2016, eseguire il comando seguente: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Quando si specifica solo il giorno, come negli esempi, si presuppone che l'ora corrisponda alle 00.00.00 nel fuso orario locale e l'orario viene quindi convertito in UTC. Quando si specifica un orario con i parametri -fromdate o -todate, ad esempio -fordate "1/2/2016 15:00:00", la data e l'ora vengono convertite in UTC. Il comando Get-AadrmUserLog recupera quindi i log per quel periodo UTC.

Non è possibile scaricare un intervallo di tempo inferiore a un giorno intero.

Per impostazione predefinita, questo cmdlet usa tre thread per scaricare i log. Se la larghezza di banda è sufficiente e si vuole ridurre il tempo necessario per scaricare i log, usare il parametro -NumberOfThreads, che supporta un valore compreso tra 1 e 32. Ad esempio, se si esegue il comando seguente, il cmdlet genera 10 thread per il download dei log: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> È possibile aggregare tutti i file di log scaricati in un formato CSV mediante [Log Parser di Microsoft](https://www.microsoft.com/download/details.aspx?id=24659), uno strumento che consente di eseguire conversioni tra formati di log noti. È possibile usare questo strumento anche per convertire i dati in formato SYSLOG o per importarli in un database. Dopo aver installato lo strumento, eseguire `LogParser.exe /?` per informazioni e supporto sul relativo uso. 
>
> È possibile, ad esempio, eseguire il comando riportato di seguito per importare tutte le informazioni in un file in formato .log: `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### Se la funzionalità di registrazione dell'utilizzo di Azure RMS è stata abilitata manualmente prima della modifica relativa alla registrazione del 22 febbraio 2016


Se la funzionalità di registrazione dell'utilizzo è stata usata prima delle modifica relativa alla registrazione, nell'account di archiviazione di Azure configurato saranno presenti log dell'utilizzo. Microsoft non copierà questi log dall'account di archiviazione nel nuovo account di archiviazione gestito di Azure RMS come parte della modifica relativa alla registrazione. L'utente è responsabile della gestione del ciclo di vita dei log generati in precedenza e può usare il cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) per scaricare i log precedenti. Ad esempio:

- Per scaricare tutti i log disponibili nella cartella E:\logs: `Get-AadrmUsageLog -Path "E:\Logs"`
    
- Per scaricare uno specifico intervallo di blob: `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

Si noti che non è necessario scaricare i log usando il cmdlet Get-AadrmUsageLog se si verifica una delle condizioni seguenti:

-  Azure Rights Management è stato attivato il 22 febbraio 2016 o in una data precedente ma la funzionalità di registrazione dell'utilizzo non è stata abilitata.

- Azure Rights Management è stato attivato dopo il 22 febbraio 2016.

## Come interpretare i log dell'utilizzo di Azure Rights Management
Usare le informazioni seguenti come riferimento per interpretare i log dell'utilizzo di Azure Rights Management.

### Sequenza dei log
Azure Rights Management scrive i log sotto forma di una serie di BLOB, 

Ogni voce del log ha un timestamp UTC. Poiché Azure Rights Management viene eseguito su più server in diversi data center, in alcuni casi i log possono sembrare fuori sequenza, anche se sono stati ordinati in base al relativo timestamp. Lo sfasamento è tuttavia minimo, in genere inferiore al minuto, e nella maggior parte dei casi non crea problemi per l'analisi dei log.

### Formato dei blob
Ciascun blob è scritto in formato di log W3C esteso ed inizia con le due righe seguenti:

**#Software: RMS**

**#Versione: 1.1**

La prima riga indica che si tratta di log di Azure Rights Management, mentre la seconda indica che il resto del BLOB segue la specifica della versione 1.1. È importante che le applicazioni che analizzano questi log verifichino queste due righe prima di procedere con l'analisi della restante parte del blob.

La terza riga è costituita da un elenco di nomi separati da caratteri di tabulazione:

**#Campi: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

Ciascuna delle righe seguenti è un record di log. I valori dei campi seguono lo stesso ordine della riga precedente e sono separati da caratteri di tabulazione. La tabella riportata di seguito consente di interpretare i campi.

|Nome campo|Tipo di dati W3C|Descrizione|Valore di esempio|
|--------------|-----------------|---------------|-----------------|
|date|Date|La data UTC in cui è stata gestita la richiesta.<br /><br />L'origine è l'orologio locale del server che ha gestito la richiesta.|25-06-2013|
|time|Ora|L'ora in cui è stata gestita la richiesta, in formato UTC 24 ore.<br /><br />L'origine è l'orologio locale del server che ha gestito la richiesta.|21.59.28|
|row-id|Testo|Il GUID univoco del record di log.<br /><br />Questo valore è utile quando i log vengono aggregati o copiati in un altro formato.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nome|Il nome dell'API RMS richiesta.|AcquireLicense|
|user-id|String|L'utente che ha effettuato la richiesta.<br /><br />Questo valore è riportato tra virgolette singole. Alcuni tipi di richiesta sono anonimi, e in questo caso il valore è ”.|‘joe@contoso.com’|
|result|String|La stringa ‘Success’ indica che la richiesta è stata eseguita con esito positivo.<br /><br />Se la richiesta ha avuto esito negativo, il tipo di errore viene riportato tra virgolette singole.|‘Success’|
|correlation-id|Testo|GUID comune tra il log del client e il log del server RMS per una determinata richiesta.<br /><br />Questo valore può essere utile per la risoluzione dei problemi del client.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Testo|GUID, riportato tra parentesi graffe, che identifica il contenuto protetto, ad esempio un documento.<br /><br />In questo campo è presente un valore solo se la richiesta è di tipo AcquireLicense. Per tutti gli altri tipi di richiesta il campo è vuoto.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|String|Indirizzo di posta elettronica del proprietario del documento.|alice@contoso.com|
|issuer|String|Indirizzo di posta elettronica del soggetto emittente il documento.|alice@contoso.com (o) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Template-id|String|ID del modello usato per proteggere il documento.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|File-name|String|Nome del documento protetto. <br /><br />Attualmente, alcuni file, ad esempio i documenti di Office, vengono visualizzati come GUID anziché come nome di file.|TopSecretDocument.docx|
|Date-published|Date|Data in cui è stato protetto il documento.|2015-10-15T21:37:00|
|c-info|String|Informazioni sulla piattaforma client che effettua la richiesta.<br /><br />La stringa specifica varia a seconda dell'applicazione (ad esempio, il sistema operativo o il browser).|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Address|L'indirizzo IP del client che effettua la richiesta.|64.51.202.144|

#### Eccezioni per il campo user-id
Anche se nel campo user-id è in genere riportato il nome dell'utente che ha effettuato la richiesta, esistono due eccezioni in cui il valore del campo non indica un utente reale:

-   Il valore **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**.

    Questo valore indica che la richiesta viene eseguita da un servizio di Office 365, ad esempio Exchange Online o SharePoint Online. Nella stringa, *&lt;YourTenantID&gt;* è il GUID del tenant, mentre *&lt;region&gt;* è l'area in cui è registrato il tenant. Ad esempio, **na** indica l'America del Nord, **eu** l'Europa e **ap** l'Asia.

-   Si sta usando il connettore RMS.

    Le richieste provenienti da questo connettore vengono registrate con il nome dell'entità servizio generato automaticamente da RMS quando si installa il connettore RMS.

#### Tipi di richiesta tipici
Azure Rights Management supporta diversi tipi di richiesta. La tabella seguente elenca i tipi di richiesta più comuni.

|Tipo di richiesta|Descrizione|
|----------------|---------------|
|AcquireLicense|Un client da un computer basato su Windows richiede una licenza per contenuto protetto con RMS.|
|AcquirePreLicense|Un client richiede una licenza per contenuto protetto con RMS per conto dell'utente.|
|AcquireTemplates|È stata eseguita una chiamata per acquisire modelli in base agli ID modello.|
|AcquireTemplateInformation|È stata eseguita una chiamata per ottenere gli ID del modello dal servizio.|
|AddTemplate|Viene eseguita una chiamata dal portale di Azure classico per aggiungere un modello.|
|BECreateEndUserLicenseV1|Viene eseguita una chiamata da un dispositivo mobile per creare un contratto di licenza con l'utente finale.|
|BEGetAllTemplatesV1|Viene eseguita una chiamata da un dispositivo mobile (back-end) per ottenere tutti i modelli.|
|Certify|Il client sta certificando la protezione del contenuto.|
|Decrypt|Il client tenta di decrittografare il contenuto protetto con RMS.|
|DeleteTemplateById|Viene eseguita una chiamata dal portale di Azure classico per eliminare un modello in base a un ID modello.|
|ExportTemplateById|Viene eseguita una chiamata dal portale di Azure classico per esportare un modello in base a un ID modello.|
|FECreateEndUserLicenseV1|Richiesta analoga ad AcquireLicense, ma inviata da dispositivi mobili.|
|FECreatePublishingLicenseV1|Questa richiesta corrisponde a una combinazione di Certify e GetClientLicensorCert ed è inviata da client mobili.|
|FEGetAllTemplates|Viene eseguita una chiamata da un dispositivo mobile (front-end) per ottenere i modelli.|
|GetAllTemplates|Viene eseguita una chiamata dal portale di Azure classico per ottenere tutti i modelli.|
|GetClientLicensorCert|Il client richiede un certificato di distribuzione, da usare in un secondo tempo per proteggere i contenuti, da un computer basato su Windows.|
|GetConfiguration|Un cmdlet di PowerShell Azure viene chiamato per ottenere la configurazione del tenant di Azure RMS.|
|GetConnectorAuthorizations|Viene eseguita una chiamata dai connettori RMS per ottenere la rispettiva configurazione dal cloud.|
|GetTenantFunctionalState|Il portale di Azure classico controlla se Azure RMS è attivato.|
|GetTemplateById|Viene eseguita una chiamata dal portale di Azure classico per ottenere un modello specificando un ID modello.|
|ExportTemplateById|Viene eseguita una chiamata dal portale di Azure classico per esportare un modello specificando un ID modello.|
|FindServiceLocationsForUser|Viene eseguita una chiamata per effettuare una query di URL, che consente di chiamare la richiesta Certify o AcquireLicense.|
|ImportTemplate|Viene eseguita una chiamata dal portale di Azure classico per importare un modello.|
|ServerCertify|Viene eseguita una chiamata da un client abilitato per RMS, come SharePoint, per certificare il server.|
|SetUsageLogFeatureState|Viene eseguita una chiamata per abilitare la funzionalità di registrazione dell'utilizzo.|
|SetUsageLogStorageAccount|Viene eseguita una chiamata per specificare il percorso dei log di Azure RMS.|
|SignDigest|Viene eseguita una chiamata quando una chiave viene usata a scopo di firma. In genere, viene eseguita una chiamata per ogni richiesta AcquireLicence (o FECreateEndUserLicenseV1), Certify e GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|UpdateTemplate|Viene eseguita una chiamata dal portale di Azure classico per aggiornare un modello esistente.|

## Riferimenti Windows PowerShell
A partire da febbraio 2016, l'unico cmdlet di Windows PowerShell necessario per la funzionalità di registrazione dell'utilizzo di Azure RMS è [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx). 

Prima di questa modifica, per i log dell'utilizzo di Azure RMS erano necessari i cmdlet seguenti, ora deprecati:  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Se la risorsa di archiviazione di Azure include log precedenti alla modifica relativa alla registrazione di Azure RMS, è possibile scaricarli usando questi cmdlet meno recenti, con Get-AadrmUsageLog e Get-AadrmUsageLogLastCounterValue, in base alla procedura consentita in precedenza. Tutti i nuovi log dell'utilizzo, tuttavia, scriveranno nella nuova risorsa di archiviazione di Azure RMS e devono essere scaricati con Get-AadrmUserLog.

Per altre informazioni sull'uso di Windows PowerShell per Azure Rights Management, vedere l'articolo relativo all'[amministrazione di Azure Rights Management tramite Windows PowerShell](administer-powershell.md).





<!--HONumber=May16_HO3-->


