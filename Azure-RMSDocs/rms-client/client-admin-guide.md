---
title: Guida dell'amministratore del client Azure Information Protection
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/20/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 036fae62087bf71e0f3bf5ef2859acac701c5e62
ms.sourcegitcommit: 724b0b5d7a3ab694643988148ca68c0eac769f1e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2017
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guida dell'amministratore del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Usare le informazioni di questa guida se si è responsabili del client Azure Information Protection in una rete aziendale o se sono necessarie maggiori informazioni rispetto a quelle disponibili nella [Guida per l'utente del client Azure Information Protection](client-user-guide.md). 

Ad esempio:

- Comprendere i diversi componenti di questo client e se è necessario installarlo

- Come installare il client per gli utenti, con informazioni su prerequisiti, opzioni e parametri di installazione e controlli di verifica

- Come gestire le configurazioni personalizzate che richiedono spesso la modifica del Registro di sistema

- Individuare i file e i log di utilizzo del client

- Identificare i tipi di file supportati dal client

- Configurare e usare il sito di rilevamento dei documenti per gli utenti

- Usare il client con PowerShell per il controllo dalla riga di comando

**In caso di domande su argomenti non trattati in questa documentazione**, visitare il [sito di Yammer su Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Panoramica tecnica sul client Azure Information Protection

Il client Azure Information Protection include gli elementi seguenti:

- Un componente aggiuntivo per Office, che installa la barra di Azure Information Protection per la selezione di etichette di classificazione, e un pulsante **Proteggi** sulla barra multifunzione per offrire altre opzioni.

- Esplora file, opzioni tramite clic con il pulsante destro del mouse per l'applicazione di etichette di classificazione e della protezione ai file.

- Un visualizzatore per visualizzare file protetti quando un'applicazione nativa non è in grado di aprirli.

- Un modulo di PowerShell per applicare e rimuovere etichette di classificazione e la protezione dei file.

- Il client Rights Management che comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

Il client Azure Information Protection si integra al meglio con i servizi di Azure, Azure Information Protection e il relativo servizio di protezione dei dati, Azure Rights Management. Tuttavia, con alcune limitazioni, il client Azure Information Protection si integra anche con la versione locale di Rights Management, AD RMS. Per un confronto completo delle funzionalità supportate da Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). 

Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-client"></a>È consigliabile distribuire il client Azure Information Protection?

Distribuire il client Azure Information Protection in uno o più dei casi seguenti:

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica selezionando etichette dalle applicazioni di Office (Word, Excel, PowerPoint, Outlook).

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica tramite Esplora file, che supporta altri tipi di file, la selezione multipla e le cartelle.

- Si vuole eseguire script che classifichino (e, facoltativamente, proteggano) documenti tramite comandi di PowerShell.

- Si vuole visualizzare documenti protetti quando non è installata un'applicazione nativa per visualizzare i file o questa applicazione non è in grado di aprire i documenti.

- Si vuole semplicemente proteggere i file usando Esplora file o i comandi di PowerShell.

- Si vuole che utenti e amministratori siano in grado di monitorare e revocare documenti protetti.

- Si vuole rimuovere la crittografia da file e contenitori (rimozione della protezione) in blocco per scopi di ripristino dei dati.

- Si usa Office 2010 e si vuole proteggere documenti e messaggi di posta elettronica tramite il servizio Azure Rights Management.

Esempio che visualizza il componente aggiuntivo client Azure Information Protection in un'applicazione di Office, con le etichette di classificazione per l'organizzazione e il nuovo pulsante **Proteggi** sulla barra multifunzione:

