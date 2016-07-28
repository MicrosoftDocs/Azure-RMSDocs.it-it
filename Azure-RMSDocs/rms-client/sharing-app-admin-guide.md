---
title: Guida dell'amministratore dell'applicazione di condivisione Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a58d50b33db95570b43fe1ec0f76bdf490ddd024
ms.openlocfilehash: 164df467632b38f179d1c1192835f919641331a5


---


# Guida dell'amministratore dell'applicazione di condivisione Rights Management

*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*


Utilizzare le seguenti informazioni se l'utente è responsabile per l'applicazione di condivisione Rights Management di Microsoft in una rete aziendale, o se si desiderano informazioni più tecniche rispetto a quelle presenti in [Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md) o [Domande frequenti per l’applicazione di condivisione Rights Management di Microsoft per Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

L’applicazione di condivisione RMS è più adatta per l'utilizzo con Azure RMS, perché questa configurazione di distribuzione supporta l'invio di allegati protetti agli utenti in un'altra organizzazione e opzioni quali le notifiche tramite posta elettronica e il rilevamento dei documenti con revoca.  Tuttavia, con alcune limitazioni, funziona anche con la versione locale, AD RMS. Per un confronto completo delle funzionalità supportate da Azure RMS e AD RMS, vedere [Confronto di Rights Management di Azure e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). Se si dispone di AD RMS e si desidera eseguire la migrazione ad Azure RMS, vedere [Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

Per una panoramica tecnica dell'applicazione di condivisione Rights Management e per informazioni sulla protezione nativa e generica, sui tipi di file supportati, sulle estensioni del nome dei file e su come modificare il livello di protezione predefinito, vedere [Panoramica tecnica dell'applicazione di condivisione Rights Management](sharing-app-admin-guide-technical.md). 

## Distribuzione automatica dell'applicazione di condivisione Microsoft Rights Management
La versione di Windows dell'applicazione di condivisione RMS supporta un'installazione tramite script, che la rende ideale per le distribuzioni aziendali.

