---
title: Protezione HYOK per Azure Information Protection
description: Panoramica della protezione HYOK (AD RMS) con Azure Information Protection, degli scenari supportati e dei relativi prerequisiti, limitazioni e raccomandazioni.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.subservice: hyok
ms.custom: admin
ms.openlocfilehash: 8ae21a207dd122066fc4dac659bd1e2e9e7c243f
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2020
ms.locfileid: "75742766"
---
# <a name="hold-your-own-key-hyok-protection-for-azure-information-protection"></a>Protezione HYOK (hold your own key) per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Le informazioni che seguono consentono di capire che cos'è la protezione HYOK (hold your own key) per Azure Information Protection e in che cosa differisce rispetto alla protezione predefinita basata su cloud. Prima di usare la protezione HYOK, verificare di avere compreso quando deve essere usata e quali sono gli scenari supportati, i requisiti e le limitazioni. 

## <a name="cloud-based-protection-vs-hyok"></a>Protezione basata sul cloud rispetto a HYOK

Per proteggere documenti e messaggi di posta elettronica contenenti informazioni riservate con Azure Information Protection, è in genere possibile applicare una chiave basata su cloud che usa la protezione di Azure Rights Management (Azure RMS) e sfruttare i vantaggi seguenti:

- Infrastruttura server non necessaria. In questo modo, la soluzione è più veloce e conveniente da distribuire e gestire rispetto a una soluzione locale.

- Condivisione più agevole con partner e utenti di altre organizzazioni tramite l'autenticazione basata su cloud.

- Stretta integrazione con altri servizi di Azure e Office 365, ad esempio ricerca, visualizzatori Web, viste trasformate tramite Pivot, anti-malware, eDiscovery e Delve.

- Monitoraggio di documenti, revoca e notifiche tramite posta elettronica per i documenti condivisi contenenti informazioni riservate.

Una chiave basata su cloud consente di proteggere i documenti e i messaggi di posta elettronica dell'organizzazione usando una chiave privata gestita da Microsoft (impostazione predefinita) o dall'utente (scenario BYOK o "bring your own key"). Per altre informazioni sulle opzioni della chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

I documenti e i messaggi di posta elettronica protetti possono essere archiviati nel cloud o in locale. Per altre informazioni sul funzionamento del processo di protezione per questa chiave basata su cloud, vedere [Informazioni su Azure Rights Management](what-is-azure-rms.md )

I servizi di Office 365 e le applicazioni basate su cloud per il tenant possono essere integrati con Azure Information Protection in modo che funzionalità aziendali importanti, ad esempio i servizi di ricerca, indicizzazione, archiviazione e antimalware, continuino a funzionare senza problemi per il contenuto protetto da Azure Information Protection. La possibilità di leggere il contenuto crittografato in questi scenari è noto anche come "ragionamento sui dati". Ad esempio, è questa funzionalità che consente a Exchange Online di decrittografare i messaggi di posta elettronica per l'analisi antimalware e di eseguire regole di prevenzione della perdita di dati per i messaggi crittografati.

Tuttavia, per i requisiti normativi, per alcune organizzazioni può essere necessario crittografare il contenuto con una chiave isolata dal cloud. Questo isolamento significa che il contenuto crittografato può essere letto solo da applicazioni e servizi locali. Questa opzione di gestione delle chiavi è supportata da Azure Information Protection e viene definita "hold your own key" o HYOK. Quando si usa Azure Information Protection con HYOK, il tenant include sia una chiave basata su cloud che una chiave locale.

## <a name="hyok-guidance-and-best-practices"></a>Materiale sussidiario e procedure consigliate per HYOK

Usare la protezione HYOK solo per i documenti e i messaggi di posta elettronica che richiedono l'isolamento della chiave di crittografia dal cloud. La protezione HYOK non offre i vantaggi che si ottengono quando si usa la protezione con chiave basata su cloud e spesso implica una certa "opacità dei dati". Ciò significa che solo le applicazioni e i servizi locali saranno in grado di aprire i dati protetti con HYOK. I servizi e le applicazioni basati su cloud non sono in grado di "ragionare" sui dati protetti da HYOK.

Anche per le organizzazioni che usano HYOK in genere la protezione è adatta per un numero ridotto di documenti che devono essere protetti. Come prassi consigliata, usarla solo per i documenti e quando sono soddisfatti tutti i criteri seguenti:

- Il contenuto è classificato come altamente riservato all'interno dell'organizzazione e l'accesso è limitato a poche persone

