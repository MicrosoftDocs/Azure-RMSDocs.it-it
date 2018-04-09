---
title: Note sulla distribuzione del client RMS - Azure Information Protection
description: Informazioni su installazione, sistemi operativi supportati, impostazioni del Registro di sistema e individuazione del servizio per il client RMS (Rights Management Service) versione 2, noto anche come client MSIPC.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/04/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: df86d75cd7337fa4642a9b758312923a3577325f
ms.sourcegitcommit: 40ac805183589a1c8ef22bc1bd9556bcc92f65e6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2018
---
# <a name="rms-client-deployment-notes"></a>Note sulla distribuzione del client RMS

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 7 con SP1, Windows 8, Windows 8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016*

Il client RMS (client Rights Management Service) versione 2 è anche noto come client MSIPC. Si tratta di un software per computer Windows che comunica con Microsoft Rights Management Services in locale o nel cloud per proteggere l'accesso alle informazioni nonché il loro utilizzo mentre passano attraverso applicazioni e dispositivi all'interno dei confini della propria organizzazione oppure al di fuori di questi confini gestiti. 

Oltre a essere incluso con il [client Azure Information Protection per Windows](aip-client.md), il client RMS è disponibile [come download facoltativo](http://www.microsoft.com/download/details.aspx?id=38396) che è possibile, dopo aver letto e accettato il contratto di licenza, distribuire gratuitamente con software di terze parti, in modo da permettere ai clienti di proteggere e usare contenuto protetto tramite Rights Management Services.


## <a name="redistributing-the-rms-client"></a>Ridistribuzione del client RMS
Il client RMS può essere ridistribuito gratuitamente e in bundle con altre applicazioni e soluzioni IT. Se si vuole ridistribuire il client RMS in qualità di sviluppatori di applicazioni o provider di soluzioni, sono disponibili due opzioni:

- Consigliato: incorporare il programma di installazione del client RMS nell'installazione dell'applicazione ed eseguirlo in modalità invisibile all'utente (l'opzione **/quiet**, descritta in dettaglio nella sezione successiva).

- Rendere il client RMS un prerequisito dell'applicazione. Con questa opzione potrebbe essere necessario fornire agli utenti istruzioni aggiuntive per ottenere, installare e aggiornare i computer con il client prima di poter usare l'applicazione.

## <a name="installing-the-rms-client"></a>Installazione del client RMS
Il client RMS è incluso in un file eseguibile del programma di installazione denominato **setup_msipc_*\<arch\>*.exe**, dove *\<arch>* è **x86** per i computer client a 32 bit o **x64** per i computer client a 64 bit. Il pacchetto di installazione a 64 bit (x64) installa un file eseguibile di runtime a 32 bit per la compatibilità con applicazioni a 32 bit eseguite sull'installazione di un sistema operativo a 64 bit, nonché un file eseguibile di runtime a 64 bit per il supporto di applicazioni native a 64 bit. Il programma di installazione a 32 bit (x86) non viene eseguito su un'installazione di Windows a 64 bit.

> [!NOTE]
> Per installare il client RMS sono necessari privilegi elevati, ad esempio di membro del gruppo Administrators nel computer locale.

È possibile installare il client RMS usando i metodi di installazione seguenti:

- **Modalità invisibile all'utente.** Usando l'opzione **/quiet** come parte delle opzioni della riga di comando, è possibile installare il client RMS sui computer senza intervento dell'utente. L'esempio seguente mostra un'installazione in modalità invisibile all'utente per il client RMS su un computer client a 64 bit:

    ```
    setup_msipc_x64.exe /quiet
    ```

- **Modalità interattiva.** In alternativa, è possibile installare il client RMS usando un programma di installazione basato su interfaccia utente grafica specificato dall'installazione guidata del client RMS. Per avviare l'installazione in modo interattivo, fare doppio clic sul pacchetto di installazione del client RMS, **setup_msipc_*\<arch\>*.exe**, nella cartella in cui è stato copiato o scaricato nel computer locale.