I soli prerequisiti per le installazioni sono che il computer esegua una versione minima di Windows 7 Service Pack 1 e che sia installata la versione minima 4.0 di Microsoft Framework. Se è necessario installare Microsoft .NET Framework 4.0, è possibile [Scaricarlo per l'installazione da Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=17718).

### Per scaricare l'applicazione di condivisione RMS per la distribuzione automatica.

1.  Visitare la pagina [Applicazione di condivisione Rights Management di Microsoft per Windows](http://www.microsoft.com/download/details.aspx?id=40857) nel Microsoft Download Center e fare clic su **Download**.

2.  Selezionare e scaricare i file necessari. Sono disponibili due pacchetti di installazione client: uno per Windows a 64 bit (applicazione di condivisione Microsoft Rights Management x64.zip) e l'altro per Windows a 32 bit (applicazione di condivisione Microsoft Rights Management x86.zip).

3.  Estrarre i file dai pacchetti di installazione compressi, ad esempio facendo doppio clic sui nomi. Quindi copiare i file estratti in un percorso di rete a cui possono accedere ai computer client.

I pacchetti di installazione per l'applicazione di condivisione RMS supporta diversi scenari di distribuzione e include quanto segue:

|Descrizione|Scenario di distribuzione|
|---------------|-----------------------|
|Assistente per l'accesso ai Microsoft Online Services|Office 2010 e Azure RMS<br /><br />Office 2013 e Azure RMS se non è stato installato [l'aggiornamento per Office 2013 del 9 giugno 2015](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Hotfix per Office (KB 2596501)|Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS|
|Aggiornamento rapido per abilitare il Client AD RMS 1.0 a lavorare con Azure RMS (2843630 KB)|Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS|
|Client AD RMS e applicazione di condivisione RMS|Office 2016 o Office 2013 e Azure RMS o Active Directory RMS<br /><br />Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS<br /><br />Solo applicazione di condivisione RMS e componente aggiuntivo di Office|
|Componente aggiuntivo di Office per la barra multifunzione|Office 2016 o Office 2013 e Azure RMS o Active Directory RMS<br /><br />Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS<br /><br />Solo applicazione di condivisione RMS e componente aggiuntivo di Office|
|Strumento di preparazione Rights Management di Azure Active Directory|Office 2010 e Azure RMS|
Utilizzare le procedure seguenti per identificare i comandi necessari per distribuire l'applicazione di condivisione RMS per questi scenari di distribuzione:

-   **Office 2016 o Office 2013 e Azure RMS o Active Directory RMS**

    Gli utenti eseguono Office 2016 o Office 2013, l'organizzazione utilizza Azure RMS o Active Directory RMS e gli utenti collaborano con altre organizzazioni che utilizzano Azure RMS o Active Directory RMS.

-   **Office 2010 e Azure RMS**

    Gli utenti eseguono Office 2010, l'organizzazione utilizza Azure RMS e gli utenti collaborano con altre organizzazioni che utilizzano Azure RMS o Active Directory RMS.

-   **Office 2010 e Active Directory RMS**

    Gli utenti eseguono Office 2010, l'organizzazione utilizza AD RMS e gli utenti collaborano con altre organizzazioni che utilizzano Azure RMS.

-   **Solo applicazione di condivisione RMS e componente aggiuntivo di Office**

    Gli utenti eseguono Office  2016, Office 2013 oppure Office 2010, l'organizzazione utilizza AD RMS e gli utenti non hanno bisogno di collaborare con altre organizzazioni che utilizzano Azure RMS. Questa installazione consente di installare solo l'applicazione di condivisione e il componente aggiuntivo di Office.

> [!NOTE]
> In questi scenari, se l'organizzazione esegue AD RMS, gli utenti possono ricevere il contenuto protetto da altre organizzazioni che utilizzano Azure RMS, ma gli utenti non possono inviare contenuti protetti agli utenti di un'organizzazione che utilizza Azure RMS. Tuttavia, se l'organizzazione esegue Azure RMS, gli utenti possono inviare e ricevere contenuto protetto da altre organizzazioni.

Per completare l'installazione per ogni procedura, è necessario riavviare il computer. È possibile avviare un'operazione di riavvio automatico tramite un comando, ad esempio **shutdown /i**.

### Per distribuire l'applicazione di condivisione RMS per Office 2016 o Office 2013 e Azure RMS o Active Directory RMS

-   In ogni computer in cui si desidera installare l'applicazione di condivisione RMS e dei relativi componenti, eseguire il comando seguente con privilegi elevati:

    ```
    setup.exe /s
    ```

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

### Per distribuire l'applicazione di condivisione RMS per Office 2010 e Azure RMS

1.  È necessario essere amministratore globale per il tenant di Office 365 o Azure Active Directory in modo che sia possibile ottenere l'URL del servizio di certificazione dell'organizzazione eseguendo lo strumento di preparazione di Azure Active Directory Rights Management. È necessario eseguire questo strumento una sola volta, in un singolo computer. Quando si installa l'applicazione di condivisione RMS in ogni computer, si utilizzerà l'URL del servizio di certificazione:

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

2.  In ogni computer in cui si installerà l'applicazione di condivisione RMS eseguire una volta il comando seguente con privilegi elevati:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  In ogni computer in cui si installerà l'applicazione di condivisione RMS ogni utente del computer deve eseguire il comando seguente (non servono privilegi elevati). Esistono diversi modi per ottenere tale scopo, tra cui chiedere agli utenti di eseguire il comando (ad esempio, un collegamento in un messaggio di posta elettronica o un collegamento nel portale di supporto tecnico) oppure è possibile aggiungere i relativi script di accesso:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

### Per distribuire l'applicazione di condivisione RMS per Office 2010 e Active Directory RMS

1.  In ogni computer in cui si installerà l'applicazione di condivisione RMS, eseguire il comando seguente con privilegi elevati:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  In ogni computer in cui si installerà l'applicazione di condivisione RMS,gli utenti devono eseguire il comando seguente (non servono privilegi elevati). Esistono diversi modi per ottenere tale scopo, tra cui chiedere agli utenti di eseguire il comando (ad esempio, un collegamento in un messaggio di posta elettronica o un collegamento nel portale di supporto tecnico) oppure è possibile aggiungere i relativi script di accesso:

    -   Per Windows 10, Windows 8.1 e Windows 8, a 64 bit:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Per Windows 10, Windows 8.1 e Windows 8, a 32 bit:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Per Windows 7, a 64 bit:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

### Per installare solo l'applicazione di condivisione RMS e il componente aggiuntivo di Office

1.  Installare il Client AD RMS e l’applicazione di condivisione utilizzando il comando seguente:

    -   Per Windows a 64 bit:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Per Windows a 32 bit:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Ad esempio: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installare il componente aggiuntivo di Office utilizzando i comandi seguenti:

    -   Per la versione di Office a 64 bit:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Per la versione di Office a 32 bit:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    Ad esempio: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

Per verificare l'esito positivo, vedere la sezione [Verificare l'esito positivo dell’installazione](#verifying-installation-success) di questo articolo.

## Verificare l'esito positivo dell’installazione
È possibile utilizzare i file di log di installazione per verificare la corretta installazione.

### Per verificare l'esito positivo di installazione per l'applicazione di condivisione RMS per Office 2016 o Office 2013 e Azure RMS o Active Directory RMS

-   Per verificare l'esito positivo del comando Setup.exe, cercare in ogni computer il file di log di installazione **RMInstaller.log** nella cartella *%temp%\RMS_installer_&lt;guid&gt;*, quindi individuare il codice di uscita.

    Una corretta installazione dispone di un codice di uscita pari a 0 e qualsiasi altro numero indica un'installazione non riuscita.

    Esempio del nome del file di log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### Per verificare l'esito positivo di installazione per l'applicazione di condivisione RMS per Office 2010 e Azure RMS

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

### Per verificare l'esito positivo di installazione per l'applicazione di condivisione RMS per Office 2010 e Active Directory RMS

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

### Per verificare l'esito positivo di installazione solo per l'applicazione di condivisione RMS e il componente aggiuntivo Office

1.  Per verificare l'esito positivo del comando Setup_ipviewer.exe, cercare il testo seguente nel file di log di installazione: **Installazione riuscita o stato di errore: 0**

    Righe di esempio da un'installazione corretta:

    **MSI (s) (F0:B8) [14:19:57:854]: Prodotto: Active Directory Rights Management Services Client 2.1 - Installazione completata.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer: installazione del prodotto completata. Nome prodotto: Active Directory Rights Management Services Client 2.1. Versione del prodotto: 1.0.1179.1. Lingua del prodotto: 1033. Produttore: Microsoft Corporation Stato di esito positivo o di errore nell’installazione: 0.**

2.  Per verificare l'esito positivo del componente aggiuntivo Office, su ogni computer, cercare il testo seguente nel file di log di installazione: **Installazione riuscita o stato di errore: 0**

    Righe di esempio da un'installazione corretta:

    **MSI (s) (9C:88) [18:49:04:007]: Prodotto: Componenti aggiuntivi di Office per Microsoft RMS - Installazione completata.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer: installazione del prodotto completata. Nome prodotto: Componenti aggiuntivi di Office per Microsoft RMS. Versione del prodotto: 1.0.7. Lingua del prodotto: 1033. Produttore: Microsoft Stato di esito positivo o di errore nell’installazione: 0.**

## Disinstallare i comandi
Non tutti i comandi di installazione necessari per tali distribuzioni supportano un comando di disinstallazione. È possibile disinstallare il client AD RMS, l'applicazione di condivisione e il componente aggiuntivo di Office. Utilizzare i comandi seguenti per disinstallare questi elementi.

### Per disinstallare il Client AD RMS e l’applicazione di condivisione RMS

-   Usare i seguenti comandi:

    -   Per Windows a 64 bit:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Per Windows a 32 bit:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### Per disinstallare il componente aggiuntivo di Office

-   Usare i seguenti comandi:

    -   Per la versione di Office a 64 bit:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Per la versione a 32 bit di Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## Eliminazione degli aggiornamenti automatici
Per impostazione predefinita, gli utenti vengono informati se esiste una versione successiva di applicazione di condivisione RMS e viene loro chiesto di scaricarla. È possibile eliminare questa notifica apportando la seguente modificare al Registro di sistema:

1.  Passare a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e, se non è già presente, creare una nuova chiave denominata **RmsSharingApp**.

2.  Selezionare **RmsSharingApp**, creare un nuovo valore DWORD di **AllowUpdatePrompt**, e impostare il valore su **0**.

Poiché l'applicazione di condivisione RMS non è supportata da WSUS, è possibile utilizzare la tecnica seguente per verificare le eventuali nuove versioni dell'applicazione di condivisione RMS prima di distribuirla a tutti gli utenti:

1.  Nei computer di tutti gli utenti, eseguire uno script per eliminare gli aggiornamenti automatici. Nei computer utilizzati dagli amministratori per verificare le nuove versioni, non eseguire questo script.

2.  Quando una nuova versione è disponibile, gli amministratori la scaricano e la testano.

3.  Quando il test è completo e i problemi sono risolti, distribuire la versione più recente a tutti gli utenti utilizzando le istruzioni di distribuzione automatica in questa Guida.

## Solo Azure RMS: Configurazione del rilevamento dei documenti
Se si dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://technet.microsoft.com/dn858608), il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione.  Il rilevamento dei documenti mostra informazioni quali indirizzi di posta elettronica delle persone che hanno tentato di accedere ai documenti protetti condivisi dagli utenti, nel momento in cui queste persone hanno tentato di accedere, e la loro posizione. Se la visualizzazione di queste informazioni non è consentita all'interno dell'organizzazione a causa dei requisiti sulla privacy, è possibile disabilitare l'accesso al sito di rilevamento dei documenti tramite il cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). È possibile riabilitare l'accesso al sito in qualsiasi momento utilizzando [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), ed è possibile verificare se l'accesso è attualmente abilitato o disabilitato utilizzando [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Per eseguire questi cmdlet, è necessario disporre almeno della versione **2.3.0.0** del modulo Azure RMS per Windows PowerShell.  Per le istruzioni di installazione, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Se il modulo è stato scaricato e installato in precedenza, verificarne il numero di versione eseguendo il comando seguente: `(Get-Module aadrm –ListAvailable).Version`

Gli URL seguenti vengono utilizzati per il rilevamento dei documenti e devono essere consentiti (ad esempio, aggiungerli ai siti attendibili se si utilizza Internet Explorer con protezione avanzata):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > questo URL è per Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## Solo AD RMS: Supporto per più domini di posta elettronica all'interno dell'organizzazione
Se si utilizza AD RMS e gli utenti dell'organizzazione hanno più domini di posta elettronica, forse a causa di una fusione o di un’acquisizione, è necessario apportare la seguente modifica al Registro di sistema:

1.  Passare a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e, se non è già presente, creare una nuova chiave denominata **RmsSharingApp**.

2.  Selezionare **RmsSharingApp**, creare un nuovo valore multistringa denominato **FederatedDomains** e poi aggiungere i domini e i sotto-domini utilizzati dall'organizzazione. I caratteri jolly non sono supportati.

    Ad esempio: la società Coho Vineyard &amp; Winery ha il dominio di posta elettronica standard **cohovineyardandwinery.com**, ma in seguito alle fusioni vengono usati anche i domini di posta elettronica **cohowinery.com**, **eastcoast.cohowinery.com** e **cohovineyard**. Per i dati di valore **FederatedDomains**, l'amministratore immette: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Se non si apporta questa modifica al Registro di sistema, gli utenti potrebbero non essere in grado di utilizzare contenuti protetti da altri utenti nella propria organizzazione. Questa modifica del Registro di sistema non è necessaria se si usa Azure RMS.


## Passaggi successivi
Per informazioni tecniche aggiuntive, inclusa la spiegazione della differenza tra i livelli di protezione (nativi e generici), i tipi di file supportati, le estensioni del nome dei file e come modificare il livello di protezione predefinito, vedere [Panoramica tecnica dell'applicazione di condivisione Rights Management](sharing-app-admin-guide-technical.md).




<!--HONumber=Jul16_HO3-->


