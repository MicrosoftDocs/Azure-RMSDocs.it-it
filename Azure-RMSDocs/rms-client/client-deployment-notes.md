---
title: Note sulla distribuzione del client RMS | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2bd8aba91b9b65777c2319baea848e8313cbccda
ms.openlocfilehash: ffddda9a144b23b64b54df4fe4d25ec62600599d


---

# Note sulla distribuzione del client RMS

*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 7 con SP1, Windows 8, Windows 8.1, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Vista*

Il client RMS (client Rights Management Service) versione 2 è anche noto come client MSIPC. Si tratta di un software per computer Windows che comunica con Microsoft Rights Management Services in locale o nel cloud per proteggere l'accesso alle informazioni nonché il loro utilizzo mentre passano attraverso applicazioni e dispositivi all'interno dei confini della propria organizzazione oppure al di fuori di questi confini gestiti. Oltre alle spedizioni con l'[applicazione di condivisione Rights Management per Windows](sharing-app-windows.md), il client RMS è disponibile [come download facoltativo](http://www.microsoft.com/download/details.aspx?id=38396) che può essere distribuito gratuitamente con software di terze parti, previo riconoscimento e accettazione del contratto di licenza, in modo che i clienti possano proteggere e utilizzare contenuti protetti dai servizi Rights Management.


## Ridistribuzione del client RMS
Il client RMS può essere ridistribuito gratuitamente e in bundle con altre applicazioni e soluzioni IT. Se si vuole ridistribuire il client RMS in qualità di sviluppatori di applicazioni o provider di soluzioni, sono disponibili due opzioni:

-   Consigliato: incorporare il programma di installazione del client RMS nell'installazione dell'applicazione ed eseguirlo in modalità invisibile all'utente (l'opzione **/quiet**, descritta in dettaglio nella sezione successiva).

-   Rendere il client RMS un prerequisito dell'applicazione. Con questa opzione potrebbe essere necessario fornire agli utenti istruzioni aggiuntive per ottenere, installare e aggiornare i computer con il client prima di poter usare l'applicazione.

## Installazione del client RMS
Il client RMS è incluso in un file eseguibile del programma di installazione denominato **setup_msipc_***<arch>***.exe**, dove *<arch>* è **x86** per i computer client a 32 bit o **x64** per i computer client a 64 bit. Il pacchetto di installazione a 64 bit (x64) installa un file eseguibile di runtime a 32 bit per la compatibilità con applicazioni a 32 bit eseguite sull'installazione di un sistema operativo a 64 bit, nonché un file eseguibile di runtime a 64 bit per il supporto di applicazioni native a 64 bit. Il programma di installazione a 32 bit (x86) non verrà eseguito su un'installazione di Windows a 64 bit.

> [!NOTE]
> Sono necessari privilegi elevati per installare il client RMS, come ad esempio un membro del gruppo Administrators sul computer locale.

È possibile installare il client RMS usando i metodi di installazione seguenti:

-   **Modalità invisibile all'utente.** Usando l'opzione **/quiet** come parte delle opzioni della riga di comando, è possibile installare il client RMS sui computer senza intervento dell'utente. L'esempio seguente mostra un'installazione in modalità invisibile all'utente per il client RMS su un computer client a 64 bit:

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **Modalità interattiva.** In alternativa, è possibile installare il client RMS usando un programma di installazione basato su interfaccia utente grafica fornito dall'installazione guidata del client RMS. Per avviare questo tipo di installazione è sufficiente fare doppio clic sul pacchetto di installazione del client RMS (**setup_msipc_***<arch>***.exe**) nella cartella in cui è stato copiato o scaricato nel computer locale.

## Domande e risposte sul client RMS
La sezione seguente contiene domande frequenti sul client RMS e le relative risposte.

### Quali sistemi operativi supportano il client RMS?
Il client RMS è supportato con i sistemi operativi seguenti:

|Sistema operativo Windows Server|Sistema operativo Windows Client|
|-----------------------------------|-----------------------------------|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 con almeno SP1|
|Windows Server 2008 (solo AD RMS)|Windows Vista con almeno SP2 (solo AD RMS)|

### Quali processori o piattaforme supportano il client RMS?
Il client RMS è supportato nelle piattaforme di elaborazione x86 e x64.

### Qual è il percorso in cui viene installato il client RMS?
Per impostazione predefinita, il client RMS è installato in %ProgramFiles%\Active Directory Rights Management Services Client 2.<minor version number>.