![Barra Azure Information Protection con criterio predefinito](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Come installare il client Azure Information Protection per gli utenti

Prima di installare il client, verificare che sui computer siano presenti le versioni del sistema operativo e le applicazioni richieste per il client Azure Information Protection: [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). 

Verificare quindi gli altri prerequisiti che possono essere necessari per il client Azure Information Protection.

### <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Altri prerequisiti per il client Azure Information Protection

- Microsoft .NET Framework 4.6.2
    
    Per impostazione predefinita, l'installazione completa del client Azure Information Protection richiede almeno Microsoft .NET Framework 4.6.2. Se questo prerequisito non è soddisfatto, il programma di installazione prova a scaricare e installare la versione richiesta. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer. Anche se non è consigliabile, è possibile ignorare questo prerequisito con un [parametro di installazione personalizzata](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

- Microsoft .NET Framework 4.5.2
    
    Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. Se questo non è presente, il programma di installazione non lo scarica e installa.

- Windows PowerShell versione 4.0
    
    Il modulo PowerShell per il client richiede Windows PowerShell versione 4.0, che potrebbe essere necessario installare in sistemi operativi precedenti. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). Il programma di installazione non controlla né installa questo prerequisito per l'utente. Per verificare quale versione di Windows PowerShell è in esecuzione, digitare `$PSVersionTable` in una sessione di PowerShell.

- Assistente per l'accesso ai Microsoft Online Services 7.250.4303.0
    
    I computer che eseguono Office 2010 richiedono l'Assistente per l'accesso ai Microsoft Online Services versione 7.250.4303.0. Questa versione è inclusa nell'installazione del client. Se si usa una versione successiva dell'Assistente per l'accesso, disinstallarla prima di installare il client Azure Information Protection. Ad esempio, per verificare la versione e disinstallare l'Assistente per l'accesso, usare **Pannello di controllo** > **Programmi e funzionalità** > **Disinstalla o modifica programma**.

- KB 2533623
    
    I computer con Windows 7 Service Pack 1 richiedono l'aggiornamento KB 2533623. Per altre informazioni su questo aggiornamento, vedere [Avviso di sicurezza Microsoft: possibile esecuzione di codice remoto durante un caricamento della libreria non protetto](https://support.microsoft.com/en-us/kb/2533623). Questo aggiornamento può essere installato direttamente dall'utente. In alternativa, è possibile sostituirlo con un altro aggiornamento che lo installa automaticamente.
    
    Se questo aggiornamento richiesto non è installato, l'installazione client avvisa che è necessario installarlo. Questo aggiornamento può essere installato dopo l'installazione del client. Alcune azioni, tuttavia, verranno bloccate e verrà visualizzato di nuovo l'avviso.  

> [!IMPORTANT]
> L'installazione del client Azure Information Protection richiede autorizzazioni amministrative locali.

### <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Opzioni di installazione del client Azure Information Protection per gli utenti

Sono disponibili tre opzioni per l'installazione del client per gli utenti:

**Windows Update**: il client Azure Information Protection è incluso nel catalogo di Microsoft Update, quindi è possibile installare e aggiornare il client usando qualsiasi servizio di aggiornamento del software che usa il catalogo.