- Il contenuto non è condiviso all'esterno dell'organizzazione

- Il contenuto viene usato solo nella rete interna

Poiché la protezione HYOK è un'opzione di configurazione dell'amministratore per un'etichetta, i flussi di lavoro utente restano invariati, indipendentemente dal fatto che la protezione usi una chiave basata su cloud o HYOK.

I [criteri con ambito](configure-policy-scope.md) costituiscono un buon metodo per verificare che le etichette configurate per la protezione HYOK siano visibili solo agli utenti che devono applicare la protezione HYOK. 

## <a name="supported-scenarios-for-hyok"></a>Scenari supportati per HYOK

Per applicare la protezione HYOK, usare le etichette di Azure Information Protection. 

Nella tabella seguente sono riportati gli scenari supportati per la protezione del contenuto con le etichette configurate per HYOK e per l'apertura e l'uso del contenuto protetto da HYOK.

|Piattaforma|Applicazioni|Funzionalità supportata|
|----------------------|----------|-----------|
|Windows|Client di Azure Information Protection con app di Office 365, Office 2019, Office 2016 e Office 2013 <br /><br />- Word, Excel, PowerPoint|Protezione: sì<br /><br />Consumo: sì|
|Windows|Client di Azure Information Protection con app di Office 365, Office 2019, Office 2016 e Office 2013 <br /><br />- Outlook|Protezione: sì<br /><br />Consumo: sì|
|Windows|Client di Azure Information Protection|Protezione: sì <br /><br />Consumo: sì|
|Windows|Visualizzatore di Azure Information Protection|Protezione: non applicabile<br /><br />Consumo: sì|
|Windows|Client di Azure Information Protection con cmdlet per le etichette di PowerShell|Protezione: sì<br /><br />Consumo: sì|
|Windows|Scanner di Azure Information Protection|Protezione: sì<br /><br />Consumo: sì|
|Windows|Applicazione di condivisione Rights Management|Protezione: no<br /><br />Consumo: sì|
|MacOS|Office per Mac <br /><br /> - Word, Excel, PowerPoint|Protezione: no<br /><br />Consumo: sì|
|MacOS|Office per Mac<br /><br />- Outlook|Protezione: no<br /><br />Consumo: sì|
|MacOS|Applicazione di condivisione Rights Management|Protezione: no<br /><br />Consumo: sì|
|iOS|Office Mobile <br /><br />- Word, Excel, PowerPoint|Protezione: no<br /><br />Consumo: sì|
|iOS|Office Mobile <br /><br />-Outlook|Protezione: no<br /><br />Consumo: no|
|iOS|Visualizzatore di Azure Information Protection|Protezione: non applicabile<br /><br />Consumo: sì|
|Android|Office Mobile <br /><br />- Word, Excel, PowerPoint|Protezione: no<br /><br />Consumo: sì|
|Android|Office Mobile <br /><br />- Outlook|Protezione: no<br /><br />Consumo: no|
|Android|Visualizzatore di Azure Information Protection|Protezione: non applicabile<br /><br />Consumo: sì|
|Web|Outlook sul Web|Protezione: no<br /><br />Consumo: no|
|Web|Office per il Web<br /><br />- Word, Excel, PowerPoint|Protezione: no<br /><br />Consumo: no|
|Universale|App universali di Office<br /><br />- Word, Excel, PowerPoint|Protezione: no<br /><br />Consumo: no|


## <a name="additional-limitations-when-using-hyok"></a>Limitazioni aggiuntive durante l'uso di HYOK

Per l'uso della protezione HYOK con le etichette di Azure Information Protection sono inoltre previste le limitazioni seguenti:

- Non supporta versioni di Office precedenti a Office 2013.

- I servizi di Office 365 e altri servizi online non saranno in grado di decrittografare i documenti e i messaggi di posta elettronica protetti da HYOK per verificarne il contenuto e agire di conseguenza. Questa limitazione si estende ai documenti e messaggi di posta elettronica con protezione HYOK che sono stati protetti con il connettore di Rights Management. 
    
    Questa perdita di funzionalità per i messaggi di posta elettronica protetti da HYOK include i programmi antimalware, le soluzioni di prevenzione della perdita di dati, le regole di routing della posta elettronica, l'inserimento nel journal, eDiscovery, le soluzioni di archiviazione ed Exchange ActiveSync. Inoltre, gli utenti non capiranno perché alcuni dispositivi non sono in grado di aprire i messaggi di posta elettronica protetti da HYOK e ciò può comportare l'aumento di chiamate all'help desk. Poiché le limitazioni sono molte, non è consigliabile usare la protezione HYOK per la posta elettronica.

