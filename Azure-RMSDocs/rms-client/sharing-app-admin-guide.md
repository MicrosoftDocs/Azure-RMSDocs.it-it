---
title: Guida dell'amministratore dell'applicazione RMS sharing - AIP
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione dell'applicazione Microsoft Rights Management sharing per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/27/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7be58d201ddd24497ff79935554c2a68efd04a3f
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53024434"
---
# <a name="rights-management-sharing-application-administrator-guide"></a>Guida dell'amministratore dell'applicazione Rights Management sharing

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

> [!IMPORTANT]
> **Notifica di fine del supporto**: l'applicazione di condivisione Rights Management per Windows verrà sostituita dal [client Azure Information Protection](aip-client.md). Il supporto per questa applicazione precedente terminerà il 31 gennaio 2019. 

Usare le informazioni seguenti se l'utente è responsabile dell'applicazione Microsoft Rights Management sharing in una rete aziendale o se si vogliono informazioni più tecniche rispetto a quelle presenti in [Guida dell'utente dell'applicazione Rights Management sharing](sharing-app-user-guide.md) o [Domande frequenti sull'applicazione Microsoft Rights Management sharing per Windows](https://go.microsoft.com/fwlink/?LinkId=303971).

L'applicazione RMS sharing è particolarmente adatta all'uso con Azure Information Protection perché questa configurazione di distribuzione supporta l'invio di allegati protetti agli utenti in un'altra organizzazione e opzioni quali le notifiche tramite posta elettronica e il rilevamento dei documenti con revoca. Tuttavia, con alcune limitazioni, funziona anche con la versione locale, AD RMS. Per un confronto completo delle funzionalità supportate da Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](../compare-on-premise.md). Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).

Per una panoramica tecnica dell'applicazione Rights Management sharing e per informazioni sulla protezione nativa e generica, sui tipi di file supportati, sulle estensioni del nome dei file e su come modificare il livello di protezione predefinito, vedere [Panoramica tecnica dell'applicazione Rights Management sharing](sharing-app-admin-guide-technical.md). 

## <a name="automatic-deployment-for-the-microsoft-rights-management-sharing-application"></a>Distribuzione automatica dell'applicazione Microsoft Rights Management sharing
La versione di Windows dell'applicazione di condivisione RMS supporta un'installazione tramite script, che la rende ideale per le distribuzioni aziendali.

Gli unici prerequisiti per l'installazione sono che i computer eseguano almeno Windows 7 Service Pack 1 e che sia installata almeno la versione 4.0 di Microsoft Framework. Se è necessario installare Microsoft .NET Framework 4.0, è possibile [scaricarlo per l'installazione dall'Area Download Microsoft](http://www.microsoft.com/download/details.aspx?id=17718).

### <a name="to-download-the-rms-sharing-application-for-automatic-deployment"></a>Per scaricare l'applicazione RMS sharing per la distribuzione automatica.

