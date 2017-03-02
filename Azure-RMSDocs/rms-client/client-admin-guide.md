---
title: Guida dell&quot;amministratore del client Azure Information Protection
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: b6a8477078a333aa23ccfe5904af3582216a1e96
ms.lasthandoff: 02/24/2017


---


# <a name="azure-information-protection-client-administrator-guide"></a>Guida dell'amministratore del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*


Usare le informazioni seguenti se si è responsabili del client Azure Information Protection in una rete aziendale o se sono necessarie maggiori informazioni rispetto a quelle disponibili nella [Guida per l'utente del client Azure Information Protection](client-user-guide.md).

Il client Azure Information Protection include gli elementi seguenti:

- Un componente aggiuntivo per Office, che installa la barra di Azure Information Protection per la selezione di etichette di classificazione, e un pulsante **Proteggi** sulla barra multifunzione per offrire altre opzioni.

- Esplora file, opzioni tramite clic con il pulsante destro del mouse per l'applicazione di etichette di classificazione e della protezione ai file.

- Un visualizzatore per visualizzare file protetti quando un'applicazione nativa non è in grado di aprirli.

- Un modulo di PowerShell per applicare e rimuovere etichette di classificazione e la protezione dei file.

- Il client Rights Management che comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

Il client Azure Information Protection si integra al meglio con i servizi di Azure, Azure Information Protection e il relativo servizio di protezione dei dati, Azure Rights Management. Tuttavia, con alcune limitazioni, il client Azure Information Protection si integra anche con la versione locale di Rights Management, AD RMS. Per un confronto completo delle funzionalità supportate da Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

**In caso di altre domande a cui questa documentazione non risponde**, visitare il [sito di Yammer su Azure Information Protection](https://www.yammer.com/AskIPTeam). 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>È consigliabile distribuire il client Azure Information Protection?

Distribuire il client Azure Information Protection in uno o più dei casi seguenti:

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica selezionando etichette dalle applicazioni di Office (Word, Excel, PowerPoint, Outlook).

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica tramite Esplora file, che supporta altri tipi di file, la selezione multipla e le cartelle.

- Si vuole eseguire script che classifichino (e, facoltativamente, proteggano) documenti tramite comandi di PowerShell.

- Si vuole visualizzare documenti protetti quando non è installata un'applicazione nativa per visualizzare i file o questa applicazione non è in grado di aprire i documenti.

- Si vuole semplicemente proteggere file tramite Esplora file o i comandi di Powershell.

- Si vuole che utenti e amministratori siano in grado di monitorare e revocare documenti protetti.

- Si vuole rimuovere la crittografia da file e contenitori (rimozione della protezione) in blocco per scopi di ripristino dei dati.

- Si usa Office 2010 e si vuole proteggere documenti e messaggi di posta elettronica tramite il servizio Azure Rights Management.

Esempio che mostra il componente aggiuntivo del client Azure Information Protection in un'applicazione di Office, che visualizza le etichette di classificazione per l'organizzazione, e il nuovo pulsante **Proteggi** sulla barra multifunzione:

![Barra Azure Information Protection con criterio predefinito](../media/info-protect-bar-default.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Come installare il client Azure Information Protection per gli utenti

Prima di installare il client, verificare di avere le versioni del sistema operativo e le applicazioni per il client di Azure Information Protection richieste: [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). 

Inoltre:

- L'installazione completa del client Azure Information Protection richiede almeno Microsoft .NET Framework versione 4.6.2. Se questo non è presente, il programma di installazione prova a scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.

- Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. Se questo non è presente, il programma di installazione non lo scarica e installa.

- Il modulo PowerShell richiede Windows PowerShell versione 4.0, che potrebbe essere necessario installare in sistemi operativi precedenti. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). Per verificare quale versione di Windows PowerShell è in esecuzione, digitare **$PSVersionTable** in una sessione di PowerShell.

- I computer con Windows 7 Service Pack 1 richiedono l'aggiornamento [KB 2533623](https://support.microsoft.com/en-us/kb/2533623), che può essere installato dopo l'installazione del client. Se questo aggiornamento obbligatorio non viene installato, viene richiesto di installarlo.

> [!NOTE]
> Per l'installazione sono necessarie autorizzazioni di amministratore locale.

Oltre all'uso delle istruzioni seguenti, il client Azure Information Protection è anche incluso in Microsoft Update Catalog, in modo da poter installare e aggiornare il client usando qualsiasi servizio di aggiornamento software che usa il catalogo. 

1. Scaricare il client di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

2. Per un'installazione predefinita, eseguire semplicemente il file eseguibile **AzInfoProtection.exe**. Al contrario, per visualizzare le opzioni di installazione, eseguire prima di tutto l'eseguibile con **/help**: `AzInfoProtection.exe /help`

   Esempio per installare automaticamente il client: `AzInfoProtection.exe /quiet`
   
   Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
   
   Inoltre, se il client viene installato in computer con Office 2010, è necessario specificare il parametro **ServiceLocation** (non incluso nella schermata del cmdlet help) se gli utenti non sono amministratori locali nei propri computer. Per altre informazioni, vedere la sezione seguente.

3. Se si sceglie l'installazione interattiva, selezionare l'opzione per l'installazione di un **criterio demo** se non si riesce a connettersi a Office 365 o ad Azure Active Directory, ma si vuole esaminare e provare il lato client di Azure Information Protection usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.
    
4. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        Se il client non è stato installato con il parametro ServiceLocation, quando si apre per la prima volta una delle applicazioni di Office che usano la barra di Azure Information Protection, ad esempio Word, è necessario confermare tutti i messaggi relativi all'aggiornamento del Registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery). 
    
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. 
        
5. È possibile verificare che l'installazione sia stata completata controllando il file di log di installazione nella cartella %temp%. Questo file ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`. Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    In questo file di log, cercare la stringa seguente: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** (Prodotto: Microsoft Azure Information Protection -- Installazione completata.)

### <a name="additional-instructions-for-office-2010-only"></a>Istruzioni aggiuntive solo per Office 2010

Quando si installa il client per gli utenti che usano Office 2010 e che non hanno autorizzazioni di amministratore locale, specificare il parametro ServiceLocation e l'URL per il servizio Azure Rights Management. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Usare la procedura seguente per identificare il valore da specificare per il parametro ServiceLocation. 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Per identificare il valore da specificare per il parametro ServiceLocation

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) e specificare le credenziali di amministratore per connettersi al servizio Azure Rights Management. Eseguire quindi [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Se non è stato ancora installato il modulo di PowerShell per il servizio Azure Rights Management, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .

    Ad esempio, **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Ad esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Esempio per installare il client in modo invisibile all'utente per Office 2010 e Azure RMS: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


## <a name="to-uninstall-the-azure-information-protection-client"></a>Per disinstallare il client di Azure Information Protection

È possibile usare una delle seguenti opzioni:

- Per disinstallare un programma, usare il Pannello di controllo: fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

- Rieseguire l'eseguibile, ad esempio **AzInfoProtection.exe**, e fare clic su **Disinstalla** nella pagina **Modifica installazione**. 

- Eseguire l'eseguibile con **/uninstall**. Ad esempio: `AzInfoProtection.exe /uninstall`


## <a name="to-verify-installation-connection-status-or-send-feedback"></a>Per verificare l'installazione o lo stato di connessione o inviare commenti e suggerimenti

1. Aprire un'applicazione di Office, quindi nel gruppo **Protection** (Protezione) della scheda **Home** fare clic su **Protect** (Proteggi) e quindi fare clic su **Help and feedback** (Guida e commenti e suggerimenti).

2. Nella finestra di dialogo **Microsoft Azure Information Protection** notare quanto segue:

    - Nella sezione **Client status** (Stato del client): usare il valore di **Version** (Versione) per verificare che l'installazione sia stata eseguita correttamente. È anche possibile sapere quando il client si è connesso per l'ultima volta al servizio Azure Information Protection dell'organizzazione e la data di installazione o aggiornamento più recente di Azure Information Protection. Quando il client si connette al servizio, scarica automaticamente il criterio più recente se rileva variazioni rispetto al criterio corrente. Se si sono apportate modifiche ai criteri dopo l'ora visualizzata, chiudere e riaprire l'applicazione di Office.
    
        Viene anche mostrato il nome utente visualizzato che identifica l'account usato per autenticare l'utente in Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory e che appartiene a un tenant configurato per Azure Information Protection.

    - Nella sezione **Guida e commenti e suggerimenti**: il collegamento **Ulteriori informazioni** reindirizza per impostazione predefinita al sito Web di [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection) ma può essere configurato con un URL personalizzato nell'ambito delle [impostazioni dei criteri](../deploy-use/configure-policy-settings.md) di Azure Information Protection.
        
        Usare il collegamento **Invia commenti e suggerimenti** per inviare suggerimenti o richieste al team di Information Protection. Non usare questa opzione se si vuole ottenere supporto tecnico. In questo caso, vedere invece [Opzioni di supporto e risorse per la community](../get-started/information-support.md#support-options-and-community-resources). 
    
        Per informazioni di diagnostica e per reimpostare il client, fare clic su **Run diagnostics** (Esegui diagnostica). Al termine dei test diagnostici, fare clic su **Copy results** (Copia risultati) per incollare le informazioni in un messaggio di posta elettronica da inviare al proprio help desk o al supporto tecnico Microsoft. Al termine dei test, è anche possibile reimpostare il client.
        
        Altre informazioni sull'opzione **Reset** (Reimposta):
        
        - Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 
        
        - A meno che i file non siano bloccati, con questa azione vengono eliminati tutti i file presenti in **%localappdata%\Microsoft\MSIPC**, dove sono archiviati i certificati del client e i modelli per Rights Management. Non vengono eliminati i criteri di Azure Information Protection e i file di log del client, né l'utente viene disconnesso.
        
        - Viene eliminata le chiave del Registro di sistema seguente con le relative impostazioni: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Se si configurano le impostazioni per questa chiave del Registro di sistema (ad esempio le impostazioni per il reindirizzamento al tenant di Azure Information Protection poiché si sta eseguendo la migrazione da AD RMS e nella rete è ancora presente un punto di connessione del servizio), è necessario riconfigurare le impostazioni del Registro di sistema dopo la reimpostazione del client.
        
        - Dopo aver reimpostato il client, è necessario inizializzare nuovamente l'ambiente utente, azione nota anche come "bootstrap", durante la quale verranno scaricati i certificati per il client e i modelli più recenti. A tale scopo, chiudere tutte le istanze di Office e quindi riavviare un'applicazione di Office. Questa azione verifica anche che siano stati scaricati i criteri di Azure Information Protection più recenti. Non eseguire di nuovo i test diagnostici prima che ciò sia stato fatto.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