## <a name="implementing-hyok"></a>Implementazione di HYOK

La protezione HYOK è supportata da Azure Information Protection quando la distribuzione di Active Directory Rights Management Services (AD RMS) è attiva con i requisiti descritti nella sezione seguente. In questo scenario i criteri dei diritti di utilizzo e la chiave privata dell'organizzazione che protegge tali criteri sono gestiti e conservati in locale, mentre i criteri di Azure Information Protection per l'applicazione di etichette e la classificazione continuano a essere gestiti e archiviati in Azure. 

Non confondere HYOK e Azure Information Protection con l'uso di una distribuzione completa di AD RMS e Azure Information Protection o con un'alternativa alla migrazione da AD RMS ad Azure Information Protection. HYOK è supportata solo se si applicano le etichette, non offre parità delle funzionalità con AD RMS e non supporta tutte le configurazioni di distribuzione di AD RMS:

- Per altre informazioni sugli scenari supportati da HYOK per la protezione del contenuto e l'uso di del protetto, vedere la sezione [Scenari supportati per HYOK](#supported-scenarios-for-hyok).

- Per le istruzioni per la migrazione da AD RMS, vedere [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

- Per altre informazioni sui requisiti di distribuzione di AD RMS, vedere la sezione successiva.

### <a name="requirements-for-ad-rms-to-support-hyok"></a>Requisiti per AD RMS per il supporto di HYOK

Una distribuzione di AD RMS deve soddisfare i requisiti seguenti per garantire la protezione HYOK per le etichette di Azure Information Protection.

- Configurazione di AD RMS:
    
  - Versione minima di Windows Server 2012 R2: obbligatoria per gli ambienti di produzione, ma per scopi di testing o valutazione è possibile usare una versione minima di Windows Server 2008 R2 con Service Pack 1.
    
  - Una delle topologie seguenti:
        
    - Foresta singola con singolo cluster radice AD RMS. 
        
    - Più foreste con cluster radice AD RMS indipendenti e utenti che non dispongono di accesso ai contenuti protetti dagli utenti delle altre foreste.
        
    - Più foreste con cluster AD RMS in ognuna di esse. Ogni cluster AD RMS condivide un URL di gestione licenze che fa riferimento allo stesso cluster AD RMS. In questo cluster AD RMS è necessario importare tutti i certificati di dominio utente trusted (TUD) da tutti gli altri cluster AD RMS. Per altre informazioni su questa topologia, vedere [Dominio utente trusted](https://technet.microsoft.com/library/dd983944(v=ws.10).aspx).
        
    Quando si hanno più cluster AD RMS in foreste diverse, eliminare le etichette presenti nei criteri globali che applicano la protezione HYOK (AD RMS) e configurare [criteri con ambito](configure-policy-scope.md) per ogni cluster. Quindi assegnare gli utenti di ogni cluster ai criteri con ambito corrispondenti, evitando di usare gruppi per i quali un utente viene assegnato a più criteri con ambito. In seguito a questa assegnazione ogni utente deve avere etichette per un solo cluster AD RMS. 
    
  - [Modalità crittografia 2](https://technet.microsoft.com/library/hh867439.aspx): è possibile verificare la modalità controllando le proprietà del cluster AD RMS nella scheda **Generale**.
    
  - Ogni server AD RMS è configurato per l'URL di certificazione. [Istruzioni](#configuring-ad-rms-servers-to-locate-the-certification-url) 
    
  - In Active Directory non è registrato un punto di connessione del servizio (SCP): il punto SCP non viene usato quando si usa la protezione di AD RMS con Azure Information Protection. 
    
      - Se è stato registrato un punto di connessione del servizio per la distribuzione di AD RMS è necessario rimuoverlo, per garantire il corretto funzionamento dell'[individuazione dei servizi](./rms-client/client-deployment-notes.md#rms-service-discovery) della protezione di Azure Rights Management. 
        
      - Se si sta installando un nuovo cluster AD RMS per HYOK, ignorare il passaggio per la registrazione del punto SCP durante la configurazione del primo nodo. Per ogni nodo aggiuntivo, assicurarsi che il server sia configurato per l'URL di certificazione prima di aggiungere il ruolo AD RMS e aggiungere il cluster esistente.
    
  - I server AD RMS sono configurati per l'uso di SSL/TLS con un certificato x.509 valido considerato attendibile dai client di connessione: necessario per gli ambienti di produzione, ma non per scopi di testing o valutazione.
    
  - Modelli di diritti configurati.
    
  - Non configurato per IRM di Exchange.
    
  - Per i dispositivi mobili e i computer Mac: [Active Directory Rights Management Services Mobile Device Extension](https://technet.microsoft.com/library/dn673574.aspx) viene installato e configurato.

- La sincronizzazione delle directory è configurata tra l'istanza locale di Active Directory e Azure Active Directory e gli utenti che usano la protezione HYOK sono configurati per l'accesso Single Sign-On.

- Se si condividono documenti o messaggi di posta elettronica protetti da HYOK con altri utenti esterni all'organizzazione: AD RMS è configurato per i trust definiti in modo esplicito in una relazione punto a punto diretta con altre organizzazioni usando domini utente trusted (TUD) o relazioni di trust federative create usando Active Directory Federation Services (AD FS).

- Gli utenti hanno una versione di Office che supporta Information Rights Management (IRM) e almeno Office 2013 Professional Plus con Service Pack 1, in esecuzione in Windows 7 Service Pack 1 o versioni successive. Si noti che Office 2010 e Office 2007 non sono supportati per questo scenario.
    
    - Per Office 2016, Microsoft Installer (MSI)-based Edition: è [stato installato l'aggiornamento 4018295 per Microsoft Office 2016 rilasciato il 6 marzo 2018](https://support.microsoft.com/en-us/help/4018295/march-6-2018-update-for-office-2016-kb4018295).

> [!IMPORTANT]
> Per soddisfare la garanzia elevata offerta dalla protezione HYOK, è consigliabile che i server di AD RMS non si trovino nella rete perimetrale e che vengano usati solo dai dispositivi gestiti. 
> 
> È inoltre consigliabile che il cluster AD RMS usi un modulo di protezione hardware (HSM), in modo che la chiave privata per il certificato concessore di licenze server (SLC) non possa essere esposta o rubata se la distribuzione di AD RMS viene violata o compromessa. 

Per informazioni sulla distribuzione e istruzioni per AD RMS, vedere [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) nella libreria di Windows Server. 


### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>Configurazione dei server AD RMS per individuare l'URL di certificazione

1. In ogni server AD RMS nel cluster, creare la voce del Registro di sistema seguente:

    `Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    
    Specificare uno dei valori seguenti per \<string>:
    
    - Per i cluster AD RMS che usano SSL/TLS:

            https://<cluster_name>/_wmcs/certification/certification.asmx
    
    - Per i cluster AD RMS che non usano SSL/TLS (solo reti di test):
        
            http://<cluster_name>/_wmcs/certification/certification.asmx

2. Riavviare IIS.

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection

Quando si configura un'etichetta per la protezione **HYOK (AD RMS)** è necessario specificare l'URL di licenza del cluster AD RMS. È anche necessario specificare un modello configurato per le autorizzazioni da concedere agli utenti oppure consentire agli utenti di definire le autorizzazioni e gli utenti. 

I valori del GUID del modello e dell'URL sono disponibili nella console di Active Directory Rights Management Services:

- Per individuare il GUID di un modello, espandere il cluster e fare clic su **Modelli di criteri per i diritti di utilizzo**. In **Modelli di criteri per i diritti di utilizzo distribuiti** è quindi possibile copiare il GUID del modello che si vuole usare. Ad esempio: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Per individuare l'URL di gestione licenze: fare clic sul nome del cluster. In **Dettagli cluster** copiare il valore **Gestione licenze** ad eccezione della stringa **/_wmcs/licensing**. ad esempio https://rmscluster.contoso.com 
    
    Se sono presenti un valore di gestione licenze Extranet e un valore di gestione licenze Intranet diversi tra loro: specificare il valore Extranet solo se si condividono documenti o messaggi di posta elettronica protetti con partner definiti mediante relazioni di trust esplicite da punto a punto. In caso contrario, usare il valore Intranet e assicurarsi che tutti i computer client che usano la protezione di AD RMS con Azure Information Protection si connettano tramite una connessione Intranet (ad esempio, i computer remoti devono usare una connessione VPN).


## <a name="next-steps"></a>Passaggi successivi

Per configurare un'etichetta per la protezione HYOK, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 