### Quali sono i file associati al software del client RMS?
I file seguenti sono installati come parte del software del client RMS:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Oltre ai file indicati sopra, il client RMS installa anche i file di supporto dell'interfaccia utente multilingue (MUI) in 44 lingue. Per verificare le lingue supportate, eseguire l'installazione del client RMS e quindi esaminare il contenuto delle cartelle del supporto multilingue nel percorso predefinito.

### Il client RMS è incluso per impostazione predefinita quando si installa un sistema operativo supportato?
No. Questa versione del client RMS viene fornita come download facoltativo e può essere installato separatamente nei computer che eseguono le versioni supportate del sistema operativo Microsoft Windows.

### Il client RMS viene aggiornato automaticamente da Microsoft Update?
Se si installa questo client RMS usando l'opzione di installazione invisibile all'utente, il client RMS erediterà le impostazioni correnti di Microsoft Update. Se si installa il client RMS usando un programma di installazione basato su interfaccia utente grafica, l'installazione guidata del client RMS richiede di abilitare Microsoft Update.

## Impostazioni del client RMS
La sezione seguente contiene le informazioni di impostazione sul client RMS. Queste informazioni potrebbero essere utili in caso di problemi con le applicazioni o i servizi che usano il client RMS.

> [!NOTE]
> Alcune impostazioni dipendono dall'esecuzione eventuale dell'applicazione con il supporto predefinito per RMS come applicazione in modalità client (come Microsoft Word e Outlook o l'applicazione RMS sharing) oppure come applicazione in modalità server (come SharePoint e Exchange).  Nelle tabelle seguenti queste impostazioni sono identificate rispettivamente come **Modalità client** e **Modalità server**.

### Dove il client RMS archivia le licenze nei computer client
Il client RMS archivia le licenze sul disco locale e memorizza anche nella cache alcune informazioni nel registro di sistema di Windows.

|Descrizione|Percorsi per la modalità client|Percorsi per la modalità server|
|---------------|---------------------|---------------------|
|Percorso dell'archivio delle licenze|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\*<SID>*\|
|Percorso dell'archivio dei modelli|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\Templates\*<SID>*\|
|Percorso del registro di sistema|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*<SID>*|
> [!NOTE]
> *<SID>* è l'ID di sicurezza (SID) dell'account con cui viene eseguita l'applicazione server. Ad esempio, se l'applicazione è in esecuzione con l'account Servizio di rete predefinito, sostituire *<SID>* con il valore SID noto dell'account (S-1-5-20).

### Impostazioni del Registro di sistema di Windows per il client RMS
Per impostare o modificare alcune configurazioni del client RMS, è possibile usare le chiavi del Registro di sistema di Windows. Ad esempio, l'amministratore di applicazioni con il supporto predefinito per RMS che comunicano con server AD RMS può decidere di aggiornare la posizione del servizio aziendale (ovvero ignorare il server AD RMS selezionato per la pubblicazione) in base alla posizione corrente del computer client all'interno della topologia di Active Directory oppure abilitare la traccia di RMS nel computer client per la risoluzione di un problema con un'applicazione con il supporto predefinito per RMS. Usare la tabella seguente per identificare le impostazioni del Registro di sistema che è possibile modificare per il client RMS.

|Attività|Impostazioni|
|--------|------------|
|Solo AD RMS: Per aggiornare il percorso di un servizio aziendale per un computer client|Aggiornare le chiavi seguenti del Registro di sistema:<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />REG_SZ: default<br /><br />**Value:**<http or https>:// *RMS_Cluster_Name*/_wmcs/Certification<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />REG_SZ: default<br /><br />**Value:** <http or https>:// *RMS_Cluster_Name*/_wmcs/Licensing|
|Per abilitare e disabilitare le operazioni di traccia|Aggiornare la chiave seguente del Registro di sistema:<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />REG_DWORD: traccia<br /><br />**Valore:** 1 per abilitare la traccia, 0 per disabilitare la traccia (impostazione predefinita)|
|Per modificare la frequenza in giorni con cui si verifica l'aggiornamento dei modelli|I valori del Registro di sistema seguenti specificano la frequenza di aggiornamento dei modelli nel computer dell'utente se il valore TemplateUpdateFrequencyInSeconds non è impostato.  Se non è impostato alcuno di questi valori, l'intervallo di aggiornamento predefinito per le applicazioni che usano il client RMS (versione 1.0.1784.0) per scaricare i modelli è 1 giorno. Le versioni precedenti hanno un valore predefinito di 7 giorni.<br /><br />**Modalità client:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valore:** valore intero che specifica il numero di giorni (almeno 1) tra i download.<br /><br />**Modalità server:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\*\<SID\>\*<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Value:** Valore intero che specifica il numero di giorni (minimo 1) tra un download e l'altro.|
|Per modificare la frequenza in secondi di aggiornamento dei modelli<br /><br />Importante: se è specificato, il valore in giorni per l'aggiornamento dei modelli viene ignorato. Specificare uno o l'altro, non entrambi.|I valori del Registro di sistema seguenti specificano la frequenza di aggiornamento dei modelli nel computer dell'utente. Se questo valore o il valore di modifica della frequenza in giorni (TemplateUpdateFrequency) non è impostato, l'intervallo di aggiornamento predefinito per le applicazioni che usano il client RMS (versione 1.0.1784.0) per scaricare i modelli è 1 giorno. Le versioni precedenti hanno un valore predefinito di 7 giorni.<br /><br />**Modalità client:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valore:** valore intero che specifica il numero di secondi (almeno 1) tra i download.<br /><br />**Modalità server:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\*\<SID\>\*<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Value:** Valore intero che specifica il numero di secondi (minimo 1) tra un download e l'altro.|
|Solo AD RMS: Per scaricare i modelli immediatamente alla successiva richiesta di pubblicazione|In fase di test e di valutazione, è preferibile che il client RMS scarichi i modelli appena possibile. A tale scopo, rimuovere la chiave del Registro di sistema seguente e il client RMS scaricherà immediatamente i modelli alla successiva richiesta di pubblicazione invece di attendere il tempo specificato dall'impostazione del Registro di sistema TemplateUpdateFrequency:<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<Server Name>\Template<br /><br />**Nota**: <Server Name> può essere sia un URL esterno (corprights.contoso.com) che interno (corprights), ovvero due valori diversi.|
|Solo AD RMS: Per abilitare il supporto dell'autenticazione federata|Se il computer client RMS si connette a un cluster AD RMS usando una relazione di trust federativa, è necessario configurare l'area di autenticazione principale della federazione.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_SZ: FederationHomeRealm<br /><br />**Valore:** il valore di questa voce del Registro di sistema è l'URI (Uniform Resource Identifier) del servizio federativo, ad esempio "http://TreyADFS.trey.net/adfs/services/trust".<br /><br /> **Nota**: è importante specificare http e non https per questo valore. Inoltre, se l'applicazione basata su MSIPC a 32 bit viene eseguita in una versione di Windows a 64 bit, il percorso sarà HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Federation. Per una configurazione di esempio, vedere [Distribuzione di Active Directory Rights Management Services con Active Directory Federation Services](https://technet.microsoft.com/library/dn758110.aspx).|
|Solo AD RMS: per supportare i server federativi partner che richiedono l'autenticazione basata su moduli per l'input utente|Per impostazione predefinita il client RMS viene eseguito in modalità invisibile all'utente e l'input dell'utente non è richiesto. I server federativi partner, tuttavia, potrebbero essere configurati per richiedere l'input dell'utente, ad esempio con l'autenticazione basata su moduli. In questo caso, il client RMS deve essere configurato per ignorare la modalità invisibile all'utente cosicché il modulo di autenticazione federata venga visualizzato in una finestra del browser e l'utente venga innalzato di livello per l'autenticazione.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_DWORD: EnableBrowser<br /><br />**Nota**: se il server federativo è configurato per l'uso dell'autenticazione basata su moduli, questa chiave è obbligatoria. Se il server federativo è configurato per l'uso dell'autenticazione integrata di Windows, questa chiave non è obbligatoria.|
|Solo AD RMS: Per impedire l'utilizzo del servizio ILS|Per impostazione predefinita, il client RMS consente l'utilizzo del contenuto protetto dal servizio ILS, ma può essere configurato per impedirlo impostando la chiave del Registro di sistema seguente. Se questa chiave del Registro di sistema è impostata in modo da impedire il servizio ILS, qualsiasi tentativo di aprire e utilizzare il contenuto protetto dal servizio ILS restituirà l'errore seguente:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: **DisablePassportCertification**<br /><br />**Valore:** 1 per impedire l'utilizzo di contenuto protetto da ILS, 0 per consentirlo (impostazione predefinita)|

### Gestione della distribuzione dei modelli per il client RMS
Per gli utenti e gli amministratori l'uso dei modelli semplifica l'applicazione rapida della protezione Rights Management e il client RMS scarica automaticamente i modelli dai server o dal servizio RMS. Se si inseriscono i modelli nel percorso della cartella seguente, il client RMS non scaricherà alcun modello dal percorso predefinito, ma scaricherà i modelli inseriti in questa cartella. Il client RMS potrebbe continuare a scaricare i modelli dal altri server RMS disponibili.

**Modalità client:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Modalità server:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\\*\<SID\>\*

Quando si usa questa cartella, non sono previste particolari convenzioni di denominazione da seguire purché i modelli siano rilasciati dal server o dal servizio RMS e devono avere l'estensione di file xml. Ad esempio, Contoso-Confidential.xml oppure Contoso-ReadOnly.xml sono nomi validi.

## Solo AD RMS: limitazione del client RMS in modo da usare server AD RMS attendibili
È possibile limitare il client RMS in modo da usare solo specifici server AD RMS attendibili apportando le modifiche seguenti al Registro di sistema di Windows nei computer locali.

**Per limitare il client RMS all'uso di server AD RMS attendibili**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **Valore:** se il valore specificato è diverso da zero, il client RMS considererà attendibili solo i server specificati che sono configurati nell'elenco TrustedServers e nel servizio Azure Rights Management.

**Per aggiungere membri all'elenco di server AD RMS attendibili**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *<URL_o_NomeHost>*

    **Valore:** i valori stringa aggiunti in questa posizione della chiave del Registro di sistema possono essere in formato nome di dominio DNS, (ad esempio **adrms.contoso.com**) oppure URL completi di server AD RMS attendibili (ad esempio **https://adrms.contoso.com**). Se un URL specificato inizia con **https://**, il client RMS userà SSL o TLS per contattare il server AD RMS specificato.

## Individuazione servizio RMS
L'individuazione servizio RMS consente al client RMS di controllare con quale server o servizio RMS comunicare per proteggere il contenuto. L'individuazione del servizio potrebbe verificarsi anche quando il client consuma contenuto protetto, ma è meno probabile che ciò avvenga perché i criteri collegati al contenuto contengono il server o servizio RMS preferito e, solo se non funzionano correttamente, il client esegue l'individuazione del servizio.

L'individuazione del servizio prima cerca una versione locale di Rights Management (AD RMS). Se la ricerca non riesce, l'individuazione del servizio cerca automaticamente la versione cloud di Rights Management (Azure RMS).

Per eseguire l'individuazione del servizio di una distribuzione locale, il client RMS esegue una serie di controlli sui seguenti elementi:

1.  Il Registro di sistema di Windows sul computer locale: Se le impostazioni dell'individuazione servizio sono configurate nel Registro di sistema, verranno provate prima queste impostazioni.  Per impostazione predefinita, queste impostazioni non vengono configurate nel Registro di sistema.

2.  Servizi di dominio Active Directory: un computer aggiunto al dominio esegue una query ad Active Directory relativamente a un punto di connessione del servizio (SCP). Se è stato registrato un punto di connessione del servizio, l'URL del server RMS verrà restituito e usato dal client RMS.

### Solo AD RMS: abilitazione dell'individuazione del servizio sul lato server usando Active Directory
Se l'account ha privilegi sufficienti (Enterprise Admins e amministratore locale per il server AD RMS), è possibile registrare automaticamente un punto di connessione del servizio durante l'installazione del server del cluster radice di AD RMS. Se nella foresta esiste già un punto di connessione del servizio, si deve prima eliminare il punto di connessione del servizio esistente prima di poterne registrare uno nuovo.

È possibile registrare ed eliminare un punto di connessione del servizio dopo aver installato AD RMS usando la procedura seguente. Prima di iniziare, verificare di avere i privilegi richiesti (Enterprise Admins e amministratore locale per il server AD RMS).

#### Per abilitare l'individuazione del servizio AD RMS registrando un punto di connessione del servizio in Active Directory

1.  Aprire la console Servizi di gestione di Active Directory sul server AD RMS:

    -   Se si sta usando Windows Server 2008 R2 o Windows Server 2008, fare clic su **Start**, **Strumenti di amministrazione**e quindi fare clic su **Active Directory Rights Management Services**.

    -   Se si sta usando Windows Server 2012 R2 o Windows Server 2012, fare clic su **Strumenti** in Server Manager e quindi fare clic su **Active Directory Rights Management Services**.

2.  Nella console AD RMS fare clic con il pulsante destro del mouse sul cluster AD RMS e quindi fare clic su **Proprietà**.

3.  Fare clic sulla scheda **SCP** .

4.  Selezionare la casella di controllo **Cambia SCP** .

5.  Selezionare l'opzione **Imposta SCP sul cluster di certificazione corrente** e quindi fare clic su **OK**.

### Abilitazione dell'individuazione del servizio sul lato client usando il Registro di sistema di Windows
In alternativa all'uso di un punto di connessione del servizio o se tale punto non esiste, è possibile configurare il Registro di sistema sul computer client in modo che il client RMS possa trovare il relativo server AD RMS.

#### Per abilitare l'individuazione del servizio AD RMS usando il Registro di sistema di Windows

1.  Aprire l'editor del Registro di sistema di Windows, ovvero Regedit.exe:

    -   Nella finestra Esegui del computer client digitare **regedit** e quindi premere Invio per aprire l'editor del Registro di sistema.

2.  Nell'editor del Registro di sistema passare a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!IMPORTANT]
    > Se si esegue un'applicazione a 32 bit in un computer a 64 bit, il percorso sarà il seguente: **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  Per creare la sottochiave ServiceLocation, fare clic con il pulsante destro del mouse su **MSIPC**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **ServiceLocation**.

4.  Per creare la sottochiave EnterpriseCertification, fare clic con il pulsante destro del mouse su **ServiceLocation**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **EnterpriseCertification**.

5.  Per impostare l'URL di certificazione globale (enterprise), fare doppio clic sul valore **(Predefinito)** nella sottochiave **EnterpriseCertification** e quando viene visualizzata la finestra di dialogo **Modifica stringa** in **Dati valore** digitare <http or https>://*AD RMS_cluster_name*/_wmcs/Certification, quindi fare clic su **OK**.

6.  Per creare la sottochiave EnterprisePublishing, fare clic con il pulsante destro del mouse su **ServiceLocation**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare EnterprisePublishing.

7.  Per impostare l'URL di pubblicazione globale (enterprise), fare doppio clic su **(Predefinito)** nella sottochiave **EnterprisePublishing** e quando viene visualizzata la finestra di dialogo **Modifica stringa** in **Dati valore** digitare <http or https>://*AD RMS_cluster_name*/_wmcs/Licensing, quindi fare clic su **OK**.

8.  Chiudere l'editor del Registro di sistema.

Se RMS non riesce a trovare un punto di connessione del servizio eseguendo una query ad Active Directory e non è specificato nel Registro di sistema, le chiamate di individuazione del servizio per AD RMS avranno esito negativo.

### Reindirizzamento del traffico del server delle licenze
In alcuni casi, potrebbe essere necessario reindirizzare il traffico durante l'individuazione del servizio, ad esempio quando vengono fuse due organizzazioni e il server licenze precedente di un'organizzazione viene rimosso e i client devono essere reindirizzati a un nuovo server licenze oppure si esegue la migrazione da AD RMS ad Azure RMS. Per abilitare il reindirizzamento delle licenze, usare la procedura seguente.

#### Per abilitare il reindirizzamento delle licenze RMS usando il Registro di sistema di Windows

1.  Aprire l'editor del Registro di sistema di Windows, ovvero Regedit.exe:

    -   Nella finestra Esegui del computer client digitare **regedit** e quindi premere Invio per aprire l'editor del Registro di sistema.

2.  Nell'editor del Registro di sistema passare a una delle posizioni seguenti:

    -   Versione a 64 bit di Office su piattaforma x64: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   Versione a 32 bit di Office su piattaforma x64: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Creare una sottochiave LicensingRedirection facendo clic con il pulsante destro del mouse su **Servicelocation**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **LicensingRedirection**.

4.  Per impostare il reindirizzamento delle licenze, fare clic con il pulsante destro del mouse sulla sottochiave **LicensingRedirection**, selezionare **Nuovo** e quindi selezionare **Valore stringa**.  In **Nome**specificare l'URL delle licenze server precedente e in **Valore** specificare il nuovo URL delle licenze server.

    Ad esempio, per reindirizzare le licenze da un server presso Contoso.com a uno in Fabrikam.com,è possibile immettere i valori seguenti:

    **Nome:** https://contoso.com/_wmcs/licensing

    **Valore:** https://fabrikam.com/_wmcs/licensing

    > [!NOTE]
    > Se per il server licenze precedente sono specificati sia l'URL Intranet che l'URL Extranet, è necessario impostare un nuovo mapping nome/valore per entrambi gli URL nella chiave LicensingRedirection.

5.  Ripetere il passaggio precedente per tutti i server da reindirizzare.

6.  Chiudere l'editor del Registro di sistema.




<!--HONumber=Jun16_HO4-->


