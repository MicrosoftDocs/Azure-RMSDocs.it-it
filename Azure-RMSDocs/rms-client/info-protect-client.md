---
title: Installazione del client di Azure Information Protection | Azure Information Protection
description: Istruzioni per installare il client che aggiunge una barra di protezione delle informazioni alle applicazioni di Office in modo che sia possibile selezionare le etichette di classificazione per i documenti e i messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: bd3cbea29183c39abaa66aa5dcec8a14ad0b0757
ms.openlocfilehash: bccddf228b33bcd8d36ef6af55dea9015cad34d0


---

# <a name="installing-the-azure-information-protection-client"></a>Installazione del client di Azure Information Protection

>*Si applica a: Azure Information Protection*

Per classificare i documenti e i messaggi di posta elettronica con Azure Information Protection, occorre prima di tutto installare il client di Azure Information Protection. Questa installazione aggiunge una barra Information Protection alle applicazioni di Office (Word, Excel, PowerPoint, Outlook) che mostra le etichette di classificazione per l'organizzazione, oltre a un nuovo gruppo **Protection** (Protezione) nella scheda **Home** di Word, Excel e PowerPoint, che presenta un pulsante denominato **Protect** (Proteggi):

L'immagine seguente mostra la barra Information Protection e le etichette del [criterio predefinito](../deploy-use/configure-policy-default.md):

![Barra Azure Information Protection con criterio predefinito](../media/info-protect-bar-default.png)

Scaricare il client di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Attualmente, è possibile installare la versione di disponibilità generale (GA) e la versione di anteprima. La versione di anteprima include nuove funzionalità a scopo di valutazione ed è soggetta a modifiche. Per altre informazioni, vedere l'annuncio del post di blog seguente: [L'anteprima di dicembre di Azure Information Protection è ora disponibile](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/).

