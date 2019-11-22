---
title: Deploy the Azure Information Protection scanner - AIP
description: Instructions to install, configure, and run the current version of the Azure Information Protection scanner to discover, classify, and protect files on data stores.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bc49fc0721ad3b3fff09856a84fdc91718d0a1d0
ms.sourcegitcommit: d9442efe61b55bb158bd50ee69873c028234842d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297633"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2*
>
> [!NOTE]
> This article is for the current general availability version of the Azure Information Protection scanner with the Azure Information Protection client (classic), and the preview version of the scanner for the current general availability version of the Azure Information Protection unified labeling client.
> 
> If you have previously installed the scanner and want to upgrade it, use the following upgrade instructions and then use the instructions on this page, omitting the step to install the scanner:
> - For the classic client: [Upgrading the Azure Information Protection scanner](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> - For the unified labeling client: [Upgrading the Azure Information Protection scanner](./rms-client/clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> 
> If you have a version of the scanner that is older than 1.48.204.0 and you're not ready to upgrade it, see [Deploying previous versions of the Azure Information Protection scanner to automatically classify and protect files](deploy-aip-scanner-previousversions.md).


Di seguito vengono illustrate le caratteristiche dello scanner di Azure Information Protection e le relative procedure per installarlo, configurarlo ed eseguirlo.

Questo scanner viene eseguito come servizio in Windows Server e consente di individuare, classificare e proteggere i file negli archivi dati seguenti:

- Cartelle locali nel computer Windows Server che esegue lo scanner.

- Percorsi UNC delle condivisioni di rete che usano il protocollo SMB (Server Message Block).

- Document libraries and folders for SharePoint Server 2019 through SharePoint Server 2013. SharePoint 2010 è supportato anche per i clienti che dispongono del [supporto "Extended" per la versione corrente di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Per analizzare ed etichettare i file nei repository cloud, usare [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) invece dello scanner.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Panoramica dello scanner di Azure Information Protection

When you have configured labels that apply automatic classification, files that this scanner discovers can then be labeled. Le etichette applicano la classificazione e, facoltativamente, applicano o rimuovono la protezione:

![Panoramica dell'architettura dello scanner di Azure Information Protection](./media/infoprotect-scanner.png)

Lo scanner può controllare tutti i file indicizzabili da Windows, tramite IFilter installati nel computer. In seguito, per stabilire se i file devono essere etichettati, lo scanner usa il rilevamento di modelli e di tipi di dati sensibili della prevenzione della perdita di dati (DLP) predefiniti in Office 365 o i modelli regex di Office 365. Because the scanner uses the Azure Information Protection client (the classic client or unified labeling client), the scanner can classify and protect the same file types:

- The classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)

- The unified labeling  client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)

È possibile eseguire lo scanner solo in modalità di individuazione, in cui si usano i report per verificare che cosa accadrebbe se i file fossero etichettati. Oppure è possibile eseguire lo scanner per applicare automaticamente le etichette. È anche possibile eseguire lo scanner per individuare i file che contengono tipi di informazioni riservate, senza configurare le etichette per le condizioni per l'applicazione della classificazione automatica.

Si noti che lo scanner non individua e non applica etichette in tempo reale. Effettua sistematicamente una ricerca per indicizzazione nei file presenti negli archivi dati specificati ed è possibile configurare questo ciclo in modo da eseguirlo una o più volte.

È possibile specificare quali tipi di file analizzare o escludere dall'analisi, definendo un elenco di tipi di file come parte della configurazione dello scanner.


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prerequisiti per lo scanner di Azure Information Protection
Prima di installare lo scanner di Azure Information Protection, verificare che i requisiti seguenti siano soddisfatti.

|Requisito|Ulteriori informazioni|
|---------------|--------------------|
|Computer Windows Server per eseguire il servizio scanner:<br /><br />- 4 processori core<br /><br />- 8 GB di RAM<br /><br />- 10 GB di spazio libero (media) per i file temporanei|Windows Server 2019, Windows Server 2016, or Windows Server 2012 R2. <br /><br />Nota: per scopi di test o valutazione in un ambiente non di produzione, è possibile usare un sistema operativo client Windows [supportato dal client di Azure Information Protection](requirements.md#client-devices).<br /><br />Il computer può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare.<br /><br /> Lo scanner richiede spazio su disco sufficiente a creare i file temporanei per ogni file analizzato, quattro file per core. Lo spazio su disco consigliato di 10 GB consente a 4 processori core di analizzare 16 file, ognuno con una dimensione di 625 MB. <br /><br /> If internet connectivity is not possible because of your organization policies, see the [Deploying the scanner with alternative configurations](#deploying-the-scanner-with-alternative-configurations) section. Otherwise, make sure that this computer has internet connectivity that allows the following URLs over HTTPS (port 443):<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com <br /> \*.protection.outlook.com (scanner from the unified labeling client only)|
|Account del servizio per eseguire il servizio scanner|Oltre a eseguire il servizio scanner nel computer Windows Server, questo account di Windows esegue l'autenticazione in Azure AD e scarica i criteri di Azure Information Protection. Questo account deve essere un account Active Directory ed essere sincronizzato con Azure AD. Se non è possibile sincronizzare questo account a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />I requisiti di questo account del servizio sono i seguenti:<br /><br />Assegnazione dei diritti utente per l'- **accesso locale**. Questo diritto è richiesto per l'installazione e la configurazione dello scanner, ma non per il funzionamento. È necessario concedere questo diritto all'account del servizio, ma è possibile rimuoverlo dopo avere verificato che lo scanner è in grado di individuare, classificare e proteggere i file. Se non è possibile concedere questo diritto neppure per un breve periodo a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />Assegnazione dei diritti utente per l'- **accesso come servizio**. Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner. <br /><br />- Autorizzazioni per i repository di dati: è necessario concedere le autorizzazioni per la **lettura** e la **scrittura** per analizzare i file e quindi applicare la classificazione e la protezione ai file che soddisfano le condizioni indicate nei criteri di Azure Information Protection. Per eseguire lo scanner solo in modalità di individuazione, è sufficiente l'autorizzazione per la **lettura**.<br /><br />- For labels that reprotect or remove protection: To ensure that the scanner always has access to protected files, make this account a [super user](configure-super-users.md) for Azure Information Protection, and ensure that the super user feature is enabled. Se inoltre sono stati implementati i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione a fasi, verificare che questo account sia incluso nei controlli di onboarding configurati.|
|SQL Server per archiviare la configurazione dello scanner:<br /><br />- Istanza locale o remota<br /><br />- [Case insensitive collation](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />- Ruolo Sysadmin per installare lo scanner|SQL Server 2012 è la versione minima per le edizioni seguenti:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Lo scanner di Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di profilo personalizzato per lo scanner. When you use the preview version of the scanner from the unified labeling client, multiple scanners can share the same configuration database.<br /><br />Quando si installa lo scanner e l'account ha il ruolo Sysadmin, il processo di installazione crea automaticamente il database di configurazione dello scanner e concede il ruolo db_owner necessario all'account del servizio che esegue lo scanner. Se non è possibile ricevere il ruolo Sysadmin o se l'organizzazione richiede che i database vengano creati e configurati manualmente, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br /> For capacity guidance, see [Storage requirements and capacity planning for SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).|
|Either of the following Azure Information Protection clients is installed on the Windows Server computer <br /><br /> - Classic client <br /><br /> - Unified labeling client ([current general availability version only](./rms-client/unifiedlabelingclient-version-release-history.md#version-25330)) |È necessario installare il client completo per lo scanner. Non installare solo il modulo PowerShell del client.<br /><br />For installation and upgrade instructions: <br /> - [Classic client](./rms-client/client-admin-guide.md)<br /> - [Unified labeling client](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner) |
|Etichette configurate che applicano la classificazione automatica e, facoltativamente, la protezione|For instructions for the classic client to configure a label for conditions and to apply protection:<br /> - [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)<br /> - [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md) <br /><br />Tip: You can use the instructions from the [tutorial](infoprotect-quick-start-tutorial.md) to test the scanner with a label that looks for credit card numbers in a prepared Word document. Tuttavia, sarà necessario modificare la configurazione dell'etichetta in modo che l'opzione **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente** sia impostata su **Automatico** anziché su **Consigliato**. Rimuovere quindi l'etichetta dal documento (se applicata) e copiare il file in un repository di dati per lo scanner. Per eseguire test velocemente, è possibile copiare il file in una cartella locale nel computer dello scanner.<br /><br /> For instructions for the unified labeling client to configure a label for auto-labeling and to apply protection:<br /> - [Apply a sensitivity label to content automatically](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)<br /> - [Restrict access to content by using encryption in sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)<br /><br /> nonostante sia possibile eseguire lo scanner anche se non sono state configurate etichette che applicano la classificazione automatica, questo scenario non è illustrato in queste istruzioni. [Altre informazioni](#using-the-scanner-with-alternative-configurations)|
|For SharePoint document libraries and folders to be scanned:<br /><br />- SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|Altre versioni di SharePoint non sono supportate per lo scanner.<br /><br />When you use [versioning](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), the scanner inspects and labels the last published version. If the scanner labels a file and [content approval](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) is required, that labeled file must be approved to be available for users. <br /><br />Per le farm SharePoint di grandi dimensioni, controllare se è necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000) per lo scanner al fine di accedere a tutti i file. For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Per i documenti di Office da analizzare:<br /><br />- Formati di file 97-2003 e formati Office Open XML per Word, Excel e PowerPoint|For more information about the file types that the scanner supports for these file formats, see the following information: <br />- Classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)<br />- Unified labeling client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)|
|Per i percorsi lunghi:<br /><br />- Massimo 260 caratteri, salvo se lo scanner è installato in Windows 2016 e il computer è configurato per il supporto dei percorsi lunghi|Windows 10 and Windows Server 2016 support path lengths greater than 260 characters with the following [group policy setting](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **All Settings** > **Enable Win32 long paths**<br /><br /> Per altre informazioni sul supporto dei percorsi di file lunghi, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) nella documentazione per sviluppatori di Windows 10.

If you can't meet all the requirements in the table because they are prohibited by your organization policies, see the [alternative configurations](#deploying-the-scanner-with-alternative-configurations) section.

When you deploy the scanner in production, or you're testing the performance for multiple scanners, see the next section for capacity planning guidance for SQL Server.

However, if you're ready to start deploying the scanner, go straight to [configuring the scanner section](#configure-the-scanner-in-the-azure-portal).

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Storage requirements and capacity planning for SQL Server

The amount of disk space required for the scanner's configuration database and the specification of the computer running SQL Server can vary for each environment, so we encourage you to do your own testing. However, you can use the following guidance as a starting point.

See the [Optimizing the performance of the scanner](#optimizing-the-performance-of-the-scanner) section for additional information.

##### <a name="scanner-from-the-classic-client"></a>Scanner from the classic client:

- **Disk size**: The size of the configuration database will vary for each deployment but we recommend you allocate 500 MB for every 1,000,000 files that you want to scan.

- **For each scanner**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

##### <a name="scanner-from-the-unified-labeling-client"></a>Scanner from the unified labeling client:

- **Disk size**: Although the size of the scanner configuration database will vary for each deployment, you can use the following equation as guidance: `100 KB + <file count> *(1000 + 4*<average file name length>)`. 
    
    For example, to scan 1 million files that have an average file name length of 250 bytes, allocate 2 GB disk space.

- **For multiple scanners, up to 12**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

- **For multiple scanners more than 12 (maximum 40)** : 8 core processes; 16 GB RAM recommended (8 GB minimum).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Distribuzione dello scanner con configurazioni alternative

I prerequisiti elencati nella tabella sono i requisiti predefiniti per lo scanner e sono consigliati perché costituiscono la configurazione più semplice per la distribuzione dello scanner. Sono appropriati per il test iniziale, per poter controllare le funzionalità dello scanner. In un ambiente di produzione, tuttavia, i criteri dell'organizzazione potrebbero non consentire questi requisiti predefiniti a causa di una o più delle restrizioni seguenti:

- Servers are not allowed internet connectivity

- Non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

- Agli account del servizio non può essere concesso il diritto **Log on locally** (Accesso locale)

- Service accounts cannot be synchronized to Azure Active Directory but servers have internet connectivity

Lo scanner può soddisfare queste restrizioni, che tuttavia richiedono una configurazione aggiuntiva.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction: The scanner server cannot have internet connectivity

Follow the instructions from the admin guides to support a disconnected computer:

- For the classic client: [Support for disconnected computers](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the classic client cannot apply protection, remove protection, or inspect protected files by using your organization's cloud-based key. Instead, the scanner is limited to using labels that apply classification only, or apply protection that uses [HYOK](configure-adrms-restrictions.md)

- For the unified labeling client: [Support for disconnected computers](./rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the unified labeling client can apply protection, remove protection, and inspect protected files by using the *DelegatedUser* parameter with the [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) cmdlet.

Procedere quindi come segue:

1. Configurare lo scanner nel portale di Azure, creando un profilo dello scanner. Se occorre assistenza per questo passaggio, vedere [Configurare lo scanner nel portale di Azure](#configure-the-scanner-in-the-azure-portal).

2. Export your scanner profile from the **Azure Information Protection - Profiles** pane, by using the **Export** option.

3. Infine, in una sessione di PowerShell, eseguire [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) e specificare il file che contiene le impostazioni esportate.

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restrizione: non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

Se è possibile concedere temporaneamente all'utente il ruolo Sysadmin per installare lo scanner, è possibile rimuovere questo ruolo al termine dell'installazione dello scanner. Quando si usa questa configurazione, il database viene creato automaticamente e all'account del servizio per lo scanner vengono concesse automaticamente le autorizzazioni necessarie. L'account utente che configura lo scanner richiede tuttavia il ruolo db_owner per il database di configurazione dello scanner ed è necessario concedere manualmente questo ruolo all'account utente.

If you cannot be granted the Sysadmin role even temporarily, you must ask a user with Sysadmin rights to manually create a database before you install the scanner. For this configuration, the following roles must be assigned:
    
|Account|Ruolo a livello database|
|--------------------------------|---------------------|
|Account del servizio per lo scanner|db_owner|
|Account utente per l'installazione dello scanner|db_owner|
|Account utente per la configurazione dello scanner |db_owner|

In genere, si usa lo stesso account utente per installare e configurare lo scanner, ma, se si usano account diversi, entrambi richiedono il ruolo db_owner per il database di configurazione dello scanner:

- If you do not specify your own profile name for the scanner (classic client only), the configuration database is named **AIPScanner_\<computer_name>** . 

- If you specify your own profile name, the configuration database is named **AIPScanner_\<profile_name>** (classic client) or **AIPScannerUL_\<profile_name>** (unified labeling client).

To create a user and grant db_owner rights on this database, ask the Sysadmin to run the following SQL script twice. The first time, for the service account that runs the scanner, and the second time for you to install and manage the scanner. Before running the script:
1. Replace *domain\user* with the domain name and user account name of the service account or user account.
2. Replace *DBName* with the name of the scanner configuration database.

SQL script:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

Inoltre:

- You must be a local administrator on the server that will run the scanner
- The service account that will run the scanner must be granted Full Control permissions to the following registry keys:
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

If, after configuring these permissions, you see an error when you install the scanner, the error can be ignored and you can manually start the scanner service.


#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restrizione: all'account del servizio per lo scanner non può essere concesso il diritto **Log on locally** (Accesso locale)

If your organization policies prohibit the **Log on locally** right for service accounts but allow the **Log on as a batch job** right, use the following instructions:

- For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.

- For the unified labeling client: Use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction: The scanner service account cannot be synchronized to Azure Active Directory but the server has internet connectivity

È possibile usare un account per eseguire il servizio dello scanner e un altro per l'autenticazione in Azure Active Directory:

- Per l'account del servizio dello scanner, è possibile usare un account Windows locale o un account Active Directory.

- For the Azure Active Directory account, use the following instructions:
    - For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    - For the unified labeling client: Specify your local account for the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.


## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurare lo scanner nel portale di Azure

Before you install the scanner, or upgrade it from an older general availability version of the scanner, create a profile for the scanner in the Azure portal. Si configura il profilo per le impostazioni dello scanner e per i repository di dati da analizzare.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al riquadro **Azure Information Protection**. 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Scanner** e selezionare **Profili**.

3. Nel riquadro **Azure Information Protection - Profili** selezionare **Aggiungi**:
    
    ![Aggiungere il profilo per lo scanner di Azure Information Protection](./media/scanner-add-profile.png)

4. Nel riquadro **Aggiungi un nuovo profilo** specificare un nome per lo scanner, usato per identificarne le impostazioni di configurazione e i repository di dati da analizzare. Ad esempio, è possibile specificare **Europa** per identificare la posizione geografica dei repository di dati che verranno analizzati dallo scanner. Quando in un secondo momento si installa o si aggiorna lo scanner, sarà necessario specificare lo stesso nome di profilo.
    
    Facoltativamente, specificare una descrizione per scopi amministrativi, per facilitare l'identificazione del nome di profilo dello scanner.

5. For this initial configuration, configure the following settings, and then select **Save** but do not close the pane:
    
    For the **Profile settings** section:
    - **Schedule**: Keep the default of **Manual**
    - **Info types to be discovered**: Change to **Policy only**
    - **Configure repositories**: Do not configure at this time because the profile must first be saved.
    
    For the **Policy enforcement** section:
    - **Enforce**: Select **Off**
    - **Label files based on content**: Keep the default of **On**
    - **Default label**: Keep the default of **Policy default**
    - **Relabel files**: Keep the default of **Off**
    
    For the **Configure file settings** section:
    - **Preserve "Date modified", "Last modified" and "Modified by"** : Keep the default of **On**
    - **File types to scan**: Keep the default file types for **Exclude**
    - **Default owner**: Keep the default of **Scanner Account**

6. Dopo aver creato e salvato il profilo, si è pronti per tornare all'opzione **Configura i repository** per specificare gli archivi dati da analizzare. You can specify local folders, UNC paths, and SharePoint Server URLs for SharePoint on-premises document libraries and folders. 
    
    SharePoint Server 2019, SharePoint Server 2016, and SharePoint Server 2013 are supported for SharePoint. Anche SharePoint Server 2010 è supportato quando è disponibile il [supporto "Extended" per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
    To add your first data store, still on the **Add a new profile** pane, select **Configure repositories** to open the **Repositories** pane:
    
    ![Configurare i repository di dati per lo scanner di Azure Information Protection](./media/scanner-repositories-bar.png)

7. Nel riquadro **Repository** selezionare **Aggiungi**:
    
    ![Aggiungere il repository di dati per lo scanner di Azure Information Protection](./media/scanner-repository-add.png)

8. On the **Repository** pane, specify the path for the data repository. 
    
    I caratteri jolly e i percorsi WebDav non sono supportati.
    
    Di seguito sono riportati alcuni esempi.
    
    - Per un percorso locale: `C:\Folder`
    
    - Per una condivisione di rete: `C:\Folder\Filename`
    
    - Per un percorso UNC: `\\Server\Folder`
    
    - Per una raccolta di SharePoint: `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > Se si aggiunge un percorso di SharePoint per "Documenti condivisi":
    >
     >- Specificare **Documenti condivisi** nel percorso quando si vogliono analizzare tutti i documenti e tutte le cartelle da Documenti condivisi. ad esempio `http://sp2013/Shared Documents`
     >
     >- Specificare **Documenti** nel percorso quando si vogliono analizzare tutti i documenti e tutte le cartelle da una sottocartella in Documenti condivisi. ad esempio `http://sp2013/Documents/Sales Reports`
    
    For the remaining settings on this pane, do not change them for this initial configuration, but keep them as **Profile default**. Questo significa che il repository dei dati eredita le impostazioni dal profilo dello scanner. 
    
    Selezionare **Salva**.

9. Se si vuole aggiungere un altro repository, ripetere i passaggi 7 e 8.

10. You can now close **Repositories** pane and your profile pane. Back on the **Azure Information Protection - Profiles** pane, you see your profile name displayed, together with the **SCHEDULE** column showing **Manual** and the **ENFORCE** column is blank.

A questo punto si è pronti per installare lo scanner con il profilo di scanner appena creato.

## <a name="install-the-scanner"></a>Installare lo scanner

1. Accedere al computer Windows Server che eseguirà lo scanner. Usare un account con diritti di amministratore locale e con le autorizzazioni per scrivere nel database master di SQL Server.

2. Aprire una sessione di Windows PowerShell con l'opzione **Esegui come amministratore**.

3. Eseguire il cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), che specifica l'istanza di SQL Server in cui creare un database per lo scanner di Azure Information Protection e il nome del profilo di scanner specificato nella sezione precedente: 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    Esempi, usando il nome di profilo **Europe**:
    
    - Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Quando richiesto, specificare le credenziali per l'account del servizio scanner (\<dominio\nome utente>) e la password.

4. Verificare che il servizio è ora installato usando **Strumenti di amministrazione** > **Servizi**. 
    
    Il servizio installato è denominato **Azure Information Protection Scanner** ed è configurato per essere eseguito usando l'account del servizio scanner creato.

Ora che è stato installato lo scanner, è necessario ottenere un token di Azure AD per l'account del servizio scanner da autenticare, in modo che lo scanner possa essere eseguito automaticamente. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Ottenere un token di Azure AD per lo scanner

The Azure AD token lets the scanner authenticate to the Azure Information Protection service.

1. Return to the Azure portal to create two Azure AD applications (just one Azure AD application for the scanner from the unified labeling client) that are needed to specify an access token for authentication. This token lets the scanner run non-interactively.
    
    To create these applications, follow the instructions in the admin guides for the relevant clients:
    
    - For the classic client: [How to label files non-interactively for Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)
    
    - For the unified labeling client: [How to label files non-interactively for Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. Dal computer Windows Server, se all'account del servizio scanner è stato concesso il diritto di **accesso locale** per l'installazione: accedere con questo account e avviare una sessione di PowerShell. Eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) specificando i valori copiati nel passaggio precedente:
    
    **For the classic client:**
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    Quando richiesto, specificare la password per le credenziali dell'account del servizio per Azure AD e quindi fare clic su **Accetto**.
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation see [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    
    **For the unified labeling client:**
    
    ```
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation, use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) from that client's admin guide.

The scanner now has a token to authenticate to Azure AD, which is valid for one year, two years, or never expires, according to your configuration of the **Web app /API** (classic client) or client secret (unified labeling client) in Azure AD. Quando il token scade, è necessario ripetere i passaggi 1 e 2.

Si è ora pronti per eseguire la prima analisi in modalità di individuazione.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner

1. In the Azure portal, on the **Azure Information Protection - Profiles** pane, select your scanner's profile, and then the **Scan now** option:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)
    
    In alternativa, nella sessione di PowerShell, eseguire il comando seguente:
    
        Start-AIPScan

2. Attendere che lo scanner completi il proprio ciclo. Quando lo scanner ha completato l'analisi per tutti i file negli archivi dati specificati, lo scanner viene arrestato anche se il servizio scanner rimane in esecuzione:
    
    - On the **Azure Information Protection - Profiles** pane, use the **Refresh** option and wait until you see values for the **LAST SCAN RESULTS** column and the **LAST SCAN (END TIME)** column.
    
    - Usando PowerShell è possibile eseguire `Get-AIPScannerStatus` per monitorare la modifica dello stato.
    
    - Scanner from the classic client only: Check the local Windows **Applications and Services** event log, **Azure Information Protection**. Questo registro indica anche quando lo scanner ha completato l'analisi, con un riepilogo dei risultati. Cercare l'ID evento informativo **911**.

3. Esaminare i report archiviati in %*localappdata*%\Microsoft\MSIP\Scanner\Reports. I file summary.txt includono il tempo impiegato per l'analisi, il numero di file analizzati e il numero di file con una corrispondenza per i tipi di informazioni. I file con estensione csv includono ulteriori dettagli per ogni file. In questa cartella vengono archiviati fino a 60 report per ogni ciclo di analisi e tutti i report tranne l'ultimo vengono compressi per ridurre al minimo lo spazio su disco necessario.
    
    > [!NOTE]
    > È possibile modificare il livello di registrazione usando il parametro *ReportLevel* con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration), ma non è possibile modificare il percorso della cartella o il nome del report. Valutare la possibilità di usare una giunzione di directory per la cartella, se si vogliono archiviare i report in un volume o una partizione diversi.
    >
    > Ad esempio, usando il comando [Mklink](/windows-server/administration/windows-commands/mklink): `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Con l'impostazione **Solo criteri** per **Tipi di informazioni da individuare**, solo i file che soddisfano le condizioni configurate per la classificazione automatica vengono inclusi nei report dettagliati. Se non si vedono etichette applicate, controllare che la configurazione delle etichette includa la classificazione automatica anziché consigliata.
    
    > [!TIP]
    > Gli scanner inviano queste informazioni ad Azure Information Protection ogni cinque minuti, in modo che sia possibile visualizzare i risultati quasi in tempo reale dal portale di Azure. Per altre informazioni, vedere [Reporting per Azure Information Protection](reports-aip.md). 
        
    If the results are not as you expect, you might need to reconfigure the conditions that you specified for you labels. In questo caso, ripetere i passaggi da 1 a 3 finché non si è pronti a modificare la configurazione per applicare la classificazione e, facoltativamente, la protezione. 

Il portale di Azure visualizza solo le informazioni sull'ultima analisi. Se è necessario visualizzare i risultati delle analisi precedenti, tornare ai report archiviati nel computer dello scanner, nella cartella %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quando si è pronti ad etichettare automaticamente i file individuati dallo scanner, passare alla procedura successiva. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurare lo scanner per applicare la classificazione e la protezione

Se si seguono queste istruzioni, lo scanner viene eseguito una volta e solo ai fini della creazione di report. Per modificare queste impostazioni, modificare il profilo dello scanner:

1. Back on the **Azure Information Protection - Profiles** pane, select the scanner profile to edit it.

2. On the \<**profile name**> pane, change the following two settings, and then select **Save**:
    
   - From the **Profile settings** section: Change the **Schedule** to **Always**
   - From the **Policy enforcement** section: Change **Enforce** to **On**
    
     Esistono altre impostazioni di configurazione che è opportuno modificare. Indicare ad esempio se gli attributi dei file vengono modificati e se lo scanner può rietichettare i file. Usare la Guida con informazioni popup per altre informazioni sulle singole impostazioni di configurazione.

3. Make a note of the current time and start the scanner again from the **Azure Information Protection - Profiles** pane:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)
    
    In alternativa, è possibile eseguire il comando seguente nella sessione di PowerShell:
    
        Start-AIPScan

4. Scanner from the classic client only: Monitor the event log for the informational type **911** again, with a time stamp later than when you started the scan in the previous step.
    
    Controllare quindi i report per visualizzare i dettagli dei file etichettati, la classificazione applicata a ogni file e se la protezione è stata applicata. In alternativa, usare il portale di Azure per visualizzare più facilmente queste informazioni.

Poiché la pianificazione è stata configurata in modo da essere eseguita continuamente, quando lo scanner ha completato l'analisi di tutti i file, avvia un nuovo ciclo automaticamente per individuare eventuali file nuovi e modificati.

## <a name="how-files-are-scanned"></a>Modalità di analisi dei file

Lo scanner esegue i processi seguenti per l'analisi di file.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determine whether files are included or excluded for scanning 
The scanner automatically skips files that are excluded from classification and protection, such as executable files and system files. For more information, see the following admin guides:

- For the classic client: [File types that are excluded from classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- For the unified labeling client: [File types that are excluded from classification and protection](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

È possibile modificare questo comportamento definendo un elenco di tipi di file da includere o escludere dall'analisi. È possibile specificare questo elenco da applicare a tutti i repository di dati per impostazione predefinita ed è possibile specificare un elenco per ogni repository dei dati. Per specificare questo elenco, usare l'impostazione **Tipi di file da analizzare** nel profilo dello scanner:

![Configurare i tipi di file da analizzare per lo scanner di Azure Information Protection](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Inspect and label files

Lo scanner usa quindi i filtri per l'analisi dei tipi di file supportati. Gli stessi filtri vengono usati dal sistema operativo per Windows Search e per l'indicizzazione. Windows IFilter viene usato senza alcuna configurazione aggiuntiva per l'analisi di file usati da Word, Excel e PowerPoint, nonché di documenti PDF e file di testo.

For a full list of file types that are supported by default, and additional information how to configure existing filters that include .zip files and .tiff files, see the following admin guides:

- For the classic client: [File types supported for inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)
- For the unified labeling client: [File types supported for inspection](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)

Dopo il controllo è possibile contrassegnare questi file mediante le condizioni specificate per le etichette. In alternativa, se si usa la modalità di individuazione, i file possono essere segnalati se contengono le condizioni specificate per le etichette o tutti i tipi di informazioni riservate noti. 

Tuttavia lo scanner non è in grado di contrassegnare i file nelle circostanze seguenti:

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Se l'etichetta applica classificazione e protezione, ma lo scanner non protegge il tipo di file.
    
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. Other file types can be protected when you [change which file types are protected](#change-which-file-types-to-protect) as described in a following section.

Ad esempio, dopo il controllo di file con estensione txt, lo scanner non può applicare un'etichetta configurata per la classificazione ma non per la protezione, perché il tipo di file con estensione txt non supporta la sola classificazione. If the label is configured for classification and protection, and the .txt file name extension is included for the scanner to protect, the scanner can label the file. 

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

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Se l'etichetta applica classificazione e protezione, ma lo scanner non protegge il tipo di file.
    
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. Other file types can be protected when you change which file types to protect, as described next.

## <a name="change-which-file-types-to-protect"></a>Change which file types to protect

By default, the scanner protects Office file types and PDF files only. You can change this behavior so that for example, the scanner protects all file types, which is the same protection behavior as the client. Or, the scanner protects additional file types that you specify, in addition to Office file types and PDF files. 

For configuration instructions, see the following sections.

### <a name="scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected"></a>Scanner from the classic client: Use the registry to change which file types are protected

This section applies to the scanner from the classic client only.

To change the default scanner behavior for protecting file types other than Office files and PDFs, you must edit the registry and specify the additional file types that you want to be protected, and the type of protection (native or generic). Per informazioni, vedere [Configurazione dell'API file](develop/file-api-configuration.md) nelle linee guida per sviluppatori. Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile". Inoltre, specificatamente per lo scanner:

- The scanner has its own default behavior: Only Office file formats and PDF documents are protected by default. Se il Registro di sistema non viene modificato, tutti gli altri tipi di file non verranno etichettati né protetti dallo scanner.

- If you want the same default protection behavior as the Azure Information Protection client, where all files are automatically protected with native or generic protection: Specify the `*` wildcard as a registry key, `Encryption` as the value (REG_SZ), and `Default` as the value data.

Quando si modifica il Registro di sistema, creare manualmente la chiave **MSIPC** e la chiave **FileProtection** se non esistono, nonché una chiave per ogni estensione del nome file.

Ad esempio, per fare in modo che lo scanner protegga le immagini TIFF oltre ai file di Office e ai file PDF, il Registro di sistema dopo la modifica avrà un aspetto simile all'immagine seguente. Dato che sono file immagine, i file con estensione tiff supportano la protezione nativa e l'estensione di file risultante è ptiff.

![Modifica del Registro di sistema per l'applicazione della protezione con lo scanner](./media/editregistry-scanner.png)

For a list of text and images file types that similarly support native protection but must be specified in the registry, see [Supported file types for classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

Per i file che non supportano la protezione nativa, specificare l'estensione del nome file come nuova chiave e **PFile** per la protezione generica. L'estensione del nome file risultante per il file protetto è pfile.

### <a name="scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected"></a>Scanner from the unified labeling client: Use PowerShell to change which file types are protected

This section applies to the scanner from the unified labeling client only.

For a label policy that applies to the user account downloading labels for the scanner, specify a PowerShell advanced setting named **PFileSupportedExtensions**. 

> [!NOTE]
> For a scanner that has access to the internet, this user account is the account that you specify for the *DelegatedUser* parameter with the Set-AIPAuthentication command.

Example 1:  PowerShell command for the scanner to protect all file types, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Example 2: PowerShell command for the scanner to protect .xml files and .tiff files in addition to Office files and PDF files, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}

For detailed instructions, see [Change which file types to protect](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) from the admin guide.


## <a name="when-files-are-rescanned"></a>Ripetizione dell'analisi dei file

Per il primo ciclo di analisi, lo scanner analizza tutti i file negli archivi dati configurati e quindi per le analisi successive, vengono controllati solo i file nuovi o modificati. 

You can force the scanner to inspect all files again from the **Azure Information Protection - Profiles** pane in the Azure portal. Select your scanner profile from the list, and then select the **Rescan all files** option:

![Avviare un'altra analisi per lo scanner di Azure Information Protection](./media/scanner-rescan-files2.png)

È utile verificare nuovamente i file quando si vuole che i report includano tutti i file e questa configurazione viene in genere usata quando lo scanner viene eseguito in modalità di individuazione. Al termine di un'analisi completa, il tipo di analisi diventa automaticamente incrementale in modo che per le analisi successive vengono analizzati solo i file nuovi o modificati.

In addition, all files are inspected when the scanner from the classic client downloads an Azure Information Protection policy that has new or changed conditions and the scanner from the unified labeling client has new or changed settings for automatic and recommended labeling. 

The scanner refreshes the policy according to the following triggers:

- Scanner from the classic client: Every hour and when the service starts and the policy is older than one hour. 

- Scanner from the unified labeling client: Every four hours and when the service starts. 

> [!TIP]
> If you need to refresh the policy sooner than the default interval, for example, during a testing period: 
>
> - Scanner from the classic client: Manually delete the policy file, **Policy.msip** from **%LocalAppData%\Microsoft\MSIP\Policy.msip**.
>
> - Scanner from the unified labeling client: Manually delete the contents from **%LocalAppData%\Microsoft\MSIP\mip\\<*processname*>\mip**.
>
Riavviare il servizio scanner di Azure Information Protection. If you changed protection settings for your labels, also wait 15 minutes from when you saved the protection settings before you restart the service.


## <a name="editing-in-bulk-for-the-data-repository-settings"></a>Modifica in blocco per le impostazioni dei repository di dati

Per i repository di dati aggiunti a un profilo dello scanner, è possibile usare le opzioni **Esporta** e **Importa** per modificare velocemente le impostazioni. Si supponga, ad esempio di volere aggiungere un nuovo tipo di file da escludere dall'analisi per i repository di dati di SharePoint.

Instead of editing each data repository in the Azure portal, use the **Export** option from the **Repositories** pane:

![Esportazione delle impostazioni del repository dei dati per lo scanner](./media/export-scanner-repositories.png)

Manually edit the file to make the change, and then use the **Import** option on the same pane.

## <a name="using-the-scanner-with-alternative-configurations"></a>Uso dello scanner con configurazioni alternative

There are three alternative scenarios that the Azure Information Protection scanner supports where labels do not need to be configured for any conditions: 

- Applicare un'etichetta predefinita a tutti i file in un repository di dati.
    
    For this configuration, set **Label files based on content** to **Off**. Then set the **Default label** to **Custom**, and select the label to use.
    
    The contents of the files are not inspected and all unlabeled files in the data repository are labeled according to the default label that you specify for the data repository or the scanner profile. 
    
    For the scanner from the unified labeling client, you can also select **Enforce default label** if you want the default label to be applied on all files, even if they are already labeled.
    

- Remove existing labels from all files in a data repository.
    
    Applicable to the scanner from the unified labeling client only, this configuration lets you remove existing labels, which includes protection if it was applied with that label. Protection that was applied independently from a label is retained. Use this configuration if you need to remove all labels from files in a repository.
    
    Configurare le impostazioni seguenti:
    - **Label files based on content**: **Off**
    - **Default label**: **None**
    - **Relabel files**: **On** with the **Enforce default label** checkbox selected

- Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.
    
    Per questa configurazione, impostare **Tipi di informazioni da individuare** su **Tutti**.
    
    For the scanner from the classic client: The scanner uses any custom conditions that you have specified for labels in the Azure Information Protection policy, and the list of information types that are available to specify for labels in the Azure Information Protection policy. 
    
    For the scanner from the unified labeling client: The scanner uses any custom sensitive info types that you have specified and the list of built-in sensitive info types that are available to select in your labeling management center.
    
    Questa impostazione consente di trovare le informazioni sensibili di cui si potrebbe non essere a conoscenza, a scapito però della velocità di analisi per lo scanner.
    
    The following quickstart for the scanner uses this configuration: [Quickstart: Find what sensitive information you have](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Ottimizzazione delle prestazioni dello scanner

Usare le linee guida seguenti per ottimizzare le prestazioni dello scanner. However, if your priority is the responsiveness of the scanner computer rather than the scanner performance, you can use an [advanced client setting](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) to limit the number of threads used by the scanner (classic client only).

Per ottimizzare le prestazioni dello scanner:

- **Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**
    
    Ad esempio, inserire il computer dello scanner nella stessa rete LAN o (scelta consigliata) nello stesso segmento di rete dell'archivio dei dati analizzati.
    
    La qualità della connessione di rete influisce sulle prestazioni dello scanner perché per controllare i file lo scanner trasferisce il contenuto dei file nel computer che esegue il servizio di analisi. Quando si riduce o si elimina il numero di hop di rete per i dati, si riduce anche il carico sulla rete. 

- **Verificare che il computer dello scanner abbia risorse del processore disponibili**
    
    La ricerca di una corrispondenza nel contenuto dei file e la crittografia e la decrittografia dei file sono operazioni che richiedono un uso intensivo del processore. Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se una mancanza di risorse del processore influisce negativamente sulle prestazioni dello scanner.
    
- **Non eseguire l'analisi delle cartelle locali nel computer che esegue il servizio di analisi**
    
    Se sono presenti cartelle da analizzare in un server di Windows, installare lo scanner in un computer diverso e configurare le cartelle come condivisioni di rete da analizzare. La separazione delle due funzioni di hosting dei file e di analisi dei file fa in modo che le risorse di elaborazione di questi servizi non siano in competizione tra loro.

Se necessario, installare più istanze dello scanner. Lo scanner di Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di profilo personalizzato per lo scanner. For the scanner from the unified labeling client, multiple scanners can share the same profile, which results in quicker scanning times.

Altri fattori che influenzano le prestazioni dello scanner:

- Carico corrente e tempi di risposta degli archivi dati che contengono i file da analizzare

- Esecuzione dello scanner in modalità di individuazione o applicazione
    
    La modalità di individuazione ha in genere una velocità di analisi maggiore rispetto alla modalità di applicazione poiché l'individuazione richiede una sola azione di lettura dei file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.

- You change the conditions in the Azure Information Protection policy (classic client) or auto-labeling in the label policy (unified labeling client)
    
    Il primo ciclo di analisi nel quale lo scanner deve analizzare ogni file richiede più tempo rispetto ai cicli di analisi successivi in cui, per impostazione predefinita, vengono analizzati solo i file nuovi e modificati. However, if you change the conditions or auto-labeling settings, all files are scanned again, as described in the [preceding section](#when-files-are-rescanned).

- La costruzione di espressioni regex per condizioni personalizzate
    
    Per evitare un consumo intenso di memoria e il rischio di timeout (15 minuti per ogni file), rivedere le espressioni regex per assicurarsi che usino criteri di ricerca efficienti. Ad esempio:
    
    - Evitare [quantificatori greedy](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - Usare gruppi di non acquisizione, ad esempio `(?:expression)` invece di `(expression)`

- Livello di registrazione selezionato
    
    È possibile scegliere tra **Debug**, **Info** (Informazioni), **Error** (Errore) e **Off** (Disattivato) per i report dello scanner. **Off** (Disattivato) offre le prestazioni migliori; **Debug** rallenta considerevolmente lo scanner ed è consigliabile usarlo solo per la ricerca e la risoluzione dei problemi. Per altre informazioni, vedere il parametro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- File:
    
    - With the exception of Excel files, Office files are more quickly scanned than PDF files.
    
    - I file non protetti sono più veloci da analizzare rispetto ai file protetti.
    
    - I file di grandi dimensioni richiedono più tempo per l'analisi rispetto ai file di piccole dimensioni.

- Inoltre:
    
    - Confirm that the service account that runs the scanner has only the rights documented in the [scanner prerequisites](#prerequisites-for-the-azure-information-protection-scanner) section, and then configure the [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) to disable the low integrity level for the scanner (classic client only).
    
    - L'esecuzione dello scanner è più rapida quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per applicare un'etichetta predefinita a tutti i file in quanto lo scanner non esamina i contenuti del file.
    
    - L'esecuzione dello scanner è più lenta quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.
    
    - You can decrease the scanner timeouts (classic client only) with [advanced client settings](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) for better scanning rates and lower memory consumption, but with the acknowledgment that some files might be skipped.

## <a name="list-of-cmdlets-for-the-scanner"></a>Elenco dei cmdlet per lo scanner

Dato che è ora possibile configurare lo scanner dal portale di Azure, i cmdlet di versioni precedenti usati per la configurazione dei repository di dati e l'elenco dei tipi di file analizzati sono deprecati. 

I cmdlet rimanenti includono i cmdlet per installare e aggiornare lo scanner, modificare il database di configurazione dello scanner e il profilo, modificare il livello di report locale e importare le impostazioni di configurazione per un computer disconnesso. 

The full list of cmdlets for the scanner: 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs) - unified labeling client only

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID registro eventi e descrizioni per lo scanner

Usare le sezioni seguenti per identificare gli ID evento e le descrizioni possibili per lo scanner. Gli eventi vengono registrati nel server su cui viene seguito il servizio scanner, nel registro eventi di **applicazioni e servizi** di Windows, **Azure Information Protection**.

> [!NOTE]
> This section applies to the scanner from the classic client only. Currently, the scanner from the unified labeling client doesn't write information to the event log.

-----

Informazione **910**

**Ciclo dello scanner avviato.**

Questo evento viene registrato quando il servizio scanner viene avviato e inizia a cercare i file negli archivi dati specificati.

----

Informazione **911**

**Ciclo dello scanner completato.**

Questo evento viene registrato quando lo scanner ha completato un'analisi manuale o un ciclo in caso di pianificazione continua.

Se lo scanner è stato configurato per l'esecuzione manuale anziché continuativa, per analizzare di nuovo i file impostare **Pianificazione** su **Manuale** o **Sempre** nel profilo dello scanner e quindi riavviare il servizio.

----

## <a name="next-steps"></a>Passaggi successivi

Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

Scoprire [Qual è la differenza tra Infrastruttura di classificazione file di Windows Server e lo scanner di Azure Information Protection](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner).

È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. For more information about this and other scenarios that use PowerShell, see the following sections from the admin guides:

- For the classic client: [Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)

- For the unified labeling client: [Using PowerShell with the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-powershell.md)
