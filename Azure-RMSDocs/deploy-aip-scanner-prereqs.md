---
title: Azure Information Protection (AIP) Unified Labeling Prerequisites scanner
description: Elenca i prerequisiti per l'installazione e la distribuzione di Azure Information Protection scanner unificato delle etichette.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cef1f6f80865f813e613e717ea301176f8fcc317
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049532"
---
# <a name="prerequisites-for-installing-and-deploying-the-azure-information-protection-unified-labeling-scanner"></a>Prerequisiti per l'installazione e la distribuzione di Azure Information Protection scanner unificato per l'assegnazione di etichette

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows Server 2012 R2*

>[!NOTE]
> Se si lavora con lo scanner classico, vedere [prerequisiti per l'installazione e la distribuzione del Azure Information Protection scanner classico](deploy-aip-scanner-prereqs-classic.md).

Prima di installare il Azure Information Protection scanner, verificare che il sistema soddisfi i requisiti seguenti:

- [Requisiti di Windows Server](#windows-server-requirements)
- [Requisiti dell'account del servizio](#service-account-requirements)
- [Requisiti di SQL Server](#sql-server-requirements)
- [Requisiti del client Azure Information Protection](#azure-information-protection-client-requirements)
- [Requisiti di configurazione delle etichette](#label-configuration-requirements)
- [Requisiti di SharePoint](#sharepoint-requirements)
- [Requisiti di Microsoft Office](#microsoft-office-requirements)
- [Requisiti del percorso del file](#file-path-requirements)
- [Requisiti statistici di utilizzo](#usage-statistics-requirements)

Se non è possibile soddisfare tutti i requisiti della tabella perché non sono consentiti dai criteri dell'organizzazione, vedere la sezione [configurazioni alternative](#deploying-the-scanner-with-alternative-configurations) .

Quando si distribuisce lo scanner in produzione o si verificano le prestazioni per più scanner, vedere [requisiti di archiviazione e pianificazione della capacità per SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

Quando si è pronti per iniziare l'installazione e la distribuzione dello scanner, continuare con [la distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](deploy-aip-scanner-configure-install.md).

## <a name="windows-server-requirements"></a>Requisiti di Windows Server

Per eseguire lo scanner, è necessario disporre di un computer Windows Server con le specifiche di sistema seguenti:

|Specifiche  |Dettagli  |
|---------|---------|
|**Processore**     |4 processori Core         |
|**RAM**     |8 GB         |
|**Spazio su disco**     |10 GB di spazio disponibile (media) per i file temporanei. </br></br>Lo scanner richiede spazio su disco sufficiente a creare i file temporanei per ogni file analizzato, quattro file per core. </br></br>Lo spazio su disco consigliato di 10 GB consente a 4 processori core di analizzare 16 file, ognuno con una dimensione di 625 MB.
|**Sistema operativo**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**Nota:** A scopo di test o valutazione in un ambiente non di produzione, è anche possibile usare qualsiasi sistema operativo Windows [supportato dal client Azure Information Protection](requirements.md#client-devices).
|**Connettività di rete**     | Il computer scanner può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare. </br></br> Se la connettività Internet non è possibile a causa dei criteri dell'organizzazione, vedere [Deploying the scanner with alternative Configurations](#deploying-the-scanner-with-alternative-configurations). </br></br>In caso contrario, verificare che il computer disponga di connettività Internet che consenta gli URL seguenti tramite HTTPS (porta 443):</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com <br />-  \*. protection.outlook.com |
| ||

## <a name="service-account-requirements"></a>Requisiti dell'account del servizio

È necessario disporre di un account del servizio per eseguire il servizio scanner nel computer Windows Server, nonché di eseguire l'autenticazione per Azure AD e scaricare i criteri di Azure Information Protection.

L'account del servizio deve essere un account di Active Directory e sincronizzato con Azure AD.

Se non è possibile sincronizzare questo account a causa dei criteri dell'organizzazione, vedere [Deploying the scanner with alternative Configurations](#deploying-the-scanner-with-alternative-configurations).

I requisiti di questo account del servizio sono i seguenti:

|Requisito  |Dettagli  |
|---------|---------|
|Assegnazione a destra dell'utente **di accesso locale**     |Necessario per installare e configurare lo scanner, ma non è necessario per eseguire le analisi.  </br></br>Una volta verificato che lo scanner è in grado di individuare, classificare e proteggere i file, è possibile rimuovere questo diritto dall'account del servizio.  </br></br>Se la concessione di questo diritto anche per un breve periodo di tempo non è possibile a causa dei criteri dell'organizzazione, vedere [distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).         |
|Assegnazione dei diritti utente per l'**accesso come servizio**.     |  Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner.        |
|**Autorizzazioni per i repository di dati**     |- **Condivisioni file o file locali:** Concedere le autorizzazioni di **lettura**, **scrittura**e **modifica** per analizzare i file e quindi applicare la classificazione e la protezione come configurata.  <br /><br />- **SharePoint:** Concedere le autorizzazioni di **controllo completo** per analizzare i file e quindi applicare la classificazione e la protezione come configurata.  <br /><br />- **Modalità di individuazione:** Per eseguire lo scanner solo in modalità di individuazione, è sufficiente l'autorizzazione di **lettura** .         |
|**Per le etichette che riproteggono o rimuovono la protezione**     | Per assicurarsi che lo scanner abbia sempre accesso ai file protetti, rendere questo account un [utente con privilegi avanzati](configure-super-users.md) per Azure Information Protection e assicurarsi che la funzionalità per utenti con privilegi avanzati sia abilitata. </br></br>Inoltre, se sono stati implementati i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione in più fasi, assicurarsi che l'account del servizio sia incluso nei controlli di onboarding configurati.|
| ||

## <a name="sql-server-requirements"></a>Requisiti di SQL Server

Per archiviare i dati di configurazione dello scanner, usare un'applicazione SQL Server con i requisiti seguenti:

- **Istanza locale o remota.**

    È consigliabile ospitare il servizio SQL Server e scanner in computer diversi, a meno che non si stia lavorando a una distribuzione di piccole dimensioni.

    SQL Server 2012 è la versione minima per le edizioni seguenti:

    - SQL Server Enterprise
    - SQL Server Standard
    - SQL Server Express (consigliato solo per gli ambienti di test)

- **Un account con ruolo sysadmin per installare lo scanner.**

    In questo modo, il processo di installazione crea automaticamente il database di configurazione dello scanner e concede il ruolo **db_owner** necessario all'account del servizio che esegue lo scanner.

    Se non è possibile concedere il ruolo sysadmin o i criteri dell'organizzazione richiedono che i database vengano creati e configurati manualmente, vedere [distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).

- **Capacità.** Per informazioni aggiuntive sulla capacità, vedere [requisiti di archiviazione e pianificazione della capacità per SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

- **[Regole di confronto senza distinzione tra maiuscole e minuscole](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15)**

> [!NOTE]
> Quando si specifica un nome di cluster personalizzato (profilo) per lo scanner oppure quando si usa la versione di anteprima dello scanner, sono supportati più database di configurazione nello stesso server SQL.
>
### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Requisiti di archiviazione e pianificazione della capacità per SQL Server

La quantità di spazio su disco necessaria per il database di configurazione dello scanner e la specifica del computer che esegue SQL Server possono variare per ogni ambiente, quindi si consiglia di eseguire i test personalizzati. Usare le linee guida seguenti come punto di partenza.

Per ulteriori informazioni, vedere [ottimizzazione delle prestazioni dello scanner](deploy-aip-scanner-configure-install.md#optimizing-scanner-performance).

Le dimensioni del disco per il database di configurazione dello scanner variano a seconda della distribuzione. Usare l'equazione seguente come linee guida:

```cli
100 KB + <file count> *(1000 + 4* <average file name length>)
```

Ad esempio, per analizzare 1 milione file con una lunghezza media del nome file di 250 byte, allocare 2 GB di spazio su disco.

Per più scanner:

- **Fino a 10 scanner,** usare:

    - 4 processori Core
    - 8 GB di RAM consigliata

- **Più di 10 scanner** (massimo 40), usare:
    - 8 processi principali
    - 16 GB di RAM consigliati

## <a name="azure-information-protection-client-requirements"></a>Requisiti del client Azure Information Protection

È necessario che sia disponibile la [versione di disponibilità generale corrente](./rms-client/unifiedlabelingclient-version-release-history.md) del client di Azure Information Protection installato nel computer Windows Server.

Per ulteriori informazioni, vedere la [Guida all'amministrazione client per l'assegnazione di etichette unificata](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner).

> [!IMPORTANT]
> È necessario installare il client completo per lo scanner. Non installare solo il modulo PowerShell del client.
>

## <a name="label-configuration-requirements"></a>Requisiti di configurazione delle etichette

È necessario che siano configurate le etichette che applicano automaticamente la classificazione e, facoltativamente, la protezione.

Se non sono state configurate queste etichette, vedere [distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).

Per altre informazioni, vedere:

- [Applicare automaticamente un'etichetta di riservatezza al contenuto](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [Limitare l'accesso al contenuto usando la crittografia nelle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)

## <a name="sharepoint-requirements"></a>Requisiti di SharePoint

Per analizzare le cartelle e le raccolte documenti di SharePoint, verificare che il server SharePoint soddisfi i requisiti seguenti:

- **Versioni supportate.** Le versioni supportate includono: SharePoint 2019, SharePoint 2016, SharePoint 2013 e SharePoint 2010. Altre versioni di SharePoint non sono supportate per lo scanner.

- **Versioning.** Quando si usa il [controllo delle versioni](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), lo scanner controlla ed etichetta l'ultima versione pubblicata. Se le etichette dello scanner sono obbligatorie per un file e l' [approvazione del contenuto](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) , è necessario approvare il file con etichetta in modo che sia disponibile per gli utenti.  

- **Farm di SharePoint di grandi dimensioni.** Per le farm SharePoint di grandi dimensioni, controllare se è necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000) per lo scanner al fine di accedere a tutti i file. Per ulteriori informazioni, vedere [gestire elenchi e librerie di grandi dimensioni in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

## <a name="microsoft-office-requirements"></a>Requisiti di Microsoft Office

Per analizzare i documenti di Office, i documenti devono essere in uno dei formati seguenti:

- Microsoft Office 97-2003
- Formati Office Open XML per Word, Excel e PowerPoint

Per altre informazioni, vedere [tipi di file supportati dal client di Azure Information Protection Unified Labeling](./rms-client/clientv2-admin-guide-file-types.md).

## <a name="file-path-requirements"></a>Requisiti del percorso del file

Per analizzare i file, i percorsi dei file devono avere un massimo di 260 caratteri, a meno che lo scanner non sia installato in Windows 2016 e che il computer sia configurato per supportare percorsi lunghi

Windows 10 e Windows Server 2016 supportano lunghezze di percorso maggiori di 260 caratteri con le seguenti impostazioni di [criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): Configurazione computer **criteri computer locale**  >  **Computer Configuration**  >  **modelli amministrativi**  >  **tutte le impostazioni**  >  **Abilita percorsi lunghi Win32**

Per altre informazioni sul supporto dei percorsi di file lunghi, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) nella documentazione per sviluppatori di Windows 10.

## <a name="usage-statistics-requirements"></a>Requisiti statistici di utilizzo

Disabilitare le statistiche di utilizzo usando uno dei metodi seguenti:

- Impostazione del parametro [AllowTelemetry](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-install#to-install-the-azure-information-protection-client-by-using-the-executable-installer) su 0

- Assicurarsi che l'opzione migliora Azure Information Protection inviando le **statistiche di utilizzo a Microsoft** rimanga deselezionata durante il processo di installazione dello scanner.

## <a name="deploying-the-scanner-with-alternative-configurations"></a>Distribuzione dello scanner con configurazioni alternative

I prerequisiti elencati sopra sono i requisiti predefiniti per la distribuzione dello scanner e sono consigliati perché supportano la configurazione dello scanner più semplice.

I requisiti predefiniti devono essere appropriati per i test iniziali, in modo da poter controllare le funzionalità dello scanner.

Tuttavia, in un ambiente di produzione, i criteri dell'organizzazione possono proibire questi requisiti predefiniti. Lo scanner è in grado di soddisfare le restrizioni seguenti con la configurazione aggiuntiva:

- [Il server scanner non può avere connettività Internet](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [Restrizione: l'account del servizio scanner non può essere sincronizzato con Azure Active Directory, ma il server ha connettività Internet](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [Restrizione: non è possibile concedere all'account di servizio per lo scanner il diritto di **accesso locale**](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [Restrizione: non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restrizione: il server scanner non può avere connettività Internet

Per supportare un computer disconnesso, seguire questa procedura:

1. Configurare le etichette nei criteri e quindi importare i criteri usando il cmdlet [Import-AIPScannerConfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration?view=azureipps) . Sebbene il client di etichettatura unificata non possa applicare la protezione senza una connessione Internet, lo scanner può comunque applicare le etichette in base ai criteri importati.

1. Configurare lo scanner nella portale di Azure creando un cluster dello scanner. Se occorre assistenza per questo passaggio, vedere [Configurare lo scanner nel portale di Azure](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

1. Esportare il processo del contenuto dal riquadro **processi di analisi Azure Information Protection-contenuto** utilizzando l'opzione **Esporta** .

1. In una sessione di PowerShell eseguire [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) e specificare il file che contiene le impostazioni esportate.

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restrizione: non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

Se è possibile concedere *temporaneamente* il ruolo sysadmin per installare lo scanner, è possibile rimuovere questo ruolo quando l'installazione dello scanner è stata completata.

Eseguire una delle operazioni seguenti, a seconda dei requisiti dell'organizzazione:

- **È possibile avere temporaneamente il ruolo sysadmin.** Se si dispone temporaneamente del ruolo sysadmin, il database viene creato automaticamente e all'account di servizio per lo scanner vengono concesse automaticamente le autorizzazioni necessarie.

    Tuttavia, l'account utente che configura lo scanner richiede ancora il ruolo **db_owner** per il database di configurazione dello scanner. Se si ha il ruolo sysadmin solo fino al completamento dell'installazione dello scanner, [concedere manualmente il ruolo db_owner all'account utente](#create-a-user-and-grant-db_owner-rights-manually).

- **Non è possibile avere il ruolo sysadmin**. Se non è possibile concedere il ruolo sysadmin anche temporaneamente, è necessario richiedere un utente con diritti sysadmin per creare manualmente un database prima di installare lo scanner.

    Per questa configurazione, è necessario assegnare il ruolo **db_owner** ai seguenti account:

    - Account del servizio per lo scanner
    - Account utente per l'installazione dello scanner
    - Account utente per la configurazione dello scanner

    In genere, si usa lo stesso account utente per installare e configurare lo scanner, Se si usano account diversi, entrambi richiedono il ruolo db_owner per il database di configurazione dello scanner. Creare l'utente e i diritti in base alle esigenze. Se si specifica il nome del cluster (profilo), il database di configurazione viene denominato **AIPScannerUL_<cluster_name>**.

Inoltre:

- È necessario essere un amministratore locale nel server che eseguirà lo scanner
- All'account del servizio che eseguirà lo scanner devono essere concesse le autorizzazioni controllo completo per le chiavi del registro di sistema seguenti:

    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

Se, dopo aver configurato queste autorizzazioni, viene visualizzato un errore durante l'installazione dello scanner, l'errore può essere ignorato ed è possibile avviare manualmente il servizio scanner.

#### <a name="populate-the-database-manually"></a>Popolamento manuale del database

Popolare il database utilizzando lo script seguente:

```cli
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END 
```

#### <a name="create-a-user-and-grant-db_owner-rights-manually"></a>Creare un utente e concedere i diritti di db_owner manualmente

Per creare un utente e concedere diritti di db_owner per il database, rivolgersi al sysadmin per eseguire le operazioni seguenti:

1. Creare un database per lo scanner:

    ```cli
    **CREATE DATABASE AIPScannerUL_[clustername]**

    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```

2. Concedere i diritti all'utente che esegue il comando di installazione e viene usato per eseguire i comandi di gestione dello scanner.

    Script SQL:

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. Concedere i diritti per l'account del servizio scanner.

    Script SQL:
    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restrizione: all'account del servizio per lo scanner non può essere concesso il diritto **Log on locally** (Accesso locale)

Se i criteri dell'organizzazione proibiscono il diritto di **accesso locale** per gli account del servizio, ma consentono il diritto **di accesso come processo batch** , usare il parametro *OnBehalfOf* con set-AIPAuthentication.

Per ulteriori informazioni, vedere [come etichettare i file in modo non interattivo per Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restrizione: l'account del servizio scanner non può essere sincronizzato con Azure Active Directory, ma il server ha connettività Internet

È possibile usare un account per eseguire il servizio dello scanner e un altro per l'autenticazione in Azure Active Directory:

- **Per l'account del servizio scanner,** utilizzare un account di Windows locale o un account Active Directory.

- **Per l'account Azure Active Directory,** specificare l'account locale per il parametro *OnBehalfOf* con set-AIPAuthentication. Per ulteriori informazioni, vedere [come etichettare i file in modo non interattivo per Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver verificato che il sistema è conforme ai prerequisiti dello scanner, continuare con [la distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](deploy-aip-scanner-configure-install.md).

Per una panoramica sullo scanner, vedere [Deploying the Azure Information Protection scanner to classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

**Ulteriori informazioni:**

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari in cui viene usato PowerShell, vedere [uso di PowerShell con il Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md).