## <a name="questions-and-answers-about-the-rms-client"></a>Domande e risposte sul client RMS
La sezione seguente contiene domande frequenti sul client RMS e le relative risposte.

### <a name="which-operating-systems-support-the-rms-client"></a>Quali sistemi operativi supportano il client RMS?
Il client RMS è supportato con i sistemi operativi seguenti:

|Sistema operativo Windows Server|Sistema operativo Windows Client|
|-----------------------------------|-----------------------------------|
|Windows Server 2016|Windows 10|
|R2 per Windows Server 2012|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 con almeno SP1|


### <a name="which-processors-or-platforms-support-the--rms-client"></a>Quali processori o piattaforme supportano il client RMS?
Il client RMS è supportato nelle piattaforme di elaborazione x86 e x64.

### <a name="where-is-the--rms-client-installed"></a>Qual è il percorso in cui viene installato il client RMS?
Per impostazione predefinita, il client RMS è installato in %ProgramFiles%\Active Directory Rights Management Services Client 2.\<numero di versione secondaria>.

### <a name="what-files--are-associated-with-the-rms-client-software"></a>Quali sono i file associati al software del client RMS?
I file seguenti sono installati come parte del software del client RMS:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Oltre ai file indicati sopra, il client RMS installa anche i file di supporto dell'interfaccia utente multilingue (MUI) in 44 lingue. Per verificare le lingue supportate, eseguire l'installazione del client RMS e quindi esaminare il contenuto delle cartelle del supporto multilingue nel percorso predefinito.

### <a name="is-the-rms-client-included-by-default-when-i-install-a-supported-operating-system"></a>Il client RMS è incluso per impostazione predefinita quando si installa un sistema operativo supportato?
No. Questa versione del client RMS viene fornita come download facoltativo e può essere installato separatamente nei computer che eseguono le versioni supportate del sistema operativo Microsoft Windows.

### <a name="is-the-rms-client-automatically-updated-by-microsoft-update"></a>Il client RMS viene aggiornato automaticamente da Microsoft Update?
Se si installa questo client RMS usando l'opzione di installazione invisibile all'utente, il client RMS erediterà le impostazioni correnti di Microsoft Update. Se si installa il client RMS usando un programma di installazione basato su interfaccia utente grafica, l'installazione guidata del client RMS richiederà di abilitare Microsoft Update.

## <a name="rms-client-settings"></a>Impostazioni del client RMS
La sezione seguente contiene le informazioni di impostazione sul client RMS. Queste informazioni potrebbero essere utili in caso di problemi con le applicazioni o i servizi che usano il client RMS.

> [!NOTE]
> Alcune impostazioni dipendono dal fatto che l'applicazione RMS venga eseguita come applicazione in modalità client, come Microsoft Word e Outlook o il client Azure Information Protection con Esplora file, oppure come applicazione in modalità server, come SharePoint ed Exchange. Nelle tabelle seguenti queste impostazioni sono identificate rispettivamente come **Modalità client** e **Modalità server**.

### <a name="where-the-rms-client-stores-licenses-on-client-computers"></a>Dove il client RMS archivia le licenze nei computer client
Il client RMS archivia le licenze sul disco locale e memorizza anche nella cache alcune informazioni nel registro di sistema di Windows.

|Descrizione|Percorsi per la modalità client|Percorsi per la modalità server|
|---------------|---------------------|---------------------|
|Percorso dell'archivio delle licenze|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\\*\<SID\>*|
|Percorso dell'archivio dei modelli|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\\*\<SID\>*|
|Percorso del registro di sistema|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \\*\<SID*\>|

> [!NOTE]
> *\<SID*> è l'ID di sicurezza (SID) per l'account con cui viene eseguita l'applicazione server. Se per esempio l'applicazione è in esecuzione con l'account Servizio di rete predefinito, sostituire *\<SID\>* con il valore SID noto per l'account (S-1-5-20).

