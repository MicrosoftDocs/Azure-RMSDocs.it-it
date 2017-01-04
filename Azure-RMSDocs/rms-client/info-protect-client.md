---
title: Installazione del client di Azure Information Protection | Azure Information Protection
description: Istruzioni per installare il client che aggiunge una barra di protezione delle informazioni alle applicazioni di Office in modo che sia possibile selezionare le etichette di classificazione per i documenti e i messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 23c437479c756f2a9335606e686f117d514a38f6
ms.openlocfilehash: 71972b0a057b1958dfa5e5b4af41b65d5080a086


---

# <a name="installing-the-azure-information-protection-client"></a>Installazione del client di Azure Information Protection

>*Si applica a: Azure Information Protection*

Per classificare i documenti e i messaggi di posta elettronica con Azure Information Protection, occorre prima di tutto installare il client di Azure Information Protection. Questa installazione aggiunge una barra Information Protection alle applicazioni di Office (Word, Excel, PowerPoint, Outlook) che mostra le etichette di classificazione per l'organizzazione, oltre a un nuovo gruppo **Protection** (Protezione) nella scheda **Home** di Word, Excel e PowerPoint, che presenta un pulsante denominato **Protect** (Proteggi):

L'immagine seguente mostra la barra Information Protection e le etichette del [criterio predefinito](../deploy-use/configure-policy-default.md):

![Barra Azure Information Protection con criterio predefinito](../media/info-protect-bar-default.png)

Scaricare il client di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Attualmente, è possibile installare la versione di disponibilità generale (GA) e la versione di anteprima. La versione di anteprima include nuove funzionalità a scopo di valutazione ed è soggetta a modifiche. Per altre informazioni, vedere l'annuncio del post di blog seguente: [L'anteprima di dicembre di Azure Information Protection è ora disponibile](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/).

Prima di installare il client, verificare di avere le versioni del sistema operativo e le applicazioni per il client di Azure Information Protection richieste: [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). Inoltre, per la versione di anteprima del client, i computer che eseguono Windows 7 SP1 richiedono [KB 2533623](https://support.microsoft.com/en-us/kb/2533623), che può essere installato dopo l'installazione del client. Se questo aggiornamento necessario non è installato, verrà richiesto di installarlo.

## <a name="to-install-the-azure-information-protection-client-manually"></a>Per installare manualmente il client di Azure Information Protection

1. Dopo avere eseguito il [download del client](https://www.microsoft.com/en-us/download/details.aspx?id=53018), eseguire l'eseguibile, ad esempio **AzInfoProtection.exe**, e seguire le istruzioni per l'installazione del client. Questa installazione richiede autorizzazioni amministrative locali.

    Selezionare l'opzione per l'installazione di un criterio demo se non si riesce a connettersi a Office 365 o Azure Active Directory, ma si vuole vedere e provare Azure Information Protection sul lato client usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione. 

2. Per iniziare a usare il client di Azure Information Protection: se il computer esegue Office 2010, riavviare il computer. Per altre versioni di Office, riavviare le applicazioni di Office.

## <a name="to-install-the-azure-information-protection-client-for-users"></a>Per installare il client di Azure Information Protection per gli utenti

È possibile creare script e automatizzare l'installazione del client di Azure Information Protection usando le opzioni della riga di comando. Per visualizzare le opzioni di installazione, eseguire l'eseguibile con **/help**. Ad esempio: `AzInfoProtection.exe /help`.

Esempio per installare automaticamente il client: `AzInfoProtection.exe /passive | quiet`

La versione di disponibilità generale del client di Azure Information Protection è anche inclusa in Microsoft Update Catalog, per cui è possibile installare e aggiornare il client tramite qualsiasi servizio di aggiornamento software che usa il catalogo. Le versioni di anteprima del client non sono incluse in Microsoft Update Catalog.

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



<!--HONumber=Dec16_HO1-->