**Eseguire la versione eseguibile (EXE) del client**: il metodo di installazione consigliato che è possibile usare in modo interattivo o automatico. Questo metodo offre la massima flessibilità ed è consigliato perché il programma di installazione verifica la maggior parte dei prerequisiti ed è in grado di installare automaticamente i prerequisiti mancanti. [Istruzioni](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**Distribuire la versione del programma di installazione di Windows (MSI) del client**: metodo supportato solo per le installazioni invisibili all'utente che usano un meccanismo di distribuzione centrale, ad esempio criteri di gruppo, Configuration Manager e Microsoft Intune. Questo metodo è necessario per i PC Windows 10 gestiti da Intune e dalla gestione dispositivi mobili (MDM) poiché per questi computer, i file eseguibili non sono supportati per l'installazione. Tuttavia, quando si usa questo metodo di installazione, è necessario verificare e installare o disinstallare manualmente il software dipendente che il programma di installazione eseguirebbe in ogni computer per il file eseguibile. [Istruzioni](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Per installare il client Azure Information Protection usando il programma di installazione del file eseguibile

Usare le istruzioni riportate di seguito per installare il client quando non si usa il catalogo di Microsoft Update o si distribuisce il file con estensione MSI usando un metodo di distribuzione centrale, ad esempio Intune.

1. Scaricare la versione eseguibile del client Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per un'installazione predefinita, basta eseguire il file eseguibile, ad esempio **AzInfoProtection.exe**. Al contrario, per visualizzare le opzioni di installazione, eseguire prima di tutto l'eseguibile con **/help**: `AzInfoProtection.exe /help`

    Esempio per installare automaticamente il client: `AzInfoProtection.exe /quiet`
    
    Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Nella schermata della Guida non sono elencati i parametri seguenti:
    
    - **ServiceLocation**: usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. [Altre informazioni](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: usare questo parametro per ignorare il requisito relativo a Microsoft .NET Framework versione 4.6.2. [Altre informazioni](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry = 0**: usare questo parametro per disabilitare l'opzione di installazione **Invia le statistiche di utilizzo a Microsoft per contribuire a migliorare Azure Information Protection**. 
    
3. Se si sceglie l'installazione interattiva, selezionare l'opzione per l'installazione di un **criterio demo** se non si riesce a connettersi a Office 365 o ad Azure Active Directory, ma si vuole esaminare e provare il lato client di Azure Information Protection usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.
    
4. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        Se il client non è stato installato con il parametro ServiceLocation, quando si apre per la prima volta una delle applicazioni di Office che usano la barra di Azure Information Protection, ad esempio Word, è necessario confermare tutti i messaggi relativi all'aggiornamento del Registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery). 
    
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. 
        
5. È possibile verificare se l'installazione è stata completata controllando il file di log di installazione, che per impostazione predefinita viene creato nella cartella %temp%. È possibile modificare questo percorso con il parametro di installazione **/log**. 
 
    Questo file ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    In questo file di log, cercare la stringa seguente: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** (Prodotto: Microsoft Azure Information Protection -- Installazione completata.) Se l'installazione non è riuscita, questo file di log contiene informazioni dettagliate per identificare e risolvere i problemi.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Altre informazioni sul parametro di installazione ServiceLocation

Quando si installa il client per gli utenti che usano Office 2010 e che non hanno autorizzazioni di amministratore locale, specificare il parametro ServiceLocation e l'URL per il servizio Azure Rights Management. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Usare la procedura seguente per identificare il valore da specificare per il parametro ServiceLocation. 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Per identificare il valore da specificare per il parametro ServiceLocation

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) e specificare le credenziali di amministratore per connettersi al servizio Azure Rights Management. Eseguire quindi [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Se non è stato ancora installato il modulo di PowerShell per il servizio Azure Rights Management, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .

    Ad esempio, **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Ad esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Esempio per installare il client in modo invisibile all'utente per Office 2010 e Azure RMS: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Altre informazioni sul parametro di installazione DowngradeDotNetRequirement installation

Per il supporto degli aggiornamenti automatici tramite Windows Update e per l'integrazione affidabile con le applicazioni di Office, il client Azure Information Protection usa Microsoft .NET Framework versione 4.6.2. Per impostazione predefinita, il programma di installazione controlla se questa versione è presente e, in caso negativo, prova a installarla. A questo punto è necessario riavviare il computer.

Se l'installazione di questa versione più recente di Microsoft .NET Framework non è una soluzione efficace, è possibile installare il client con il parametro **DowngradeDotNetRequirement=True**, in modo da ignorare questo requisito se è installato Microsoft .NET Framework versione 4.5.1.

Ad esempio: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

È consigliabile usare questo parametro con cautela, tenendo presente che sono stati segnalati problemi di blocco delle applicazioni di Office quando il client Azure Information Protection viene usato con questa versione precedente di Microsoft .NET Framework. Se si riscontrano problemi di blocco delle applicazioni, eseguire l'aggiornamento alla versione consigliata prima di provare altre soluzioni. 

Tenere anche presente che se si usa Windows Update per mantenere aggiornato il client Azure Information Protection, è necessario adottare un altro meccanismo di distribuzione del software per aggiornare il client alle versioni successive.

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>Per installare il client Azure Information Protection usando il programma di installazione MSI

Per la distribuzione centrale, usare le seguenti informazioni specifiche della versione dell'installazione MSI del client Azure Information Protection. 

Se si usa Intune per il metodo di distribuzione del software, usare queste istruzioni insieme a quelle incluse in [Aggiungere app con Microsoft Intune](/intune/deploy-use/add-apps).

1. Scaricare la versione MSI del client Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per ogni computer che esegue il file con estensione msi è necessario verificare che siano soddisfatte le seguenti dipendenze software. Ad esempio, creare un pacchetto con le dipendenze e la versione MSI del client oppure distribuire solo ai computer che soddisfano queste dipendenze:
    
    |Versione di Office|Sistema operativo|Software|Azione|
    |--------------------|--------------|----------------|---------------------|
    |Office 2013|Tutte le versioni supportate|[KB 3054941](https://www.microsoft.com/en-us/download/details.aspx?id=49337)<br /><br /> Numero di versione nel nome file: v3|Installare|
    |Office 2010|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installare|
    |Office 2010|Windows 8.1 e Windows Server 2012 R2|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare se KB 2843630 o KB 2919355 non è installato|
    |Office 2010|Windows 8 e Windows Server 2012|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare|
    |Office 2010|Windows 7|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB 3125574|
    |Non applicabile|Windows 7|KB 2627273 <br /><br /> Numero di versione incluso nel nome file: v4|Uninstall|

3. Per un'installazione predefinita, eseguire il file MSI con **/quiet/**, ad esempio, `AzInfoProtection.msi /quiet`. Tuttavia, può essere necessario specificare parametri di installazione aggiuntivi, che sono documentati nelle [istruzioni del programma di installazione del file eseguibile](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).  

## <a name="additional-checks-and-troubleshooting"></a>Controlli aggiuntivi e risoluzione dei problemi

Usare l'opzione **Guida e commenti** per aprire la finestra di dialogo **Microsoft Azure Information Protection**:

- Da un'applicazione di Office: nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**.

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**. 

### <a name="help-and-feedback-section"></a>Sezione **Guida e commenti**

Il collegamento **Altre informazioni** reindirizza per impostazione predefinita al sito Web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), ma è possibile configurarlo con un URL personalizzato nelle [impostazioni dei criteri](../deploy-use/configure-policy-settings.md) di Azure Information Protection.

Usare il collegamento **Invia commenti e suggerimenti** per inviare suggerimenti o richieste al team di Information Protection. Non usare questa opzione se si vuole ottenere supporto tecnico. In questo caso, vedere invece [Opzioni di supporto e risorse per la community](../get-started/information-support.md#support-options-and-community-resources). 

L'opzione **Esporta log** consente di raccogliere e allegare automaticamente i file di log relativi al client Azure Information Protection se ne è stato chiesto l'invio al supporto tecnico Microsoft. Questa opzione può essere usata anche dagli utenti finali per inviare i file di log all'help desk.

Per visualizzare informazioni di diagnostica e reimpostare il client, selezionare **Esegui la diagnostica**. Al termine dei test di diagnostica, fare clic su **Copy results** (Copia risultati) per incollare le informazioni in un messaggio di posta elettronica che l'amministratore e gli utenti finali possono inviare rispettivamente al supporto tecnico Microsoft e all'help desk. Al termine dei test, è anche possibile reimpostare il client.

> [!NOTE]
> Nella versione di anteprima del client l'opzione **Esegui diagnostica** è stata rimossa e sostituta con **Ripristina impostazioni**. È inoltre [cambiato](#more-information-about-the-reset-option-for-the-current-preview-version-of-the-azure-information-protection-client) il comportamento per questa opzione.

#### <a name="more-information-about-the-reset-option-for-the-general-availability-ga-version-of-the-azure-information-protection-client"></a>Altre informazioni sull'opzione di reimpostazione per la versione disponibile a livello generale del client Azure Information Protection

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, con questa azione vengono eliminati tutti i file presenti in **%LocalAppData%\Microsoft\MSIPC**, dove sono archiviati i certificati del client e i modelli per Rights Management. Non vengono eliminati i criteri di Azure Information Protection e i file di log del client, né l'utente viene disconnesso.

- Viene eliminata le chiave del Registro di sistema seguente con le relative impostazioni: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Se sono state configurate impostazioni per questa chiave del Registro di sistema, dopo la reimpostazione del client è necessario riconfigurare le impostazioni del Registro di sistema. Un esempio è il caso in cui sono state configurate le impostazioni per il reindirizzamento al tenant di Azure Information Protection, poiché si sta eseguendo la migrazione da AD RMS e nella rete è ancora presente un punto di connessione del servizio.

- Dopo aver reimpostato il client è necessario reinizializzare l'ambiente utente. In questo modo verranno scaricati i certificati per il client e i modelli più recenti. A tale scopo, chiudere tutte le istanze di Office e quindi riavviare un'applicazione di Office. Questa azione verifica anche che siano stati scaricati i criteri di Azure Information Protection più recenti. Non eseguire di nuovo i test diagnostici prima che ciò sia stato fatto.

#### <a name="more-information-about-the-reset-option-for-the-current-preview-version-of-the-azure-information-protection-client"></a>Altre informazioni sull'opzione di reimpostazione per la versione di anteprima corrente del client Azure Information Protection

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, questa azione elimina tutti i file nelle posizioni seguenti. Questi file includono i certificati client, i modelli di Rights Management, i criteri di Azure Information Protection e le credenziali utente memorizzate nella cache. I file di log del client non vengono eliminati.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- Vengono eliminate le chiavi e le impostazioni del Registro di sistema seguenti. Se sono state configurate impostazioni per chiavi del Registro di sistema in questo elenco, dopo la reimpostazione del client è necessario riconfigurarle. Un esempio è il caso in cui sono state configurate le impostazioni per il reindirizzamento al tenant di Azure Information Protection, poiché si sta eseguendo la migrazione da AD RMS, e nella rete è ancora presente un punto di connessione del servizio:
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- L'utente connesso viene disconnesso.

### <a name="client-status-section"></a>Sezione **Stato del client**

Usare il valore di **Connessione effettuata come** per verificare se il nome utente visualizzato identifica l'account da usare per l'autenticazione di Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory. L'account deve anche appartenere a un tenant configurato per Azure Information Protection.

Se è necessario accedere con un nome utente diverso da quello visualizzato, vedere la personalizzazione in [Accedere come utente diverso](client-admin-guide-customizations.md#sign-in-as-a-different-user).

Il valore **Ultima connessione** indica quando il client si è connesso per l'ultima volta al servizio Azure Information Protection dell'organizzazione. È possibile usare queste informazioni con l'impostazione **Il criterio di Information Protection è stato installato il giorno** per verificare la data e ora dell'installazione o dell'ultimo aggiornamento dei criteri di Azure Information Protection. Quando si connette al servizio, il client scarica automaticamente i criteri più recenti se rileva variazioni rispetto a quelli correnti e anche ogni 24 ore. Se si sono apportate modifiche ai criteri dopo l'ora visualizzata, chiudere e riaprire l'applicazione di Office.

Se viene visualizzato il messaggio **Questo client non ha la licenza per Office Professional Plus**, il client Azure Information Protection ha rilevato che l'edizione installata di Office non supporta l'applicazione della protezione di Rights Management. Quando viene effettuato questo rilevamento, le etichette che applicano la protezione non vengono visualizzate sulla barra di Azure Information Protection.

Usare le informazioni di **Versione** per verificare la versione del client installata. È possibile controllare se la versione installata è quella più recente e verificare le nuove funzionalità e le correzioni di tale versione facendo clic sul collegamento **Novità** che consente di accedere alla [cronologia delle versioni](client-version-release-history.md) del client.


## <a name="to-uninstall-the-azure-information-protection-client"></a>Per disinstallare il client di Azure Information Protection

È possibile usare una delle seguenti opzioni:

- Per disinstallare un programma, usare il Pannello di controllo: fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

- Rieseguire l'eseguibile, ad esempio **AzInfoProtection.exe**, e fare clic su **Disinstalla** nella pagina **Modifica installazione**. 

- Eseguire l'eseguibile con **/uninstall**. Ad esempio: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