Prima di installare il client, verificare di avere le versioni del sistema operativo e le applicazioni per il client di Azure Information Protection richieste: [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). Inoltre, per la versione di anteprima del client, i computer che eseguono Windows 7 SP1 richiedono [KB 2533623](https://support.microsoft.com/en-us/kb/2533623), che può essere installato dopo l'installazione del client. Se questo aggiornamento necessario non è installato, verrà richiesto di installarlo.


## <a name="to-install-the-azure-information-protection-client-manually"></a>Per installare manualmente il client di Azure Information Protection

> [!NOTE]
> Questa installazione richiede autorizzazioni amministrative locali.

    
1. Dopo avere eseguito il [download del client](https://www.microsoft.com/en-us/download/details.aspx?id=53018), eseguire l'eseguibile, ad esempio **AzInfoProtection.exe**, e seguire le istruzioni per l'installazione del client.
    
    Selezionare l'opzione per l'installazione di un **criterio demo** se non si riesce a connettersi a Office 365 o Azure Active Directory, ma si vuole vedere e provare Azure Information Protection sul lato client usando un criterio locale a scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.
    
    Altre informazioni su ciò che viene installato:

    - La versione disponibile a livello generale installa la barra di Azure Information Protection per le applicazioni di Office. 
    
    - La versione di anteprima più recente del client installa la barra di Azure Information Protection per le applicazioni di Office, i comandi accessibili con il pulsante destro del mouse per Esplora file, un visualizzatore per i file protetti e i cmdlet di Windows PowerShell per classificare e proteggere i file in blocco. 
        
        Si noti che è possibile installare solo il modulo di PowerShell (RMSProtection) specificando il parametro **PowerShellOnly=true**. Ad esempio: `AzInfoProtection_PREVIEW_1.3.98.0.exe  PowerShellOnly=true`

2. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        **Se è stata installata la versione di anteprima del client**: oltre a riavviare il computer, aprire una delle applicazioni di Office che usano la barra di Azure Information Protection (ad esempio, Word) e confermare eventuali messaggi relativi all'aggiornamento del Registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery). 
    
    - Per altre versioni di Office, riavviare le applicazioni di Office. 
        
        **Se è stata installata la versione di anteprima del client**: oltre a riavviare le eventuali applicazioni di Office, chiudere e riavviare anche Esplora file.

## <a name="to-install-the-azure-information-protection-client-for-users"></a>Per installare il client di Azure Information Protection per gli utenti

È possibile creare script e automatizzare l'installazione del client di Azure Information Protection usando le opzioni della riga di comando. Per visualizzare le opzioni di installazione, eseguire l'eseguibile con **/help**. Ad esempio: `AzInfoProtection.exe /help`

Esempio per l'installazione invisibile all'utente della versione disponibile a livello generale del client:`AzInfoProtection.exe /quiet`

Esempio per l'installazione invisibile all'utente solo del modulo di PowerShell, con il client di anteprima:`AzInfoProtection_PREVIEW_1.3.98.0.exe  PowerShellOnly=true /quiet`

Durante l'installazione della versione di anteprima del client nei computer che eseguono Office 2010, specificare il parametro **ServiceLocation** se gli utenti non sono amministratori locali nei propri computer. Per altre informazioni, vedere la sezione seguente.

La versione di disponibilità generale del client di Azure Information Protection è anche inclusa in Microsoft Update Catalog, per cui è possibile installare e aggiornare il client tramite qualsiasi servizio di aggiornamento software che usa il catalogo. Le versioni di anteprima del client non sono incluse in Microsoft Update Catalog.

### <a name="preview-version-and-office-2010-only"></a>Versione di anteprima e solo Office 2010

Per la versione di anteprima del client e Office 2010, quando si installa il client per gli utenti, specificare il parametro ServiceLocation e l'URL per il servizio Azure Rights Management. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

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


## <a name="to-verify-installation-connection-status-or-report-a-problem"></a>Per verificare l'installazione, lo stato della connessione o segnalare un problema

1. Aprire un'applicazione di Office, quindi nel gruppo **Protection** (Protezione) della scheda **Home** fare clic su **Protect** (Proteggi) e quindi fare clic su **Help and feedback** (Guida e commenti e suggerimenti).

2. Nella finestra di dialogo **Microsoft Azure Information Protection** notare quanto segue:

    - Nella sezione **Client status** (Stato del client): usare il valore di **Version** (Versione) per verificare che l'installazione sia stata eseguita correttamente. È anche possibile sapere quando il client si è connesso per l'ultima volta al servizio Azure Information Protection dell'organizzazione e la data di installazione o aggiornamento più recente di Azure Information Protection. Quando il client si connette al servizio, scarica automaticamente il criterio più recente se rileva variazioni rispetto al criterio corrente. Se si sono apportate modifiche ai criteri dopo l'ora visualizzata, chiudere e riaprire l'applicazione di Office.
    
        Viene anche mostrato il nome utente visualizzato che identifica l'account usato per autenticare l'utente in Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory e che appartiene a un tenant configurato per Azure Information Protection.

    - Nella sezione **Guida e commenti e suggerimenti**: il collegamento **Ulteriori informazioni** reindirizza per impostazione predefinita al sito Web di [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection) ma può essere configurato con un URL personalizzato nell'ambito delle [impostazioni dei criteri](../deploy-use/configure-policy-settings.md) di Azure Information Protection.
        
        Usare il collegamento **Invia commenti e suggerimenti** per allegare automaticamente i log del client a un messaggio di posta elettronica da inviare al team di Information Protection per l'analisi di un problema. 
    
        Per informazioni di diagnostica e per reimpostare il client, fare clic su **Run diagnostics** (Esegui diagnostica). Al termine dei test diagnostici, fare clic su **Copy results** (Copia risultati) per incollare le informazioni in un messaggio di posta elettronica da inviare al proprio help desk o al supporto tecnico Microsoft. Al termine dei test, è anche possibile reimpostare il client.
        
        Altre informazioni sull'opzione **Reset** (Reimposta):
        
        - Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 
        
        - A meno che i file non siano bloccati, con questa azione vengono eliminati tutti i file presenti in **%localappdata%\Microsoft\MSIPC**, dove sono archiviati i certificati del client e i modelli per Rights Management. Non vengono eliminati i criteri di Azure Information Protection e i file di log del client, né l'utente viene disconnesso.
        
        - Viene eliminata le chiave del Registro di sistema seguente con le relative impostazioni: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Se si configurano le impostazioni per questa chiave del Registro di sistema (ad esempio le impostazioni per il reindirizzamento al tenant di Azure Information Protection poiché si sta eseguendo la migrazione da AD RMS e nella rete è ancora presente un punto di connessione del servizio), è necessario riconfigurare le impostazioni del Registro di sistema dopo la reimpostazione del client.
        
        - Dopo aver reimpostato il client, è necessario inizializzare nuovamente l'ambiente utente, azione nota anche come "bootstrap", durante la quale verranno scaricati i certificati per il client e i modelli più recenti. A tale scopo, chiudere tutte le istanze di Office e quindi riavviare un'applicazione di Office. Questa azione verifica anche che siano stati scaricati i criteri di Azure Information Protection più recenti. Non eseguire di nuovo i test diagnostici prima che ciò sia stato fatto.


## <a name="usage-logging"></a>Registrazione dell'utilizzo

**[Questa funzionalità richiede la versione di anteprima del client ed è soggetta a modifiche].**

Per la versione di anteprima del client di Azure Information Protection, il client registra l'attività utente nel registro eventi locale di Windows **Applicazioni e servizi**, **Azure Information Protection**. Gli eventi includono le informazioni seguenti:

- Data, versione del client, ID criterio

- Nome utente connesso, nome computer

- Nome file e percorso

- Action:

    - Impostare l'etichetta: ID informazioni 101
    
    - Impostare l'etichetta (inferiore): ID informazioni 102
    
    - Impostare l'etichetta (superiore): ID informazioni 103
    
    - Rimuovere l'etichetta: ID informazioni 104
   
    - Suggerimento consigliato: ID informazioni 105
    
    - Applicare la protezione personalizzata: ID informazioni 201
    
    - Rimuovere la protezione personalizzata: ID informazioni 202
    
    - Accesso (operativo): ID informazioni 902
    
    - Download dei criteri (operativo): ID informazioni 901
    
- Origine azione:
    
    - Manuale 
    
    - Consigliato
    
    - Automatico  
    
    - Sistema (per l'accesso e il download dei criteri)
    
- Etichetta prima e dopo l'azione 
    
- Protezione prima e dopo l'azione
    
- Giustificazione utente (se applicabile)
    

## <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Tasti di scelta rapida per la barra di Azure Information Protection

Per accedere alla barra di Azure Information Protection tramite i tasti di scelta rapida, usare la combinazione di tasti seguente:

- Premere **CTRL** + **MAIUSC** + **~** 

Quindi usare TAB per selezionare le etichette e altri controlli della barra (le icone **Nascondi etichette** e **Rimuovi etichetta**) e INVIO per selezionarle.


## <a name="file-locations"></a>Percorsi di file

File del client:   

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client e file di criteri attualmente installati:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>Passaggi successivi

Per modificare le etichette sulla barra Information Protection, è necessario configurare i criteri di Azure Information Protection. Per altre informazioni, veder e[Configurazione dei criteri di Azure Information Protection](../deploy-use/configure-policy.md).

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Per verificare le informazioni sulla versione del client, vedere [Cronologia delle versioni](client-version-release-history.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


