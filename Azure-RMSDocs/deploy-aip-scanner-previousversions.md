---
title: Deploy the Azure Information Protection scanner - previous versions
description: Deployment instructions for versions of the Azure Information Protection scanner older than the current general availability version.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e5f0efad328a4c3cd479895e2324538e45a9b922
ms.sourcegitcommit: d9442efe61b55bb158bd50ee69873c028234842d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297596"
---
# <a name="deploying-previous-versions-of-the-azure-information-protection-scanner"></a>Deploying previous versions of the Azure Information Protection scanner

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2*
>
> *Instructions for: [Azure Information Protection client for Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> This article is for versions of the Azure Information Protection scanner that are earlier than version **1.48.204.0** but still in support. To upgrade earlier versions to the current version, see [Upgrading the Azure Information Protection scanner](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).
> 
> If you are looking for deployment instructions for the current version of the scanner, which includes configuration from the Azure portal, see [Deploying the Azure Information Protection scanner to automatically classify and protect files](deploy-aip-scanner.md).

Di seguito vengono illustrate le caratteristiche dello scanner di Azure Information Protection e le relative procedure per installarlo, configurarlo ed eseguirlo.

Questo scanner viene eseguito come servizio in Windows Server e consente di individuare, classificare e proteggere i file negli archivi dati seguenti:

- Cartelle locali nel computer Windows Server che esegue lo scanner.

- Percorsi UNC delle condivisioni di rete che usano il protocollo SMB (Server Message Block).

- Document libraries and folders for SharePoint Server 2019 through SharePoint Server 2013. SharePoint 2010 è supportato anche per i clienti che dispongono del [supporto "Extended" per la versione corrente di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Per analizzare ed etichettare i file nei repository cloud, usare [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) invece dello scanner.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Panoramica dello scanner di Azure Information Protection

Dopo aver configurato i [criteri di Azure Information Protection](configure-policy.md) per le etichette che applicano la classificazione automatica, è possibile etichettare i file rilevati dallo scanner. Le etichette applicano la classificazione e, facoltativamente, applicano o rimuovono la protezione:

![Panoramica dell'architettura dello scanner di Azure Information Protection](./media/infoprotect-scanner.png)

Lo scanner può controllare tutti i file indicizzabili da Windows, tramite IFilter installati nel computer. In seguito, per stabilire se i file devono essere etichettati, lo scanner usa il rilevamento di modelli e di tipi di dati sensibili della prevenzione della perdita di dati (DLP) predefiniti in Office 365 o i modelli regex di Office 365. Poiché usa il client di Azure Information Protection, lo scanner è in grado di classificare e proteggere gli stessi [tipi di file](./rms-client/client-admin-guide-file-types.md).

È possibile eseguire lo scanner solo in modalità di individuazione, in cui si usano i report per verificare che cosa accadrebbe se i file fossero etichettati. Oppure è possibile eseguire lo scanner per applicare automaticamente le etichette. È anche possibile eseguire lo scanner per individuare i file che contengono tipi di informazioni riservate, senza configurare le etichette per le condizioni per l'applicazione della classificazione automatica.

Si noti che lo scanner non individua e non applica etichette in tempo reale. Effettua sistematicamente una ricerca per indicizzazione nei file presenti negli archivi dati specificati ed è possibile configurare questo ciclo in modo da eseguirlo una o più volte.

È possibile specificare i tipi di file da includere o escludere dall'analisi. Per limitare i file esaminati dallo scanner, definire un elenco di tipi di file tramite **Set-AIPScannerScannedFileTypes**.


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prerequisiti per lo scanner di Azure Information Protection
Prima di installare lo scanner di Azure Information Protection, verificare che i requisiti seguenti siano soddisfatti.

|Requisito|Ulteriori informazioni|
|---------------|--------------------|
|Computer Windows Server per eseguire il servizio scanner:<br /><br />- 4 processori core<br /><br />- 8 GB di RAM<br /><br />- 10 GB di spazio libero (media) per i file temporanei|Windows Server 2019, Windows Server 2016, or Windows Server 2012 R2. <br /><br />**Note**: For testing or evaluation purposes in a non-production environment, you can use a Windows client operating system that is [supported by the Azure Information Protection client](requirements.md#client-devices).<br /><br />Il computer può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare.<br /><br /> Lo scanner richiede spazio su disco sufficiente a creare i file temporanei per ogni file analizzato, quattro file per core. Lo spazio su disco consigliato di 10 GB consente a 4 processori core di analizzare 16 file, ognuno con una dimensione di 625 MB. <br /><br />If internet connectivity is not possible because of your organization policies, see the [Deploying the scanner with alternative configurations](#deploying-the-scanner-with-alternative-configurations) section. Otherwise, make sure that this computer has internet connectivity that allows the following URLs over HTTPS (port 443):<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|Account del servizio per eseguire il servizio scanner |Oltre a eseguire il servizio scanner nel computer Windows Server, questo account di Windows esegue l'autenticazione in Azure AD e scarica i criteri di Azure Information Protection. Questo account deve essere un account Active Directory ed essere sincronizzato con Azure AD. Se non è possibile sincronizzare questo account a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />I requisiti di questo account del servizio sono i seguenti:<br /><br />Assegnazione dei diritti utente per l'- **accesso locale**. Questo diritto è richiesto per l'installazione e la configurazione dello scanner, ma non per il funzionamento. È necessario concedere questo diritto all'account del servizio, ma è possibile rimuoverlo dopo avere verificato che lo scanner è in grado di individuare, classificare e proteggere i file. Se non è possibile concedere questo diritto neppure per un breve periodo a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />Assegnazione dei diritti utente per l'- **accesso come servizio**. Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner. <br /><br />- Permissions to the data repositories: For data repositories on SharePoint on-premises, always grant the **Edit** permission if **Add and Customize Pages** is selected for the site, or grant the **Design** permission. For other data repositories, grant **Read** and **Write** permissions for scanning the files and then applying classification and protection to the files that meet the conditions in the Azure Information Protection policy. To run the scanner in discovery mode only for these other data repositories, **Read** permission is sufficient.<br /><br />- Per le etichette che riproteggono o rimuovono la protezione: per garantire che lo scanner abbia sempre accesso ai file protetti, trasformare l'account in un [utente con privilegi avanzati](configure-super-users.md) per il servizio Azure Rights Management e verificare che sia abilitata la funzionalità per utenti con privilegi avanzati. Per altre informazioni sui requisiti dell'account per l'applicazione della protezione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md). Se inoltre sono stati implementati i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione a fasi, verificare che questo account sia incluso nei controlli di onboarding configurati.|
|SQL Server per archiviare la configurazione dello scanner:<br /><br />- Istanza locale o remota<br /><br />- [Case insensitive collation](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />- Ruolo Sysadmin per installare lo scanner|SQL Server 2012 è la versione minima per le edizioni seguenti:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Se si installano più istanze dello scanner, ognuna di esse richiede la propria istanza di SQL Server.<br /><br />Quando si installa lo scanner e l'account ha il ruolo Sysadmin, il processo di installazione crea automaticamente il database AzInfoProtectionScanner e concede il ruolo db_owner necessario all'account del servizio che esegue lo scanner. Se non è possibile ricevere il ruolo Sysadmin o se l'organizzazione richiede che i database vengano creati e configurati manualmente, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />Le dimensioni del database di configurazione varieranno per ogni distribuzione, ma è consigliabile allocare 500 MB ogni 1.000.000 file da analizzare. |
|The Azure Information Protection client (classic) is installed on the Windows Server computer|È necessario installare il client completo per lo scanner. Non installare solo il modulo PowerShell del client.<br /><br />Per istruzioni sull'installazione del client, vedere la [guida per l'amministratore](./rms-client/client-admin-guide.md). Se lo scanner è stato installato in precedenza e ora è necessario aggiornarlo a una versione più recente, vedere [Aggiornamento dello scanner di Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|
|Etichette configurate che applicano la classificazione automatica e, facoltativamente, la protezione|Per altre informazioni su come configurare un'etichetta per le condizioni e applicare la protezione:<br /> - [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)<br /> - [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md) <br /><br />**Tip**: You can use the instructions from the [tutorial](infoprotect-quick-start-tutorial.md) to test the scanner with a label that looks for credit card numbers in a prepared Word document. Tuttavia, sarà necessario modificare la configurazione dell'etichetta in modo che l'opzione **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente** sia impostata su **Automatico** anziché su **Consigliato**. Rimuovere quindi l'etichetta dal documento (se applicata) e copiare il file in un repository di dati per lo scanner. Per eseguire test velocemente, è possibile copiare il file in una cartella locale nel computer dello scanner.<br /><br /> nonostante sia possibile eseguire lo scanner anche se non sono state configurate etichette che applicano la classificazione automatica, questo scenario non è illustrato in queste istruzioni. [Altre informazioni](#using-the-scanner-with-alternative-configurations)|
|For SharePoint document libraries and folders to be scanned:<br /><br />- SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|Altre versioni di SharePoint non sono supportate per lo scanner.<br /><br />When you use [versioning](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), the scanner inspects and labels the last published version. If the scanner labels a file and [content approval](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) is required, that labeled file must be approved to be available for users. <br /><br />Per le farm SharePoint di grandi dimensioni, controllare se è necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000) per lo scanner al fine di accedere a tutti i file. For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Per i documenti di Office da analizzare:<br /><br />- Formati di file 97-2003 e formati Office Open XML per Word, Excel e PowerPoint|Per altre informazioni sui tipi di file supportati dallo scanner per questi formati di file, vedere [Tipi di file supportati dal client Azure Information Protection](./rms-client/client-admin-guide-file-types.md)|
|Per i percorsi lunghi:<br /><br />- Massimo 260 caratteri, salvo se lo scanner è installato in Windows 2016 e il computer è configurato per il supporto dei percorsi lunghi|Windows 10 and Windows Server 2016 support path lengths greater than 260 characters with the following [group policy setting](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **All Settings** > **Enable Win32 long paths**<br /><br /> Per altre informazioni sul supporto dei percorsi di file lunghi, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) nella documentazione per sviluppatori di Windows 10.

Se non è possibile soddisfare tutti i requisiti indicati nella tabella perché non sono consentiti dai criteri dell'organizzazione, vedere la sezione successiva per conoscere le alternative.

Se tutti i requisiti sono soddisfatti, passare alla [sezione sull'installazione](#install-the-scanner).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Distribuzione dello scanner con configurazioni alternative

I prerequisiti elencati nella tabella sono i requisiti predefiniti per lo scanner e sono consigliati perché costituiscono la configurazione più semplice per la distribuzione dello scanner. Sono appropriati per il test iniziale, per poter controllare le funzionalità dello scanner. In un ambiente di produzione, tuttavia, i criteri dell'organizzazione potrebbero non consentire questi requisiti predefiniti a causa di una o più delle restrizioni seguenti:

- Servers are not allowed internet connectivity

- Non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

- Agli account del servizio non può essere concesso il diritto **Log on locally** (Accesso locale)

- Service accounts cannot be synchronized to Azure Active Directory but servers have internet connectivity

Lo scanner può soddisfare queste restrizioni, che tuttavia richiedono una configurazione aggiuntiva.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction: The scanner server cannot have internet connectivity

Seguire le istruzioni per un [computer disconnesso](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). 

Si noti che in questa configurazione lo scanner non può applicare la protezione (o rimuovere la protezione) usando la chiave basata sul cloud dell'organizzazione. Lo scanner può invece usare esclusivamente le etichette che applicano solo la classificazione o la protezione che usa [HYOK](configure-adrms-restrictions.md). 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restrizione: non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

Se è possibile concedere temporaneamente all'utente il ruolo Sysadmin per installare lo scanner, è possibile rimuovere questo ruolo al termine dell'installazione dello scanner. Quando si usa questa configurazione, il database viene creato automaticamente e all'account del servizio per lo scanner vengono concesse automaticamente le autorizzazioni necessarie. L'account utente che configura lo scanner richiede tuttavia il ruolo db_owner per il database AzInfoProtectionScanner ed è necessario concedere manualmente questo ruolo all'account utente.

If you cannot be granted the Sysadmin role even temporarily, you must ask a user with Sysadmin rights to manually create a database named AzInfoProtectionScanner before you install the scanner. For this configuration, the following roles must be assigned:
    
|Account|Ruolo a livello database|
|--------------------------------|---------------------|
|Account del servizio per lo scanner|db_owner|
|Account utente per l'installazione dello scanner|db_owner|
|Account utente per la configurazione dello scanner |db_owner|

In genere, si usa lo stesso account utente per installare e configurare lo scanner, ma, se si usano account diversi, entrambi richiedono il ruolo db_owner per il database AzInfoProtectionScanner.

To create a user and grant db_owner rights on this database, ask the Sysadmin to run the following SQL script twice. The first time, for the service account that runs the scanner, and the second time for you to install and manage the scanner. Before running the script, replace *domain\user* with the domain name and user account name of the service account or user account:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE AzInfoProtectionScanner IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

Inoltre:

- You must be a local administrator on the server that will run the scanner
- The service account that will run the scanner must be granted Full Control permissions to the following registry keys:
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

If, after configuring these permissions, you see an error when you install the scanner, the error can be ignored and you can manually start the scanner service.

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restrizione: all'account del servizio per lo scanner non può essere concesso il diritto **Log on locally** (Accesso locale)

Se i criteri dell'organizzazione non consentono il diritto **Log on locally** (Accesso locale) per gli account del servizio, ma consentono il diritto **Accesso come processo batch**, seguire le istruzioni per [specificare e usare il parametro Token per Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) della Guida dell'amministratore.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction: The scanner service account cannot be synchronized to Azure Active Directory but the server has internet connectivity

È possibile usare un account per eseguire il servizio dello scanner e un altro per l'autenticazione in Azure Active Directory:

- Per l'account del servizio dello scanner, è possibile usare un account Windows locale o un account Active Directory.

- Per l'account Azure Active Directory, seguire le istruzioni per [specificare e usare il parametro Token per Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) nella Guida dell'amministratore.


## <a name="install-the-scanner"></a>Installare lo scanner

1. Accedere al computer Windows Server che eseguirà lo scanner. Usare un account con diritti di amministratore locale e con le autorizzazioni per scrivere nel database master di SQL Server.

2. Aprire una sessione di Windows PowerShell con l'opzione **Esegui come amministratore**.

3. Eseguire il cmdlet **Install-AIPScanner**, che specifica l'istanza di SQL Server in cui creare un database per lo scanner di Azure Information Protection: 
    
    ```
    Install-AIPScanner -SqlServerInstance <name>
    ```
    
    Di seguito sono riportati alcuni esempi.
    
    Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`
    
    Quando richiesto, specificare le credenziali per l'account del servizio scanner (\<dominio\nome utente>) e la password.

4. Verificare che il servizio è ora installato usando **Strumenti di amministrazione** > **Servizi**. 
    
    Il servizio installato è denominato **Azure Information Protection Scanner** ed è configurato per essere eseguito usando l'account del servizio scanner creato.

Ora che è stato installato lo scanner, è necessario ottenere un token di Azure AD per l'account del servizio scanner da autenticare in modo che possa essere eseguito automaticamente. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Ottenere un token di Azure AD per lo scanner

Il token di Azure AD consente all'account del servizio scanner di eseguire l'autenticazione per il servizio Azure Information Protection.

1. Dallo stesso computer Windows Server, o dal desktop, accedere al portale di Azure per creare due applicazioni di Azure AD necessarie per specificare un token di accesso per l'autenticazione. Dopo un accesso interattivo iniziale, questo token consente di eseguire lo scanner in modo non interattivo.
    
    Per creare queste applicazioni, seguire le istruzioni della sezione [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) della guida per l'amministratore.

2. Dal computer Windows Server, se all'account del servizio scanner è stato concesso il diritto di **accesso locale** per l'installazione: accedere con questo account e avviare una sessione di PowerShell. Eseguire **Set-AIPAuthentication** specificando i valori copiati nel passaggio precedente:
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```
    
    Quando richiesto, specificare la password per le credenziali dell'account del servizio per Azure AD e quindi fare clic su **Accetto**.
    
    Se all'account del servizio scanner non è possibile concedere il diritto di **accesso locale** per l'installazione: seguire le istruzioni nella sezione [Specificare e usare il parametro Token per Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) della Guida dell'amministratore. 

Lo scanner ora ha un token per l'autenticazione ad Azure AD, che può essere valido per un anno, due anni, o senza scadenza, in base alla configurazione dell'**app Web/API** in Azure AD. Quando il token scade, è necessario ripetere i passaggi 1 e 2.

A questo punto si è pronti a specificare gli archivi dati da analizzare. 

## <a name="specify-data-stores-for-the-scanner"></a>Specificare gli archivi dati per lo scanner

Usare il cmdlet **Add-AIPScannerRepository** per specificare gli archivi dati che devono essere analizzati dallo scanner di Azure Information Protection. You can specify local folders, UNC paths, and SharePoint Server URLs for SharePoint document libraries and folders. 

Supported versions for SharePoint: SharePoint Server 2019, SharePoint Server 2016, and SharePoint Server 2013. Anche SharePoint Server 2010 è supportato per i clienti che dispongono del [supporto "Extended" per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

1. Dallo stesso computer Windows Server, nella sessione di PowerShell, aggiungere il primo archivio dati eseguendo il comando seguente:
    
        Add-AIPScannerRepository -Path <path>
    
    ad esempio `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    For other examples, use the PowerShell help command `Get-Help Add-AIPScannerRepository -examples` for this cmdlet.

2. Ripetere questo comando per tutti gli archivi dati da analizzare. Per rimuovere un archivio dati aggiunto in precedenza, usare il cmdlet **Remove-AIPScannerRepository**.

3. Verificare di avere specificato correttamente tutti gli archivi dati eseguendo il cmdlet **Get-AIPScannerRepository**:
    
        Get-AIPScannerRepository

Con la configurazione predefinita dello scanner ora è possibile eseguire la prima analisi in modalità di individuazione.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner

1. Nella sessione di PowerShell avviare lo scanner eseguendo il comando seguente:
    
        Start-AIPScan
    
    In alternativa, è possibile avviare lo scanner dal portale di Azure. From the **Azure Information Protection - Nodes** pane, select your scanner node, and then the **Scan now** option:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

2. Attendere che lo scanner completi il ciclo eseguendo il comando seguente:
    
        Get-AIPScannerStatus
    
    Alternatively, you can view the status from the **Azure Information Protection - Nodes** pane in the Azure portal, by checking the **STATUS** column.
    
    Cercare lo stato **Idle** (Inattivo) invece di **Scanning** (Analisi in corso).
    
    Quando lo scanner ha completato l'analisi per tutti i file negli archivi dati specificati, lo scanner viene arrestato anche se il servizio scanner rimane in esecuzione.
    
    Controllare il registro eventi locale **Applicazioni e servizi** di Windows, **Azure Information Protection**. Questo registro indica anche quando lo scanner ha completato l'analisi, con un riepilogo dei risultati. Cercare l'ID evento informativo **911**.

3. Esaminare i report archiviati in %*localappdata*%\Microsoft\MSIP\Scanner\Reports. I file summary.txt includono il tempo impiegato per l'analisi, il numero di file analizzati e il numero di file con una corrispondenza per i tipi di informazioni. I file con estensione csv includono ulteriori dettagli per ogni file. In questa cartella vengono archiviati fino a 60 report per ogni ciclo di analisi e tutti i report tranne l'ultimo vengono compressi per ridurre al minimo lo spazio su disco necessario.
    
    > [!NOTE]
    > È possibile modificare il livello di registrazione usando il parametro *ReportLevel* con **Set-AIPScannerConfiguration**, ma non è possibile modificare il percorso della cartella o il nome del report. Valutare la possibilità di usare una giunzione di directory per la cartella, se si vogliono archiviare i report in un volume o una partizione diversi.
    >
    > Ad esempio, usando il comando [Mklink](/windows-server/administration/windows-commands/mklink): `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Con l'impostazione predefinita, solo i file che soddisfano le condizioni configurate per la classificazione automatica vengono inclusi nei report dettagliati. Se non si vedono etichette applicate in questi report, controllare che la configurazione delle etichette includa la classificazione automatica anziché consigliata.
    
    > [!TIP]
    > Gli scanner inviano queste informazioni ad Azure Information Protection ogni cinque minuti, in modo che sia possibile visualizzare i risultati quasi in tempo reale dal portale di Azure. Per altre informazioni, vedere [Reporting per Azure Information Protection](reports-aip.md). 
        
    Se i risultati non sono quelli previsti, potrebbe essere necessario ottimizzare le condizioni specificate nei criteri di Azure Information Protection. In questo caso, ripetere i passaggi da 1 a 3 finché non si è pronti a modificare la configurazione per applicare la classificazione e, facoltativamente, la protezione. 

Il portale di Azure visualizza solo le informazioni sull'ultima analisi. Se è necessario visualizzare i risultati delle analisi precedenti, tornare ai report archiviati nel computer dello scanner, nella cartella %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quando si è pronti ad etichettare automaticamente i file individuati dallo scanner, passare alla procedura successiva. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurare lo scanner per applicare la classificazione e la protezione

Per impostazione predefinita, lo scanner viene eseguito una volta e solo ai fini della creazione di report. To change these settings, use the **Set-AIPScannerConfiguration**:

1. Eseguire il comando seguente nel computer Windows Server, nella sessione di PowerShell:
    
        Set-AIPScannerConfiguration -Enforce On -Schedule Always
    
    Esistono altre impostazioni di configurazione che è opportuno modificare. Indicare ad esempio se gli attributi dei file vengono modificati e quali informazioni vengono registrate nei report. Inoltre, se i criteri di Azure Information Protection includono l'impostazione che richiede un messaggio di giustificazione per abbassare il livello di classificazione o rimuovere la protezione, specificare il messaggio usando questo cmdlet. Use the following PowerShell help command for more information about each configuration setting: `Get-Help Set-AIPScannerConfiguration -detailed`

2. Prendere nota dell'ora corrente e avviare di nuovo lo scanner eseguendo il comando seguente:
    
        Start-AIPScan
    
    In alternativa, è possibile avviare lo scanner dal portale di Azure. From the **Azure Information Protection - Nodes** pane, select your scanner node, and then the **Scan now** option:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

3. Monitorare di nuovo il tipo di evento informativo **911** nel registro eventi, con un timestamp successivo all'avvio dell'analisi nel passaggio precedente. 
    
    Controllare quindi i report per visualizzare i dettagli dei file etichettati, la classificazione applicata a ogni file e se la protezione è stata applicata. In alternativa, usare il portale di Azure per visualizzare più facilmente queste informazioni.

Poiché la pianificazione è stata configurata in modo da essere eseguita continuamente, quando lo scanner ha completato l'analisi di tutti i file, avvia un nuovo ciclo per individuare eventuali file nuovi e modificati.


## <a name="how-files-are-scanned"></a>Modalità di analisi dei file

Lo scanner esegue i processi seguenti per l'analisi di file.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determine whether files are included or excluded for scanning 
Lo scanner ignora automaticamente i file [esclusi dalla classificazione e dalla protezione](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection), ad esempio file eseguibili e file di sistema.

È possibile modificare questo comportamento definendo un elenco di tipi di file da includere o escludere dall'analisi. Quando si specifica questo elenco e non si specifica un repository di dati, l'elenco si applica a tutti i repository di dati per cui non è stato specificato un elenco. Per specificare questo elenco, usare **Set-AIPScannerScannedFileTypes**. 

Dopo aver specificato l'elenco di tipi di file, è possibile aggiungere un nuovo tipo di file all'elenco usando **Add-AIPScannerScannedFileTypes** e rimuovere un tipo di file dall'elenco usando **Remove-AIPScannerScannedFileTypes**.

### <a name="2-inspect-and-label-files"></a>2. Inspect and label files

Lo scanner usa quindi i filtri per l'analisi dei tipi di file supportati. Gli stessi filtri vengono usati dal sistema operativo per Windows Search e per l'indicizzazione. Windows IFilter viene usato senza alcuna configurazione aggiuntiva per l'analisi di file usati da Word, Excel e PowerPoint, nonché di documenti PDF e file di testo.

Per l'elenco completo dei tipi di file supportati per impostazione predefinita e per informazioni aggiuntive su come configurare filtri esistenti che includono i file con estensione zip e tiff, vedere [Tipi di file supportati per il controllo](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection).

Dopo il controllo è possibile contrassegnare questi file mediante le condizioni specificate per le etichette. In alternativa, se si usa la modalità di individuazione, i file possono essere segnalati se contengono le condizioni specificate per le etichette o tutti i tipi di informazioni riservate noti. 

Tuttavia lo scanner non è in grado di contrassegnare i file nelle circostanze seguenti:

- Se l'etichetta applica classificazione ma non protezione e il tipo di file non [supporta solo la classificazione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Se l'etichetta applica classificazione e protezione, ma lo scanner non protegge il tipo di file.
    
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. È possibile impostare la protezione di altri tipi di file quando si [modifica il Registro di sistema](#editing-the-registry-for-the-scanner), come descritto in una delle sezioni seguenti.

Ad esempio, dopo il controllo di file con estensione txt, lo scanner non può applicare un'etichetta configurata per la classificazione ma non per la protezione, perché il tipo di file con estensione txt non supporta la sola classificazione. Se l'etichetta è configurata per la classificazione e la protezione dati e il Registro di sistema viene modificato per il tipo di file con estensione txt, lo scanner può applicare un'etichetta al file. 

> [!TIP]
> Durante questo processo, se lo scanner si arresta e non completa l'analisi di un numero elevato di file in un repository:
> 
> - Potrebbe essere necessario aumentare il numero di porte dinamiche per il sistema operativo che ospita i file. Uno dei motivi per cui lo scanner supera il numero di connessioni di rete consentite e pertanto si arresta può essere la protezione avanzata dei server per SharePoint.
>     
>     To check whether this is the cause of the scanner stopping, look to see if the following error message is logged for the scanner in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zipped if there are multiple logs): **Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port**
>    
>     Per altre informazioni su come visualizzare l'intervallo di porte corrente e aumentarlo, vedere [Impostazioni che possono essere modificate per migliorare le prestazioni di rete](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
> 
> - Per le farm SharePoint di grandi dimensioni, potrebbe essere necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000). For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Label files that can't be inspected
Per i tipi di file che non possono essere controllati, lo scanner applica l'etichetta predefinita nei criteri di Azure Information Protection oppure l'etichetta predefinita configurata per lo scanner.

Come nel passaggio precedente, lo scanner non è in grado di contrassegnare i file nelle circostanze seguenti:

- Se l'etichetta applica classificazione ma non protezione e il tipo di file non [supporta solo la classificazione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Se l'etichetta applica classificazione e protezione, ma lo scanner non protegge il tipo di file.
    
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. È possibile impostare la protezione di altri tipi di file quando si [modifica il Registro di sistema](#editing-the-registry-for-the-scanner), come descritto di seguito.


### <a name="editing-the-registry-for-the-scanner"></a>Modifica del Registro di sistema per lo scanner

Per modificare il comportamento predefinito dello scanner per la protezione di tipi di file diversi dai file di Office e i file PDF, è necessario modificare manualmente il Registro di sistema e specificare i tipi di file aggiuntivi da proteggere e il tipo di protezione (nativa o generica). Per informazioni, vedere [Configurazione dell'API file](develop/file-api-configuration.md) nelle linee guida per sviluppatori. Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile". Inoltre, specificatamente per lo scanner:

- The scanner has its own default behavior: Only Office file formats and PDF documents are protected by default. Se il Registro di sistema non viene modificato, tutti gli altri tipi di file non verranno etichettati né protetti dallo scanner.

- If you want the same default protection behavior as the Azure Information Protection client, where all files are automatically protected with native or generic protection: Specify the `*` wildcard as a registry key, `Encryption` as the value (REG_SZ), and `Default` as the value data.

Quando si modifica il Registro di sistema, creare manualmente la chiave **MSIPC** e la chiave **FileProtection** se non esistono, nonché una chiave per ogni estensione del nome file.

Ad esempio, per fare in modo che lo scanner protegga le immagini TIFF oltre ai file di Office e ai file PDF, il Registro di sistema dopo la modifica avrà un aspetto simile all'immagine seguente. Dato che sono file immagine, i file con estensione tiff supportano la protezione nativa e l'estensione di file risultante è ptiff.

![Modifica del Registro di sistema per l'applicazione della protezione con lo scanner](./media/editregistry-scanner.png)

Per un elenco di file di testo e file immagine che supportano la protezione nativa ma vanno specificati nel Registro di sistema, vedere [Tipi di file supportati per la classificazione e la protezione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) nella Guida dell'amministratore.

Per i file che non supportano la protezione nativa, specificare l'estensione del nome file come nuova chiave e **PFile** per la protezione generica. L'estensione del nome file risultante per il file protetto è pfile.


## <a name="when-files-are-rescanned"></a>Ripetizione dell'analisi dei file

Per il primo ciclo di analisi, lo scanner analizza tutti i file negli archivi dati configurati e quindi per le analisi successive, vengono controllati solo i file nuovi o modificati. 

You can force the scanner to inspect all files again by running **Start-AIPScan** with the *Reset* parameter. The scanner must be configured for a manual schedule, which requires the *Schedule* parameter to be set to **Manual** with **Set-AIPScannerConfiguration**.

Alternatively, you can force the scanner to inspect all files again from the **Azure Information Protection - Nodes** pane in the Azure portal. Selezionare lo scanner nell'elenco e quindi selezionare l'opzione **Ripeti l'analisi di tutti i file**:

![Avviare un'altra analisi per lo scanner di Azure Information Protection](./media/scanner-rescan-files.png)

È utile verificare nuovamente i file quando si vuole che i report includano tutti i file e questa configurazione viene in genere usata quando lo scanner viene eseguito in modalità di individuazione. Al termine di un'analisi completa, il tipo di analisi diventa automaticamente incrementale in modo che per le analisi successive vengono analizzati solo i file nuovi o modificati.

Inoltre, tutti i file vengono controllati quando lo scanner scarica un criterio di Azure Information Protection con condizioni nuove o modificate. Lo scanner aggiorna i criteri ogni ora, all'avvio del servizio e quando risalgono a più di un'ora prima.  

> [!TIP]
> Se è necessario aggiornare i criteri prima di questo intervallo di un'ora, ad esempio durante un periodo di test, eliminare manualmente il file dei criteri **Policy.msip** da **%LocalAppData%\Microsoft\MSIP\Policy.msip** e **%LocalAppData%\Microsoft\MSIP\Scanner**. Riavviare il servizio scanner di Azure Information Protection.
> 
> Se sono state modificate le impostazioni di protezione dei criteri, attendere 15 minuti dal salvataggio delle impostazioni di protezione prima di riavviare il servizio.

Se lo scanner ha scaricato criteri per cui non sono state configurate condizioni automatiche, la copia del file dei criteri nella cartella dello scanner non viene aggiornata. In questo scenario, è necessario eliminare il file di criteri **Policy.msip** sia da **%LocalAppData%\Microsoft\MSIP\Policy.msip** che da **%LocalAppData%\Microsoft\MSIP\Scanner** prima che lo scanner possa usare un nuovo file dei criteri scaricato con etichette calcolate correttamente per le condizioni automatiche.

## <a name="using-the-scanner-with-alternative-configurations"></a>Uso dello scanner con configurazioni alternative

Lo scanner di Azure Information Protection supporta due scenari alternativi in cui non è necessario configurare le etichette per le condizioni: 
- Applicare un'etichetta predefinita a tutti i file in un repository di dati.
    
    Per questa configurazione, usare il cmdlet **Set-AIPScannerRepository** e impostare il parametro *MatchPolicy* su **Off**. 
    
    I contenuti dei file non vengono esaminati e tutti i file nel repository di dati vengono etichettati in base all'etichetta predefinita specificata per il repository (con il parametro *SetDefaultLabel*) oppure, se questa non è specificata, con l'etichetta predefinita specificata come impostazione di criteri per l'account dello scanner.
    

- Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.
    
    Per questa configurazione, usare il cmdlet **Set-AIPScannerConfiguration** e impostare il parametro *DiscoverInformationTypes* su **All**.
    
    Lo scanner usa eventuali condizioni personalizzate specificate per le etichette nei criteri di Azure Information Protection e l'elenco di tipi di informazioni che è possibile specificare per le etichette nei criteri di Azure Information Protection.
    
    The following quickstart uses this configuration, although it's for the current version of the scanner: [Quickstart: Find what sensitive information you have](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Ottimizzazione delle prestazioni dello scanner

Usare le linee guida seguenti per ottimizzare le prestazioni dello scanner. However, if your priority is the responsiveness of the scanner computer rather than the scanner performance, you can use an [advanced client setting](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) to limit the number of threads used by the scanner.

Per ottimizzare le prestazioni dello scanner:

- **Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**
    
    Ad esempio, inserire il computer dello scanner nella stessa rete LAN o (scelta consigliata) nello stesso segmento di rete dell'archivio dei dati analizzati.
    
    La qualità della connessione di rete influisce sulle prestazioni dello scanner perché per controllare i file lo scanner trasferisce il contenuto dei file nel computer che esegue il servizio di analisi. Quando si riduce o si elimina il numero di hop di rete per i dati, si riduce anche il carico sulla rete. 

- **Verificare che il computer dello scanner abbia risorse del processore disponibili**
    
    La ricerca di una corrispondenza nel contenuto dei file in base alle condizioni configurate e la crittografia e la decrittografia dei file sono operazioni che richiedono un uso intensivo del processore. Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se una mancanza di risorse del processore influisce negativamente sulle prestazioni dello scanner.
    
- **Non eseguire l'analisi delle cartelle locali nel computer che esegue il servizio di analisi**
    
    Se sono presenti cartelle da analizzare in un server di Windows, installare lo scanner in un computer diverso e configurare le cartelle come condivisioni di rete da analizzare. La separazione delle due funzioni di hosting dei file e di analisi dei file fa in modo che le risorse di elaborazione di questi servizi non siano in competizione tra loro.

Se necessario, installare più istanze dello scanner. Ogni istanza dello scanner richiede un proprio database di configurazione in un'istanza diversa di SQL Server.

Altri fattori che influenzano le prestazioni dello scanner:

- Carico corrente e tempi di risposta degli archivi dati che contengono i file da analizzare

- Esecuzione dello scanner in modalità di individuazione o applicazione
    
    La modalità di individuazione ha in genere una velocità di analisi maggiore rispetto alla modalità di applicazione poiché l'individuazione richiede una sola azione di lettura dei file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.

- Modifica delle condizioni in Azure Information Protection
    
    Il primo ciclo di analisi nel quale lo scanner deve controllare ogni file richiede più tempo rispetto ai cicli di analisi successivi in cui, per impostazione predefinita, vengono analizzati solo i file nuovi e modificati. Tuttavia, se si modificano le condizioni nei criteri di Azure Information Protection, tutti i file vengono analizzati nuovamente come descritto nella [sezione precedente](#when-files-are-rescanned).

- La costruzione di espressioni regex per condizioni personalizzate
    
    Per evitare un consumo intenso di memoria e il rischio di timeout (15 minuti per ogni file), rivedere le espressioni regex per assicurarsi che usino criteri di ricerca efficienti. Ad esempio:
    
    - Evitare [quantificatori greedy](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - Usare gruppi di non acquisizione, ad esempio `(?:expression)` invece di `(expression)`

- Livello di registrazione selezionato
    
    È possibile scegliere tra **Debug**, **Info** (Informazioni), **Error** (Errore) e **Off** (Disattivato) per i report dello scanner. **Off** (Disattivato) offre le prestazioni migliori; **Debug** rallenta considerevolmente lo scanner ed è consigliabile usarlo solo per la ricerca e la risoluzione dei problemi. For more information, see the *ReportLevel* parameter for the Set-AIPScannerConfiguration cmdlet by running `Get-Help Set-AIPScannerConfiguration -detailed`.

- File:
    
    - With the exception of Excel files, Office files are more quickly scanned than PDF files.
    
    - I file non protetti sono più veloci da analizzare rispetto ai file protetti.
    
    - I file di grandi dimensioni richiedono più tempo per l'analisi rispetto ai file di piccole dimensioni.

- Inoltre:
    
    - Confirm that the service account that runs the scanner has only the rights documented in the [scanner prerequisites](#prerequisites-for-the-azure-information-protection-scanner) section, and then configure the [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) to disable the low integrity level for the scanner.
    
    - L'esecuzione dello scanner è più rapida quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per applicare un'etichetta predefinita a tutti i file in quanto lo scanner non esamina i contenuti del file.
    
    - L'esecuzione dello scanner è più lenta quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.
    
    - You can decrease the scanner timeouts with [advanced client settings](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) for better scanning rates and lower memory consumption, but with the acknowledgment that some files might be skipped.

## <a name="list-of-cmdlets-for-the-scanner"></a>Elenco dei cmdlet per lo scanner 

Altri cmdlet per lo scanner consentono di modificare l'account del servizio e il database per lo scanner, ottenere le impostazioni correnti per lo scanner e disinstallare il servizio scanner. Lo scanner usa i cmdlet seguenti:

- Add-AIPScannerScannedFileTypes

- Add-AIPScannerRepository

- Get-AIPScannerConfiguration

- Get-AIPScannerRepository

- Get-AIPScannerStatus

- Install-AIPScanner

- Remove-AIPScannerRepository

- Remove-AIPScannerScannedFileTypes

- Set-AIPScanner

- Set-AIPScannerConfiguration

- Set-AIPScannerScannedFileTypes

- Set-AIPScannerRepository

- Start-AIPScan

- Uninstall-AIPScanner

- Update-AIPScanner

> [!NOTE]
> Many of these cmdlets are now deprecated in the current version of the scanner, and the online help for the scanner cmdlets reflects this change. For cmdlet help earlier than version 1.48.204.0 of the scanner, use the built-in `Get-Help <cmdlet name>` command in your PowerShell session.

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID registro eventi e descrizioni per lo scanner

Usare le sezioni seguenti per identificare gli ID evento e le descrizioni possibili per lo scanner. Gli eventi vengono registrati nel server su cui viene seguito il servizio scanner, nel registro eventi di **applicazioni e servizi** di Windows, **Azure Information Protection**.

-----

Informazione **910**

**Ciclo dello scanner avviato.**

Questo evento viene registrato quando il servizio scanner viene avviato e inizia a cercare i file negli archivi dati specificati.

----

Informazione **911**

**Ciclo dello scanner completato.**

Questo evento viene registrato quando lo scanner ha completato un'analisi manuale o un ciclo in caso di pianificazione continua.

Se lo scanner è stato configurato per l'esecuzione manuale anziché continua, per eseguire una nuova analisi usare il cmdlet **Start-AIPScan**. Per modificare la pianificazione, usare il cmdlet **Set AIPScannerConfiguration** e il parametro *Pianificazione*.

----

## <a name="next-steps"></a>Passaggi successivi

Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

Scoprire [Qual è la differenza tra Infrastruttura di classificazione file di Windows Server e lo scanner di Azure Information Protection](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner).

È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).