1.  Visitare la pagina [Applicazione Microsoft Rights Management sharing per Windows](http://www.microsoft.com/download/details.aspx?id=40857) nel Microsoft Download Center e fare clic su **Download**.

2.  Selezionare e scaricare i file necessari. Sono disponibili due pacchetti di installazione client: uno per Windows a 64 bit (Microsoft Rights Management sharing application x64.zip) e l'altro per Windows a 32 bit (Microsoft Rights Management sharing application x86.zip).

3.  Estrarre i file dai pacchetti di installazione compressi, ad esempio facendo doppio clic sui nomi. Quindi copiare i file estratti in un percorso di rete a cui possono accedere ai computer client.

I pacchetti di installazione per l'applicazione RMS sharing supportano diversi scenari di distribuzione e includono quanto segue:

|Descrizione|Scenario di distribuzione|
|---------------|-----------------------|
|Assistente per l'accesso ai Microsoft Online Services|Office 2010 e Azure Information Protection<br /><br />Office 2013 e Azure Information Protection se non è stato installato [l'aggiornamento per Office 2013 del 9 giugno 2015](https://support.microsoft.com/kb/3054853) (KB 3054853)|
|Hotfix per Office (KB 2596501)|Office 2010 e Azure Information Protection<br /><br />Office 2010 e Active Directory RMS|
|Hotfix per abilitare AD RMS Client 1.0 per l'uso con Azure Information Protection (KB 2843630)|Office 2010 e Azure Information Protection<br /><br />Office 2010 e Active Directory RMS|
|Client AD RMS e applicazione RMS sharing|Office 2016 o Office 2013 e Azure Information Protection o Active Directory RMS<br /><br />Office 2010 e Azure Information Protection<br /><br />Office 2010 e Active Directory RMS<br /><br />Solo applicazione RMS sharing e componente aggiuntivo di Office|
|Componente aggiuntivo di Office per la barra multifunzione|Office 2016 o Office 2013 e Azure Information Protection o Active Directory RMS<br /><br />Office 2010 e Azure Information Protection<br /><br />Office 2010 e Active Directory RMS<br /><br />Solo applicazione RMS sharing e componente aggiuntivo di Office|
|Strumento di preparazione Rights Management di Azure Active Directory|Office 2010 e Azure Information Protection|
Utilizzare le procedure seguenti per identificare i comandi necessari per distribuire l'applicazione RMS sharing per questi scenari di distribuzione:

-   **Office 2016 o Office 2013 e Azure Information Protection o Active Directory RMS**

    Gli utenti eseguono Office 2016 o Office 2013, l'organizzazione usa Azure Information Protection o Active Directory RMS e gli utenti collaborano con altre organizzazioni che usano Azure Information Protection o Active Directory RMS.

-   **Office 2010 e Azure Information Protection**

    Gli utenti eseguono Office 2010, l'organizzazione usa Azure Information Protection e gli utenti collaborano con altre organizzazioni che usano Azure Information Protection o Active Directory RMS.

-   **Office 2010 e Active Directory RMS**

    Gli utenti eseguono Office 2010, l'organizzazione usa AD RMS e gli utenti collaborano con altre organizzazioni che usano Azure Information Protection.

-   **Solo applicazione RMS sharing e componente aggiuntivo di Office**

    Gli utenti eseguono Office 2016, Office 2013 oppure Office 2010, l'organizzazione usa AD RMS e gli utenti non hanno bisogno di collaborare con altre organizzazioni che usano Azure Information Protection. Questa installazione consente di installare solo l'applicazione di condivisione e il componente aggiuntivo di Office.

> [!NOTE]
> In questi scenari, se l'organizzazione esegue AD RMS, gli utenti possono ricevere contenuto protetto da altre organizzazioni che usano Azure Information Protection, ma non possono inviare contenuto protetto agli utenti di un'organizzazione che usa Azure Information Protection. Tuttavia, se l'organizzazione esegue Azure Information Protection, gli utenti possono inviare e ricevere contenuto protetto da altre organizzazioni.

Per completare l'installazione per ogni procedura, è necessario riavviare il computer. È possibile avviare un'operazione di riavvio automatico tramite un comando, ad esempio **shutdown /i**.

### <a name="to-deploy-the-rms-sharing-application-for-office2016-or-office-2013-and-azure-information-protection-or-active-directory-rms"></a>Per distribuire l'applicazione RMS sharing per Office 2016 o Office 2013 e Azure Information Protection o Active Directory RMS

-   In ogni computer in cui si vuole installare l'applicazione RMS sharing e i relativi componenti, eseguire il comando seguente con privilegi elevati:

    ```
    setup.exe /s
    ```

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

### <a name="to-deploy-the-rms-sharing-application-for-office-2010-and-azure-information-protection"></a>Per distribuire l'applicazione RMS sharing per Office 2010 e Azure Information Protection

1.  È necessario essere l'amministratore globale del tenant di Office 365 o di Azure Active Directory in modo da ottenere l'URL del servizio di certificazione dell'organizzazione eseguendo l'utilità di preparazione di Azure Active Directory Rights Management. È necessario eseguire questo strumento una sola volta, in un singolo computer. Quando si installa l'applicazione RMS sharing in ogni computer, si userà l'URL del servizio di certificazione:

    1.  Accedere a un computer utilizzando un account amministratore locale.

    2.  In tale computer [scaricare e installare l’Assistente per l’accesso a Microsoft Online](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Eseguire il comando seguente per vedere visualizzato sullo schermo l'URL del servizio di certificazione, che è possibile poi copiare e salvare per il passaggio successivo:

        -   Per Windows 8.1 e Windows 8, a 64 bit:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Per Windows 8.1 e Windows 8, a 32 bit:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Per Windows 7, a 64 bit:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Questo comando potrebbe richiedere di immettere le credenziali per Azure. Se il computer non è unito a un dominio, verrà richiesto di farlo. Se il computer è unito a un dominio, lo strumento potrebbe essere in grado di utilizzare credenziali memorizzate nella cache.

2.  In ogni computer in cui si installerà l'applicazione RMS sharing eseguire una volta il comando seguente con privilegi elevati:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  In ogni computer in cui si installerà l'applicazione RMS sharing ogni utente di tale computer deve eseguire il comando seguente (non servono privilegi elevati). Esistono diversi modi per ottenere tale scopo, tra cui chiedere agli utenti di eseguire il comando (ad esempio, un collegamento in un messaggio di posta elettronica o un collegamento nel portale di supporto tecnico) oppure è possibile aggiungere i relativi script di accesso:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

### <a name="to-deploy-the-rms-sharing-application-for-office2010-and-active-directoryrms"></a>Per distribuire l'applicazione di condivisione RMS per Office 2010 e Active Directory RMS

1.  In ogni computer in cui si installerà l'applicazione RMS sharing, eseguire il comando seguente con privilegi elevati:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  In ogni computer in cui si installerà l'applicazione RMS sharing gli utenti devono eseguire i comandi seguenti (non servono privilegi elevati). Esistono diversi modi per ottenere tale scopo, tra cui chiedere agli utenti di eseguire i comandi (ad esempio, un collegamento in un messaggio di posta elettronica o un collegamento nel portale di supporto tecnico) oppure è possibile aggiungere i relativi script di accesso:

    -   Per Windows 10, Windows 8.1 e Windows 8, a 64 bit:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Per Windows 10, Windows 8.1 e Windows 8, a 32 bit:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Per Windows 7 a 64 bit:

            pushd x64\win7
            aadrmpep.exe /configureO2010
            popd

    -   Per Windows 7, a 32 bit:

            pushd x86\win7
            aadrmpep.exe /configureO2010
            popd


Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

### <a name="to-install-the-rms-sharing-application-and-office-add-in-only"></a>Per installare solo l'applicazione RMS sharing e il componente aggiuntivo di Office

1.  Installare il client AD RMS e l'applicazione di condivisione RMS tramite il comando seguente e specificando una cartella esistente per la creazione del file di log:

    -   Per Windows a 64 bit:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Per Windows a 32 bit:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    ad esempio `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`
    
    Se questo comando ha esito negativo, non verrà visualizzato nessun messaggio di errore perché è stato specificato il parametro **/quiet**. Per risolvere il problema dell'installazione non riuscita, eseguire nuovamente il comando senza il parametro /quiet per visualizzare eventuali messaggi di errore.

2.  Installare il componente aggiuntivo di Office tramite i comandi seguenti e specificando una cartella esistente per la creazione del file di log:

    -   Per la versione di Office a 64 bit:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Per la versione di Office a 32 bit:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    ad esempio `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`
    
    Se questo comando ha esito negativo, non verrà visualizzato nessun messaggio di errore perché è stato specificato il parametro **/quiet**. Per risolvere il problema dell'installazione non riuscita, eseguire nuovamente il comando senza il parametro /quiet per visualizzare eventuali messaggi di errore.

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

## <a name="verifying-installation-success"></a>Verificare l'esito positivo dell’installazione
È possibile utilizzare i file di log di installazione per verificare la corretta installazione.

### <a name="to-verify-installation-success-for-the-rms-sharing-application-for-office2016-or-office-2013-and-azure-information-protection-or-active-directory-rms"></a>Per verificare l'esito positivo dell'installazione per l'applicazione RMS sharing per Office 2016 o Office 2013 e Azure Information Protection o Active Directory RMS

-   Per verificare l'esito positivo del comando Setup.exe, cercare in ogni computer il file di log di installazione **RMInstaller.log** nella cartella *%temp%\RMS_installer_&lt;guid&gt;*, quindi individuare il codice di uscita.

    Una corretta installazione dispone di un codice di uscita pari a 0 e qualsiasi altro numero indica un'installazione non riuscita.

    Esempio del nome del file di log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### <a name="to-verify-installation-success-for-the-rms-sharing-application-for-office2010-and-azure-information-protection"></a>Per verificare l'esito positivo dell'installazione per l'applicazione RMS sharing per Office 2010 e Azure Information Protection

1.  Per verificare l'esito positivo del comando Setup.exe, cercare in ogni computer il file di log di installazione **RMInstaller.log** nella cartella *%temp%\RMS_installer_&lt;guid&gt;*, quindi individuare il codice di uscita.

    Una corretta installazione dispone di un codice di uscita pari a 0 e qualsiasi altro numero indica un'installazione non riuscita.

    Esempio del nome del file di log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Per verificare l'esito positivo per il comando RMSSetup.exe, è necessario che siano stati creati i file seguenti nella cartella *%localappdata%\microsoft\drm*:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    Esempio di un file CLC-&#42;.drm:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### <a name="to-verify-installation-success-for-the-rms-sharing-application-for-office-2010-and-active-directory-rms"></a>Per verificare l'esito positivo dell'installazione per l'applicazione RMS sharing per Office 2010 e Active Directory RMS

1.  Per verificare l'esito positivo del comando Setup.exe, cercare in ogni computer il file di log di installazione nella cartella *%temp%\RMS_installer_&lt;guid&gt;* e individuare il codice di uscita.

    Una corretta installazione dispone di un codice di uscita pari a 0 e qualsiasi altro numero indica un'installazione non riuscita.

    Esempio del nome del file di log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Per verificare l'esito positivo del comando aadrmprep.exe, in ogni computer, cercare il testo seguente nel file di log di installazione: **aadrmprep.exe si è concluso con lo status ESITO POSITIVO**

    > [!NOTE]
    > In alcuni casi, l'installazione può eseguire due volta; la prima occorrenza avrà esito negativo e il secondo esito positivo.

    Se si desidera controllare manualmente le modifiche applicate dall’utilità nel Registro di sistema, sono disponibili di seguito:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### <a name="to-verify-installation-success-for-the-rms-sharing-application-and-office-add-in-only"></a>Per verificare l'esito positivo dell'installazione solo per l'applicazione RMS sharing e il componente aggiuntivo di Office

1.  Per verificare l'esito positivo del comando Setup_ipviewer.exe, cercare il testo seguente nel file di log di installazione: **Installazione riuscita o stato di errore: 0**

    Righe di esempio da un'installazione corretta:

    **MSI (s) (F0:B8) [14:19:57:854]: Prodotto: Active Directory Rights Management Services Client 2.1 - Installazione completata.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer: installazione del prodotto completata. Nome prodotto: Active Directory Rights Management Services Client 2.1. Versione del prodotto: 1.0.1179.1. Lingua del prodotto: 1033. Produttore: Microsoft Corporation Stato di esito positivo o di errore nell'installazione: 0.**

2.  Per verificare l'esito positivo del componente aggiuntivo Office, su ogni computer, cercare il testo seguente nel file di log di installazione: **Installazione riuscita o stato di errore: 0**

    Righe di esempio da un'installazione corretta:

    **MSI (s) (9C:88) [18:49:04:007]: Prodotto: Componenti aggiuntivi di Office per Microsoft RMS - Installazione completata.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer: installazione del prodotto completata. Nome prodotto: Componenti aggiuntivi di Office per Microsoft RMS. Versione del prodotto: 1.0.7. Lingua del prodotto: 1033. Produttore: Microsoft Stato di esito positivo o di errore nell'installazione: 0.**

## <a name="uninstall-commands"></a>Disinstallare i comandi
Non tutti i comandi di installazione necessari per tali distribuzioni supportano un comando di disinstallazione. È possibile disinstallare il client AD RMS, l'applicazione RMS sharing e il componente aggiuntivo di Office. Utilizzare i comandi seguenti per disinstallare questi elementi.

### <a name="to-uninstall-the-adrms-client-and-the-rms-sharing-application"></a>Per disinstallare il Client AD RMS e l’applicazione di condivisione RMS

-   Usare i seguenti comandi:

    -   Per Windows a 64 bit:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Per Windows a 32 bit:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### <a name="to-uninstall-the-office-add-in"></a>Per disinstallare il componente aggiuntivo di Office

-   Usare i seguenti comandi:

    -   Per Windows a 64 bit:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Per Windows a 32 bit:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## <a name="suppressing-automatic-updates"></a>Eliminazione degli aggiornamenti automatici
Per impostazione predefinita, gli utenti vengono informati se esiste una versione più recente di RMS sharing e viene loro chiesto di scaricarla. È possibile eliminare questa notifica apportando la seguente modificare al Registro di sistema:

1.  Passare a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e, se non è già presente, creare una nuova chiave denominata **RmsSharingApp**.

2.  Selezionare **RmsSharingApp**, creare un nuovo valore DWORD di **AllowUpdatePrompt**, e impostare il valore su **0**.

Poiché l'applicazione RMS sharing non è supportata da WSUS, è possibile usare la tecnica seguente per verificare le eventuali nuove versioni dell'applicazione RMS sharing prima di distribuirla a tutti gli utenti:

1.  Nei computer di tutti gli utenti, eseguire uno script per eliminare gli aggiornamenti automatici. Nei computer utilizzati dagli amministratori per verificare le nuove versioni, non eseguire questo script.

2.  Quando una nuova versione è disponibile, gli amministratori la scaricano e la testano.

3.  Quando il test è completo e i problemi sono risolti, distribuire la versione più recente a tutti gli utenti utilizzando le istruzioni di distribuzione automatica in questa Guida.

## <a name="azure-information-protection-only-configuring-document-tracking"></a>Solo Azure Information Protection: Configurazione del rilevamento dei documenti
Se si dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://www.microsoft.com/cloud-platform/azure-information-protection-features), il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione. Il rilevamento dei documenti mostra informazioni quali indirizzi di posta elettronica delle persone che hanno tentato di accedere ai documenti protetti condivisi dagli utenti, nel momento in cui queste persone hanno tentato di accedere, e la loro posizione. Se la visualizzazione di queste informazioni non è consentita all'interno dell'organizzazione a causa dei requisiti sulla privacy, è possibile disabilitare l'accesso al sito di rilevamento dei documenti tramite il cmdlet [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). È possibile riabilitare l'accesso al sito in qualsiasi momento utilizzando [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature), ed è possibile verificare se l'accesso è attualmente abilitato o disabilitato utilizzando [Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature).

Per eseguire questi cmdlet, è necessario disporre almeno della versione **2.3.0.0** del modulo Azure Rights Management per Windows PowerShell. Per le istruzioni di installazione, vedere [Installazione del modulo PowerShell AADRM](../install-powershell.md).

> [!TIP]
> Se il modulo è stato scaricato e installato in precedenza, verificarne il numero di versione eseguendo: `(Get-Module aadrm –ListAvailable).Version`

Gli URL seguenti vengono utilizzati per il rilevamento dei documenti e devono essere consentiti (ad esempio, aggiungerli ai siti attendibili se si utilizza Internet Explorer con protezione avanzata):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > questo URL è per Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### <a name="tracking-and-revoking-documents-for-users"></a>Rilevamento e revoca dei documenti per gli utenti

Quando gli utenti accedono al sito di rilevamento dei documenti, possono tenere traccia dei documenti condivisi e revocarli tramite l'applicazione RMS sharing. Quando si accede come amministratore di Azure Information Protection (amministratore globale), è possibile fare clic sull'icona di amministrazione nella parte superiore destra della pagina per passare alla modalità amministratore in modo da visualizzare i documenti che sono stati condivisi dagli utenti dell'organizzazione.

Le azioni intraprese in modalità amministratore vengono controllate e registrate nei file di log dei dati di utilizzo e, per continuare, è necessario confermare. Per altre informazioni su questa registrazione, vedere la sezione seguente.

Quando si è in modalità amministratore, è quindi possibile eseguire la ricerca in base all'utente o al documento. Se si esegue la ricerca in base all'utente, si visualizzeranno tutti i documenti che l'utente specificato ha condiviso. Se si esegue la ricerca in base al documento, si visualizzeranno tutti gli utenti dell'organizzazione che hanno condiviso tale documento. È quindi possibile analizzare i risultati della ricerca per rilevare i documenti che gli utenti hanno condiviso e, se necessario, revocarli. 

Per uscire dalla modalità amministratore, fare clic su **X** accanto a **Esci dalla modalità amministratore**.

Per istruzioni su come usare il sito di rilevamento dei documenti, vedere [Tenere traccia dei documenti e revocarli](sharing-app-track-revoke.md) nella Guida dell'utente.



### <a name="usage-logging-for-the-document-tracking-site"></a>Registrazione dei dati di utilizzo per il sito di rilevamento dei documenti

Nei file di log dei dati di utilizzo sono presenti due campi applicabili al rilevamento dei documenti: **AdminAction** e **ActingAsUser**.

**AdminAction**: questo campo ha un valore true quando un amministratore usa il sito di rilevamento dei documenti in modalità amministratore, ad esempio, per revocare un documento per conto dell'utente o per visualizzare quando il documento è stato condiviso. Questo campo è vuoto quando l'accesso al sito di rilevamento dei documenti viene eseguito dall'utente.

**ActingAsUser**: quando il campo AdminAction è true, questo campo contiene il nome utente per conto del quale agisce l'amministratore per eseguire la ricerca di un utente o del proprietario di un documento. Questo campo è vuoto quando l'accesso al sito di rilevamento dei documenti viene eseguito dall'utente. 

Sono inoltre disponibili tipi di richieste che registrano la modalità in cui utenti e amministratori stanno usando il sito di rilevamento dei documenti. **RevokeAccess**, ad esempio, è il tipo di richiesta usato quando un utente, o un amministratore che agisce per conto dell'utente, revoca un documento nel sito di rilevamento dei documenti. Usare questo tipo di richiesta in combinazione con il campo AdminAction per determinare se il documento è stato revocato dal relativo utente (il campo AdminAction è vuoto) o se un amministratore ha revocato un documento per conto di un utente (il campo AdminAction è true).


Per altre informazioni sulla registrazione dell'utilizzo, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../log-analyze-usage.md)

## <a name="ad-rms-only-support-for-multiple-email-domains-within-your-organization"></a>Solo AD RMS: Supporto per più domini di posta elettronica all'interno dell'organizzazione
Se si usa AD RMS e gli utenti dell'organizzazione hanno più domini di posta elettronica, magari in seguito a una fusione o acquisizione, è necessario apportare la modifica seguente nel Registro di sistema:

1.  Passare a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e, se non è già presente, creare una nuova chiave denominata **RmsSharingApp**.

2.  Selezionare **RmsSharingApp**, creare un nuovo valore multistringa denominato **FederatedDomains** e poi aggiungere i domini e i sotto-domini utilizzati dall'organizzazione. I caratteri jolly non sono supportati.

    Ad esempio: la società Coho Vineyard &amp; Winery ha il dominio di posta elettronica standard **cohovineyardandwinery.com**, ma in seguito alle fusioni vengono usati anche i domini di posta elettronica **cohowinery.com**, **eastcoast.cohowinery.com** e **cohovineyard**. Per i dati di valore **FederatedDomains**, l'amministratore immette: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Se non si apporta questa modifica al Registro di sistema, gli utenti potrebbero non essere in grado di utilizzare contenuti protetti da altri utenti nella propria organizzazione. Questa modifica del Registro di sistema non è necessaria se si usa Azure Information Protection.


## <a name="next-steps"></a>Passaggi successivi
Per informazioni tecniche aggiuntive, inclusa la spiegazione della differenza tra i livelli di protezione (nativi e generici), i tipi di file supportati, le estensioni del nome dei file e la modalità di modifica del livello di protezione predefinito, vedere [Panoramica tecnica dell'applicazione Rights Management sharing](sharing-app-admin-guide-technical.md).