### <a name="windows-registry-settings-for-the-rms-client"></a>Impostazioni del Registro di sistema di Windows per il client RMS
Per impostare o modificare alcune configurazioni del client RMS, è possibile usare le chiavi del Registro di sistema di Windows. Ad esempio, l'amministratore di applicazioni con il supporto predefinito per RMS che comunicano con server AD RMS può decidere di aggiornare la posizione del servizio aziendale (ovvero ignorare il server AD RMS selezionato per la pubblicazione) in base alla posizione corrente del computer client all'interno della topologia di Active Directory oppure abilitare la traccia di RMS nel computer client per la risoluzione di un problema con un'applicazione con il supporto predefinito per RMS. Usare la tabella seguente per identificare le impostazioni del Registro di sistema che è possibile modificare per il client RMS.

|Attività|Impostazioni|
|--------|------------|
|Se la versione del client è 1.03102.0221 o successiva:<br /><br />**Per controllare la raccolta dei dati delle applicazioni**|**Importante**: per rispettare la privacy degli utenti, l'amministratore deve chiedere il loro consenso prima di abilitare la raccolta dei dati.<br /><br />Se si abilita la raccolta dei dati, si accetta di inviare dati a Microsoft attraverso Internet. Microsoft usa questi dati per offrire e migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi Microsoft. Microsoft analizza, ad esempio, prestazioni e affidabilità quali le funzionalità usate dagli utenti, la velocità di risposta delle funzionalità, le prestazioni del dispositivo, le interazioni con l'interfaccia utente e tutti i problemi che possono verificarsi durante l'uso del prodotto. I dati includono anche informazioni sulla configurazione del software, ad esempio la versione attualmente in esecuzione e l'indirizzo IP.<br /><br />Per la versione 1.0.3356 o successiva: <br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft\MSIPC<br />REG_DWORD: DiagnosticAvailability<br /><br />Per le versioni precedenti alla 1.0.3356: <br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft\MSIPC<br />REG_DWORD: DiagnosticState<br /><br />**Valore:** 0 per l'applicazione definita (impostazione predefinita) mediante la proprietà di ambiente [IPC_EI_DATA_COLLECTION_ENABLED](https://msdn.microsoft.com/library/hh535247(v=vs.85).aspx), 1 per disabilitato, 2 per abilitato<br /><br />**Nota**: se l'applicazione basata su MSIPC a 32 bit viene eseguita in una versione di Windows a 64 bit, il percorso è HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC.|
|Solo AD RMS:<br /><br />**Per aggiornare il percorso di un servizio aziendale per un computer client**|Aggiornare le chiavi seguenti del Registro di sistema:<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />REG_SZ: default<br /><br />**Valore:**\<http o https>://*Nome_cluster_RMS*/_wmcs/Certification<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />REG_SZ: default<br /><br />**Valore:** \<http o https>://*Nome_cluster_RMS*/_wmcs/Licensing|
|**Per abilitare e disabilitare la traccia**|Aggiornare la chiave seguente del Registro di sistema:<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />REG_DWORD: traccia<br /><br />**Valore:** 1 per abilitare la traccia, 0 per disabilitare la traccia (impostazione predefinita)|
|**Per modificare la frequenza in giorni con cui si verifica l'aggiornamento dei modelli**|I valori del Registro di sistema seguenti specificano la frequenza di aggiornamento dei modelli nel computer dell'utente se il valore TemplateUpdateFrequencyInSeconds non è impostato.  Se non è impostato alcuno di questi valori, l'intervallo di aggiornamento predefinito per le applicazioni che usano il client RMS (versione 1.0.1784.0) per scaricare i modelli è 1 giorno. Le versioni precedenti hanno un valore predefinito di 7 giorni.<br /><br />**Modalità client:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valore:** valore intero che specifica il numero di giorni (almeno 1) tra i download.<br /><br />**Modalità server:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\<SID\><br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valore:** valore intero che specifica il numero di giorni (almeno 1) tra i download.|
|**Per modificare la frequenza in secondi di aggiornamento dei modelli**<br /><br />Importante: se l'impostazione è specificata, il valore in giorni per l'aggiornamento dei modelli viene ignorato. Specificare uno o l'altro, non entrambi.|I valori del Registro di sistema seguenti specificano la frequenza di aggiornamento dei modelli nel computer dell'utente. Se questo valore o il valore di modifica della frequenza in giorni (TemplateUpdateFrequency) non è impostato, l'intervallo di aggiornamento predefinito per le applicazioni che usano il client RMS (versione 1.0.1784.0) per scaricare i modelli è 1 giorno. Le versioni precedenti hanno un valore predefinito di 7 giorni.<br /><br />**Modalità client:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valore:** valore intero che specifica il numero di secondi (almeno 1) tra i download.<br /><br />**Modalità server:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\<*SID*><br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valore:** valore intero che specifica il numero di secondi (almeno 1) tra i download.|
|Solo AD RMS:<br /><br />**Per scaricare i modelli immediatamente alla successiva richiesta di pubblicazione**|In fase di test e di valutazione, è preferibile che il client RMS scarichi i modelli appena possibile. Per questa configurazione, rimuovere la chiave del Registro di sistema seguente e il client RMS scaricherà immediatamente i modelli alla richiesta di pubblicazione successiva, invece di attendere il tempo specificato dall'impostazione del Registro di sistema TemplateUpdateFrequency:<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*Nome server*>\Template <br /><br />**Nota**: \<*Nome server*> può includere URL sia esterni (corprights.contoso.com) che interni (corprights) e quindi due voci diverse.|
|Solo AD RMS:<br /><br />**Per abilitare il supporto dell'autenticazione federata**|Se il computer client RMS si connette a un cluster AD RMS usando una relazione di trust federativa, è necessario configurare l'area di autenticazione principale della federazione.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_SZ: FederationHomeRealm<br /><br />**Valore:** il valore di questa voce del Registro di sistema è l'URI (Uniform Resource Identifier) del servizio federativo, (ad esempio, "http://TreyADFS.trey.net/adfs/services/trust").<br /><br /> **Nota**: è importante specificare http e non https per questo valore. Se l'applicazione basata su MSIPC a 32 bit viene eseguita in una versione di Windows a 64 bit, il percorso è HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Federation. Per una configurazione di esempio, vedere [Distribuzione di Active Directory Rights Management Services con Active Directory Federation Services](https://technet.microsoft.com/library/dn758110.aspx).|
|Solo AD RMS:<br /><br />**Per supportare i server federativi partner che richiedono l'autenticazione basata su moduli per l'input utente**|Per impostazione predefinita, il client RMS viene eseguito in modalità invisibile all'utente e l'input dell'utente non è richiesto. I server federativi partner, tuttavia, potrebbero essere configurati per richiedere l'input dell'utente, ad esempio con l'autenticazione basata su moduli. In questo caso, il client RMS deve essere configurato per ignorare la modalità invisibile all'utente affinché il modulo di autenticazione federata venga visualizzato in una finestra del browser e l'utente venga innalzato di livello per l'autenticazione.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_DWORD: EnableBrowser<br /><br />**Nota**: se il server federativo è configurato per l'uso dell'autenticazione basata su moduli, questa chiave è obbligatoria. Se il server federativo è configurato per l'uso dell'autenticazione integrata di Windows, la chiave non è obbligatoria.|
|Solo AD RMS:<br /><br />**Per impedire l'utilizzo del servizio ILS**|Per impostazione predefinita, il client RMS consente l'utilizzo del contenuto protetto dal servizio ILS, ma può essere configurato per impedirlo impostando la chiave del Registro di sistema seguente. Se la chiave del Registro di sistema è impostata in modo da impedire il servizio ILS, qualsiasi tentativo di aprire e usare il contenuto protetto dal servizio ILS restituisce l'errore seguente:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: **DisablePassportCertification**<br /><br />**Valore:** 1 per impedire l'utilizzo di contenuto protetto da ILS, 0 per consentirlo (impostazione predefinita)|

### <a name="managing-template-distribution-for-the-rms-client"></a>Gestione della distribuzione dei modelli per il client RMS
I modelli consentono a utenti e amministratori di applicare rapidamente la protezione di Rights Management e fanno sì che il client RMS scarichi automaticamente i modelli dai server o dal servizio RMS. Se si inseriscono i modelli nel percorso della cartella seguente, il client RMS non scarica alcun modello dal percorso predefinito, scarica invece i modelli inseriti nella cartella. Il client RMS potrebbe continuare a scaricare i modelli dal altri server RMS disponibili.

**Modalità client:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Modalità server:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\\*\<SID\>*

Quando si usa questa cartella, non sono previste particolari convenzioni di denominazione da seguire purché i modelli siano rilasciati dal server o dal servizio RMS e devono avere l'estensione di file xml. Ad esempio, Contoso-Confidential.xml oppure Contoso-ReadOnly.xml sono nomi validi.

## <a name="ad-rms-only-limiting-the-rms-client-to-use-trusted-ad-rms-servers"></a>Solo AD RMS: limitazione del client RMS in modo da usare server AD RMS attendibili
È possibile limitare il client RMS in modo da usare solo specifici server AD RMS attendibili apportando le modifiche seguenti al Registro di sistema di Windows nei computer locali.

**Per limitare il client RMS al solo uso di server AD RMS attendibili**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
   
    REG_DWORD:AllowTrustedServersOnly
    
    **Valore:** se il valore specificato è diverso da zero, il client RMS considera attendibili solo i server specificati che sono configurati nell'elenco TrustedServers e nel servizio Azure Rights Management.

**Per aggiungere membri all'elenco di server AD RMS attendibili**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    
    REG_SZ:*\<URL_o_nomehost>*
    
    **Valore:** i valori stringa aggiunti in questo percorso della chiave del Registro di sistema possono essere in formato nome di dominio DNS, (ad esempio **adrms.contoso.com**) oppure URL completi di server AD RMS attendibili (ad esempio **https://adrms.contoso.com**). Se un URL specificato inizia con **https://**, il client RMS usa SSL o TLS per contattare il server AD RMS specificato.

## <a name="rms-service-discovery"></a>Individuazione servizio RMS
L'individuazione del servizio RMS consente al client RMS di controllare con quale server o servizio RMS comunicare prima di proteggere il contenuto. L'individuazione del servizio potrebbe verificarsi anche quando il client RMS usa contenuto protetto, ma è meno probabile che ciò avvenga perché i criteri collegati al contenuto contengono il server o il servizio RMS preferito. L'individuazione del servizio viene eseguita solo se tali origini non sono corrette.

Per eseguire l'individuazione del servizio, il client RMS esegue una serie di controlli sugli elementi seguenti:

1. **Registro di sistema di Windows nel computer locale**: se le impostazioni dell'individuazione del servizio sono configurate nel Registro di sistema, verranno provate prima queste impostazioni. 

    Per impostazione predefinita, queste impostazioni non sono configurate nel Registro di sistema, ma un amministratore può configurarle per AD RMS come illustrato nella [sezione seguente](#enabling-client-side-service-discovery-by-using-the-windows-registry). In genere l'amministratore configura queste impostazioni per il servizio Azure Rights Management durante il [processo di migrazione](../plan-design/migrate-from-ad-rms-phase2.md) da AD RMS ad Azure Information Protection.

2. **Servizi di dominio Active Directory**: un computer aggiunto al dominio esegue una query in Active Directory relativamente a un punto di connessione del servizio (SCP). 

    Se è stato registrato un punto di connessione del servizio come illustrato nella [sezione seguente](#ad-rms-only-enabling-server-side-service-discovery-by-using-active-directory), verrà restituito l'URL del server AD RMS per l'uso da parte del client RMS.

3. **Servizio di individuazione di Azure Rights Management**: il client RMS si connette al sito **https://discover.aadrm.com**, che richiede all'utente di eseguire l'autenticazione.

    Quando l'autenticazione riesce, vengono utilizzati il relativo nome utente e il relativo dominio per identificare il tenant di Azure Information Protection da usare. Viene quindi restituito al client RMS l'URL di Azure Information Protection da usare per l'account utente. Il formato dell'URL è il seguente: **https://**\<URL del tenant\>**/_wmcs/licensing** 

    Ad esempio: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

    *\<URL del tenant\>* ha il formato seguente: **{GUID}.rms.[Region].aadrm.com**. È possibile individuare questo valore identificando il valore **RightsManagementServiceId** quando si esegue il cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per Azure RMS.

> [!NOTE]
> Esistono tre importanti eccezioni a questo flusso di individuazione del servizio:
> 
> - Poiché i dispositivi mobili sono i più adatti per l'uso di un servizio cloud, per impostazione predefinita usano l'individuazione del servizio per il servizio Azure Rights Management (https://discover.aadrm.com)). Per forzare l'impostazione predefinita in modo che i dispositivi mobili usino AD RMS anziché il servizio Azure Rights Management, è necessario specificare i record SRV nel DNS e installare l'estensione per dispositivi mobili, come illustrato in [Estensione di Active Directory Rights Management Services per dispositivi mobili](https://technet.microsoft.com/library/dn673574\(v=ws.11\).aspx). 
>
> - Quando il servizio Rights Management viene richiamato da un'etichetta di Azure Information Protection, l'individuazione del servizio non viene eseguita. L'URL viene invece specificato direttamente nell'impostazione dell'etichetta configurata nei criteri di Azure Information Protection.  

> - Quando un utente esegue l'accesso da un'applicazione di Office, vengono utilizzati il nome utente e il dominio dell'autenticazione per identificare il tenant di Azure Information Protection da usare. In questo caso, le impostazioni del Registro di sistema non sono necessarie e il punto di connessione del servizio non viene controllato.

### <a name="ad-rms-only-enabling-server-side-service-discovery-by-using-active-directory"></a>Solo AD RMS: abilitazione dell'individuazione del servizio sul lato server usando Active Directory
Se l'account ha privilegi sufficienti (Enterprise Admins e amministratore locale per il server AD RMS), è possibile registrare automaticamente un punto di connessione del servizio durante l'installazione del server del cluster radice di AD RMS. Se nella foresta esiste già un punto di connessione del servizio, è necessario prima eliminare il punto di connessione del servizio esistente prima di poterne registrare uno nuovo.

È possibile registrare ed eliminare un punto di connessione del servizio dopo aver installato AD RMS usando la procedura seguente. Prima di iniziare, verificare di avere i privilegi richiesti (Enterprise Admins e amministratore locale per il server AD RMS).

#### <a name="to-enable-ad-rms-service-discovery-by-registering-an-scp-in-active-directory"></a>Per abilitare l'individuazione del servizio AD RMS registrando un punto di connessione del servizio in Active Directory

1.  Aprire la console Servizi di gestione di Active Directory sul server AD RMS:
    
    - Per Windows Server 2012 R2 o Windows Server 2012, in Server Manager fare clic su **Strumenti** > **Active Directory Rights Management Services**.

    - Per Windows Server 2008 R2, selezionare **Start** > **Strumenti di amministrazione** > **Active Directory Rights Management Services**.

2.  Nella console AD RMS fare clic con il pulsante destro del mouse sul cluster AD RMS e quindi fare clic su **Proprietà**.

3.  Fare clic sulla scheda **SCP** .

4.  Selezionare la casella di controllo **Cambia SCP** .

5.  Selezionare l'opzione **Imposta SCP sul cluster di certificazione corrente** e quindi fare clic su **OK**.

### <a name="enabling-client-side-service-discovery-by-using-the-windows-registry"></a>Abilitazione dell'individuazione del servizio sul lato client usando il Registro di sistema di Windows
In alternativa all'uso di un punto di connessione del servizio o se tale punto non esiste, è possibile configurare il Registro di sistema sul computer client in modo che il client RMS possa trovare il relativo server AD RMS.

#### <a name="to-enable-client-side-ad-rms-service-discovery-by-using-the-windows-registry"></a>Per abilitare l'individuazione del servizio AD RMS usando il Registro di sistema di Windows

1. Aprire l'editor del Registro di sistema di Windows, ovvero Regedit.exe:
    
    - Nella finestra Esegui del computer client digitare **regedit** e quindi premere Invio per aprire l'editor del Registro di sistema.

2. Nell'editor del Registro di sistema passare a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!NOTE]
    > Se si esegue un'applicazione a 32 bit in un computer a 64 bit, passare a: **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3. Per creare la sottochiave ServiceLocation, fare clic con il pulsante destro del mouse su **MSIPC**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **ServiceLocation**.

4. Per creare la sottochiave EnterpriseCertification, fare clic con il pulsante destro del mouse su **ServiceLocation**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **EnterpriseCertification**.

5. Per impostare l'URL di certificazione dell'organizzazione, fare doppio clic sul valore **(predefinito)**, nella sottochiave **EnterpriseCertification**. Quando viene visualizzata la finestra di dialogo **Modifica stringa**, per **Dati del valore**, digitare `<http or https>://<AD RMS_cluster_name>/_wmcs/Certification` e fare clic su **OK**.

6. Per creare la sottochiave EnterprisePublishing, fare clic con il pulsante destro del mouse su **ServiceLocation**, scegliere **Nuovo**, fare clic su **Chiave** e digitare `EnterprisePublishing`.

7. Per impostare l'URL di pubblicazione dell'organizzazione, fare doppio clic su **(predefinito)** nella sottochiave **EnterprisePublishing**. Quando viene visualizzata la finestra di dialogo **Modifica stringa**, per **Dati del valore**, digitare `<http or https>://<AD RMS_cluster_name>/_wmcs/Licensing` e fare clic su **OK**.

8.  Chiudere l'editor del Registro di sistema.

Se il client RMS non riesce a trovare un punto di connessione del servizio eseguendo una query in Active Directory e non è specificato nel Registro di sistema, le chiamate di individuazione del servizio per AD RMS hanno esito negativo.

### <a name="redirecting-licensing-server-traffic"></a>Reindirizzamento del traffico del server delle licenze
In alcuni casi, potrebbe essere necessario reindirizzare il traffico durante l'individuazione del servizio, ad esempio quando vengono fuse due organizzazioni e il server licenze precedente di un'organizzazione viene rimosso e i client devono essere reindirizzati a un nuovo server licenze oppure si esegue la migrazione da AD RMS ad Azure RMS. Per abilitare il reindirizzamento delle licenze, usare la procedura seguente.

#### <a name="to-enable-rms-licensing-redirection-by-using-the-windows-registry"></a>Per abilitare il reindirizzamento delle licenze RMS usando il Registro di sistema di Windows

1.  Aprire l'editor del Registro di sistema di Windows, ovvero Regedit.exe.

2.  Nell'editor del Registro di sistema passare a una delle posizioni seguenti:

    -   Versione a 64 bit di Office su piattaforma x64: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   Versione a 32 bit di Office su piattaforma x64: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Creare una sottochiave LicensingRedirection facendo clic con il pulsante destro del mouse su **Servicelocation**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **LicensingRedirection**.

4.  Per impostare il reindirizzamento delle licenze, fare clic con il pulsante destro del mouse sulla sottochiave **LicensingRedirection**, selezionare **Nuovo** e quindi selezionare **Valore stringa**.  In **Nome**specificare l'URL delle licenze server precedente e in **Valore** specificare il nuovo URL delle licenze server.

    Ad esempio, per reindirizzare le licenze da un server presso Contoso.com a uno in Fabrikam.com,è possibile immettere i valori seguenti:

    **Nome:** `https://contoso.com/_wmcs/licensing`

    **Valore:** `https://fabrikam.com/_wmcs/licensing`
    
    > [!NOTE]
    > Se per il server licenze precedente sono specificati sia l'URL Intranet che l'URL Extranet, è necessario impostare un nuovo mapping nome/valore per entrambi gli URL nella chiave **LicensingRedirection**.

5.  Ripetere il passaggio precedente per tutti i server da reindirizzare.

6.  Chiudere l'editor del Registro di sistema.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
