---
title: Azure Information Protection (AIP) Unified Labeling Prerequisites scanner
description: Elenca i prerequisiti per l'installazione e la distribuzione di Azure Information Protection scanner unificato delle etichette.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/27/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4e8c4444aad6185b54a6f5b5178fa225857b71d2
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414957"
---
# <a name="requirements-for-installing-and-deploying-the-azure-information-protection-unified-labeling-scanner"></a>Requisiti per l'installazione e la distribuzione del Azure Information Protection scanner per l'assegnazione di etichette unificata

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Pertinente per**: [AIP Unified Labeling client only](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere [prerequisiti di scanner client classici](deploy-aip-scanner-prereqs-classic.md)*

Prima di installare lo scanner locale Azure Information Protection, assicurarsi che il sistema sia conforme ai requisiti di [Azure Information Protection](requirements.md)di base.

Inoltre, i requisiti seguenti sono specifici per lo scanner:

- [Requisiti di Windows Server](#windows-server-requirements)
- [Requisiti dell'account del servizio](#service-account-requirements)
- [Requisiti di SQL Server](#sql-server-requirements)
- [Requisiti per il client di Azure Information Protection](#azure-information-protection-client-requirements)
- [Requisiti di configurazione delle etichette](#label-configuration-requirements)
- [Requisiti di SharePoint](#sharepoint-requirements)
- [Requisiti di Microsoft Office](#microsoft-office-requirements)
- [Requisiti del percorso del file](#file-path-requirements)

Se non è possibile soddisfare tutti i requisiti elencati per lo scanner perché non sono consentiti dai criteri dell'organizzazione, vedere la sezione [configurazioni alternative](#deploying-the-scanner-with-alternative-configurations) .

Quando si distribuisce lo scanner in produzione o si verificano le prestazioni per più scanner, vedere [requisiti di archiviazione e pianificazione della capacità per SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

Quando si è pronti per iniziare l'installazione e la distribuzione dello scanner, continuare con [la distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](deploy-aip-scanner-configure-install.md).

## <a name="windows-server-requirements"></a>Requisiti di Windows Server

Per eseguire lo scanner, è necessario disporre di un computer Windows Server con le specifiche di sistema seguenti:

|Specifiche  |Dettagli  |
|---------|---------|
|**Processore**     |4 processori Core         |
|**RAM**     |8 GB         |
|**Spazio su disco**     |10 GB di spazio disponibile (media) per i file temporanei. </br></br>Lo scanner richiede spazio su disco sufficiente a creare i file temporanei per ogni file analizzato, quattro file per core. </br></br>Lo spazio su disco consigliato di 10 GB consente a 4 processori core di analizzare 16 file, ognuno con una dimensione di 625 MB.
|**Sistema operativo**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**Nota**: a scopo di test o valutazione in un ambiente non di produzione, è anche possibile usare qualsiasi sistema operativo Windows [supportato dal client Azure Information Protection](requirements.md#client-devices).
|**Connettività di rete**     | Il computer scanner può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare. </br></br> Se la connettività Internet non è possibile a causa dei criteri dell'organizzazione, vedere [Deploying the scanner with alternative Configurations](#deploying-the-scanner-with-alternative-configurations). </br></br>In caso contrario, verificare che il computer disponga di connettività Internet che consenta gli URL seguenti tramite HTTPS (porta 443):</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com <br />-  \*. protection.outlook.com |
|**Condivisioni NFS** |Per supportare le analisi sulle condivisioni NFS, i servizi per NFS devono essere distribuiti nel computer dello scanner. <br><br>Nel computer passare alla finestra di dialogo Impostazioni **funzionalità Windows (attiva o disattiva funzionalità Windows)** e selezionare gli elementi seguenti: **Servizi per**  >  **strumenti di amministrazione** NFS e **client per NFS**. |
| | |

## <a name="service-account-requirements"></a>Requisiti dell'account del servizio

È necessario disporre di un account del servizio per eseguire il servizio scanner nel computer Windows Server, nonché di eseguire l'autenticazione per Azure AD e scaricare i criteri di Azure Information Protection.

L'account del servizio deve essere un account di Active Directory e sincronizzato con Azure AD.

Se non è possibile sincronizzare questo account a causa dei criteri dell'organizzazione, vedere [Deploying the scanner with alternative Configurations](#deploying-the-scanner-with-alternative-configurations).

I requisiti di questo account del servizio sono i seguenti:

|Requisito  |Dettagli  |
|---------|---------|
|Assegnazione a destra dell'utente **di accesso locale**     |Necessario per installare e configurare lo scanner, ma non è necessario per eseguire le analisi.  </br></br>Una volta verificato che lo scanner è in grado di individuare, classificare e proteggere i file, è possibile rimuovere questo diritto dall'account del servizio.  </br></br>Se la concessione di questo diritto anche per un breve periodo di tempo non è possibile a causa dei criteri dell'organizzazione, vedere [distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).         |
|Assegnazione dei diritti utente per l'**accesso come servizio**.     |  Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner.        |
|**Autorizzazioni per i repository di dati**     |- **Condivisioni file o file locali**: concedere le autorizzazioni di **lettura**, **scrittura** e **modifica** per la scansione dei file e quindi l'applicazione della classificazione e della protezione come configurato.  <br /><br />- **SharePoint**: è necessario concedere le autorizzazioni di **controllo completo** per analizzare i file e quindi applicare la classificazione e la protezione ai file che soddisfano le condizioni nei criteri di Azure Information Protection.  <br /><br />- **Modalità di individuazione**: per eseguire lo scanner solo in modalità di individuazione, è sufficiente l'autorizzazione di **lettura** .         |
|**Per le etichette che riproteggono o rimuovono la protezione**     | Per assicurarsi che lo scanner abbia sempre accesso ai file protetti, rendere questo account un [utente con privilegi avanzati](configure-super-users.md) per Azure Information Protection e assicurarsi che la funzionalità per utenti con privilegi avanzati sia abilitata. </br></br>Inoltre, se sono stati implementati i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione in più fasi, assicurarsi che l'account del servizio sia incluso nei controlli di onboarding configurati.|
|**Analisi specifica a livello di URL**: |Per analizzare e individuare siti e siti secondari [in un URL specifico](#deploying-the-scanner-with-alternative-configurations), concedere all' **agente di raccolta siti** i diritti per l'account scanner a livello di farm.|
| | |

## <a name="sql-server-requirements"></a>Requisiti di SQL Server

Per archiviare i dati di configurazione dello scanner, usare un'applicazione SQL Server con i requisiti seguenti:

- **Istanza locale o remota.**

    Si consiglia di ospitare SQL Server e il servizio scanner in computer diversi, a meno che non si stia lavorando a una distribuzione di piccole dimensioni. Inoltre, è consigliabile disporre di un'istanza di SQL dedicata che funge solo da database scanner e che non sia condivisa con altre applicazioni.

    Se si lavora su un server condiviso, verificare che il [numero consigliato di core](#windows-server-requirements) siano gratuiti per il funzionamento del database dello scanner.

    SQL Server 2016 è la versione minima per le edizioni seguenti:

    - SQL Server Enterprise

    - SQL Server Standard

    - SQL Server Express (consigliato solo per gli ambienti di test)

- **Un account con ruolo sysadmin per installare lo scanner.**

    Il ruolo sysadmin consente al processo di installazione di creare automaticamente il database di configurazione dello scanner e concedere al ruolo **db_owner** necessario l'account del servizio che esegue lo scanner.

    Se non è possibile concedere il ruolo sysadmin o i criteri dell'organizzazione richiedono che i database vengano creati e configurati manualmente, vedere [distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).

- **Capacità.** Per informazioni aggiuntive sulla capacità, vedere [requisiti di archiviazione e pianificazione della capacità per SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

- **[Regole di confronto senza distinzione tra maiuscole](/sql/relational-databases/collations/collation-and-unicode-support)e minuscole.**

> [!NOTE]
> Quando si specifica un nome di cluster personalizzato per lo scanner oppure quando si usa la versione di anteprima dello scanner, sono supportati più database di configurazione nello stesso server SQL.
>
### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Requisiti di archiviazione e pianificazione della capacità per SQL Server

La quantità di spazio su disco necessaria per il database di configurazione dello scanner e la specifica del computer che esegue SQL Server possono variare per ogni ambiente, quindi si consiglia di eseguire i test personalizzati. Usare le linee guida seguenti come punto di partenza.

Per ulteriori informazioni, vedere [ottimizzazione delle prestazioni dello scanner](deploy-aip-scanner-configure-install.md#optimize-scanner-performance).

Le dimensioni del disco per il database di configurazione dello scanner variano a seconda della distribuzione. Usare l'equazione seguente come linee guida:

```cli
100 KB + <file count> *(1000 + 4* <average file name length>)
```

Ad esempio, per analizzare 1 milione file con una lunghezza media del nome file di 250 byte, allocare 2 GB di spazio su disco.

Per più scanner:

- **Fino a 10 scanner**, usare:

    - 4 processori Core
    - 8 GB di RAM consigliata

- **Più di 10 scanner** (massimo 40), usare:
    - 8 processi principali
    - 16 GB di RAM consigliati

## <a name="azure-information-protection-client-requirements"></a>Requisiti per il client di Azure Information Protection

È necessario che sia disponibile la [versione di disponibilità generale corrente](./rms-client/unifiedlabelingclient-version-release-history.md) del client di Azure Information Protection installato nel computer Windows Server.

Per ulteriori informazioni, vedere la [Guida all'amministrazione client per l'assegnazione di etichette unificata](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner).

> [!IMPORTANT]
> È necessario installare il client completo per lo scanner. Non installare solo il modulo PowerShell del client.
>

## <a name="label-configuration-requirements"></a>Requisiti di configurazione delle etichette

Per applicare la classificazione e, facoltativamente, la protezione, è necessario che sia configurata almeno un'etichetta di riservatezza in uno dei Microsoft 365 l'assegnazione di etichette ai centri di amministrazione per l'account dello scanner.

Microsoft 365 l'assegnazione di etichette ai centri di amministrazione includono il Centro sicurezza Microsoft 365, il centro di conformità Microsoft 365 e il Microsoft 365 Centro sicurezza e conformità. 

L' *account dello scanner* è l'account che verrà specificato nel parametro **DelegatedUser** del cmdlet [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) , eseguito quando si configura lo scanner. 

Se le etichette non hanno condizioni di etichetta automatica, vedere le [istruzioni per le configurazioni alternative](#restriction-your-labels-do-not-have-auto-labeling-conditions) riportate di seguito.

Per altre informazioni, vedere:

- [Informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels)
- [Applicare automaticamente un'etichetta di riservatezza al contenuto](/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [Limitare l'accesso al contenuto usando la crittografia nelle etichette di riservatezza](/microsoft-365/compliance/encryption-sensitivity-labels)
- [Configurazione e installazione dello scanner di Azure Information Protection Unified Labeling](deploy-aip-scanner-configure-install.md)

## <a name="sharepoint-requirements"></a>Requisiti di SharePoint

Per analizzare le cartelle e le raccolte documenti di SharePoint, verificare che il server SharePoint soddisfi i requisiti seguenti:

|Requisito  |Descrizione  |
|---------|---------|
|**Versioni supportate** | Le versioni supportate includono: SharePoint 2019, SharePoint 2016 e SharePoint 2013. <br> Altre versioni di SharePoint non sono supportate per lo scanner.     |
|**Controllo delle versioni**     |  Quando si usa il [controllo delle versioni](/sharepoint/governance/versioning-content-approval-and-check-out-planning), lo scanner controlla ed etichetta l'ultima versione pubblicata. <br><br>Se le etichette dello scanner sono obbligatorie per un file e l' [approvazione del contenuto](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) , è necessario approvare il file con etichetta in modo che sia disponibile per gli utenti.       |
|**Farm di SharePoint di grandi dimensioni** |Per le farm SharePoint di grandi dimensioni, controllare se è necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000) per lo scanner al fine di accedere a tutti i file. <br><br>Per ulteriori informazioni, vedere [gestire elenchi e librerie di grandi dimensioni in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server). |
|**Percorsi di file lunghi**  |Se si dispone di percorsi di file lunghi in SharePoint, verificare che il valore [httpRuntime. maxUrlLength](/dotnet/api/system.web.configuration.httpruntimesection.maxurllength) del server SharePoint sia maggiore di quello predefinito di 260 caratteri. <br><br>Per altre informazioni, vedere [evitare i timeout dello scanner in SharePoint](rms-client/clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint). | 
| | |

## <a name="microsoft-office-requirements"></a>Requisiti di Microsoft Office

Per analizzare i documenti di Office, i documenti devono essere in uno dei formati seguenti:

- Microsoft Office 97-2003
- Formati Office Open XML per Word, Excel e PowerPoint

Per altre informazioni, vedere [tipi di file supportati dal client di Azure Information Protection Unified Labeling](./rms-client/clientv2-admin-guide-file-types.md).

## <a name="file-path-requirements"></a>Requisiti del percorso del file

Per impostazione predefinita, per analizzare i file, i percorsi dei file devono avere un massimo di 260 caratteri.

Per analizzare i file con percorsi di file di più di 260 caratteri, installare lo scanner in un computer con una delle seguenti versioni di Windows e configurare il computer in base alle esigenze:

|Versione di Windows  |Descrizione  |
|---------|---------|
|**Windows 2016 o versione successiva**     |   Configurare il computer per supportare percorsi lunghi      |
|**Windows 10 o Windows Server 2016**     | Definire la seguente [impostazione di criteri di gruppo](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10): Configurazione computer **criteri computer locale**  >    >  **modelli amministrativi**  >  **tutte le impostazioni**  >  **Abilita percorsi lunghi Win32**.    </br></br>Per ulteriori informazioni sul supporto dei percorsi di file lunghi in queste versioni, vedere la sezione [limitazione della lunghezza massima del percorso](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dalla documentazione per gli sviluppatori di Windows 10.    |
|**Windows 10, versione 1607 o successiva**     |  Acconsentire esplicitamente alla funzionalità di **MAX_PATH** aggiornata. Per ulteriori informazioni, vedere [Enable Long paths in Windows 10 versioni 1607 e versioni successive](/windows/win32/fileio/naming-a-file#enable-long-paths-in-windows-10-version-1607-and-later).      |
| | |


## <a name="deploying-the-scanner-with-alternative-configurations"></a>Distribuzione dello scanner con configurazioni alternative

I prerequisiti elencati sopra sono i requisiti predefiniti per la distribuzione dello scanner e sono consigliati perché supportano la configurazione dello scanner più semplice.

I requisiti predefiniti devono essere appropriati per i test iniziali, in modo da poter controllare le funzionalità dello scanner.

Tuttavia, in un ambiente di produzione, i criteri dell'organizzazione possono essere diversi dai requisiti predefiniti. Lo scanner è in grado di supportare le seguenti modifiche con la configurazione aggiuntiva:

- [Individuare e analizzare tutti i siti e i siti secondari in un URL specifico](#discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url)

- [Restrizione: il server scanner non può avere connettività Internet](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [Restrizione: l'account del servizio scanner non può essere sincronizzato con Azure Active Directory, ma il server ha connettività Internet](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [Restrizione: non è possibile concedere all'account di servizio per lo scanner il diritto di **accesso locale**](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [Restrizione: non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

- [Restrizione: le etichette non hanno condizioni di etichetta automatica](#restriction-your-labels-do-not-have-auto-labeling-conditions)

### <a name="discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url"></a>Individuare e analizzare tutti i siti e i siti Web di SharePoint in un URL specifico

Lo scanner è in grado di individuare e analizzare tutti i siti e i siti Web di SharePoint in un URL specifico con la seguente configurazione:

1. Avviare **Amministrazione centrale SharePoint**.

1. Nel sito Web **Amministrazione centrale SharePoint** , nella sezione **Gestione applicazioni** , fare clic su **Gestisci applicazioni Web**.

1. Fare clic per evidenziare l'applicazione Web di cui si desidera gestire il livello di criteri di autorizzazione.

1. Scegliere la farm pertinente e quindi selezionare **Gestisci livelli di criteri autorizzazioni**.

1. Selezionare **site collection auditor** nelle opzioni delle autorizzazioni per la **raccolta siti** , quindi concedere la **visualizzazione delle pagine dell'applicazione** nell'elenco delle autorizzazioni e infine assegnare un nome al nuovo **Auditor e al visualizzatore della raccolta siti** del livello di criteri AIP scanner.

1. Aggiungere l'utente dello scanner al nuovo criterio e concedere la **raccolta siti** nell'elenco delle autorizzazioni.   

1. Aggiungere un URL di SharePoint che ospita siti o siti secondari che devono essere analizzati. Per altre informazioni, vedere [configurare lo scanner nella portale di Azure](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

Per ulteriori informazioni sulla gestione dei livelli di criteri di SharePoint, vedere [gestire i criteri di autorizzazione per un'applicazione Web](/sharepoint/administration/manage-permission-policies-for-a-web-application).

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restrizione: il server scanner non può avere connettività Internet

Sebbene il client di etichettatura unificata non possa applicare la protezione senza una connessione Internet, lo scanner può comunque applicare le etichette in base ai criteri importati.

Per supportare un computer disconnesso, utilizzare uno dei metodi seguenti:

- [Usa la portale di Azure](#use-the-azure-portal-with-a-disconnected-computer) (scelta consigliata quando possibile)

- [Usare PowerShell](#use-powershell-with-a-disconnected-computer)

#### <a name="use-the-azure-portal-with-a-disconnected-computer"></a>Usare il portale di Azure con un computer disconnesso

Per supportare un computer disconnesso dalla portale di Azure, seguire questa procedura:

1.  Configurare le etichette nei criteri e quindi usare la [procedura per supportare i computer disconnessi](rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers) per abilitare la classificazione e l'assegnazione di etichette offline.

1. Abilitare la gestione offline per i processi di analisi del contenuto e di rete come segue:

    **Abilitare la gestione offline per i processi di analisi del contenuto**:

    1. Impostare lo scanner per il funzionamento in modalità **offline** , usando il cmdlet [set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) .

    1. Configurare lo scanner nella portale di Azure creando un cluster dello scanner. Per altre informazioni, vedere [configurare lo scanner nella portale di Azure](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

    1. Esportare il processo del contenuto dal riquadro **processi di analisi Azure Information Protection-contenuto** utilizzando l'opzione **Esporta** .
    
    1. Importare i criteri usando il cmdlet [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/import-aipscannerconfiguration) . 
    
    I risultati per i processi di analisi del contenuto offline sono disponibili all'indirizzo: **%LocalAppData%\Microsoft\MSIP\Scanner\Reports**
    
    **Abilitare la gestione offline dei processi di analisi di rete**:

    1. Impostare il servizio di individuazione della rete (anteprima pubblica) per il funzionamento in modalità offline usando il cmdlet [set-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/set-mipnetworkdiscoveryconfiguration) .

    1. Configurare il processo di analisi di rete nel portale di Azure. Per ulteriori informazioni, vedere [creazione di un processo di analisi di rete](deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview).
    
    1. Esportare il processo di analisi della rete dal riquadro processi di analisi di **rete Azure Information Protection (anteprima)** con l'opzione di **esportazione** . 
    
    1.  Importare il processo di analisi di rete usando il file che corrisponde al nome del cluster usando il cmdlet [Import-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/import-mipnetworkdiscoveryconfiguration) .  
    
    I risultati per i processi di analisi di rete offline sono disponibili in: **%LocalAppData%\Microsoft\MSIP\Scanner\Reports**

#### <a name="use-powershell-with-a-disconnected-computer"></a>Usare PowerShell con un computer disconnesso

Eseguire la procedura seguente per supportare un computer disconnesso usando solo PowerShell.

> [!IMPORTANT]
> Per gestire i processi di analisi dei contenuti è *necessario* che gli amministratori dei [server dello scanner 21ViaNet di Azure Cina](/microsoft-365/admin/services-in-china/parity-between-azure-information-protection#manage-azure-information-protection-content-scan-jobs) usino questa procedura.
> 

**Gestire i processi di analisi del contenuto solo usando PowerShell**:

1. Impostare lo scanner per il funzionamento in modalità **offline** , usando il cmdlet [set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) .

1. Creare un nuovo processo di analisi del contenuto utilizzando il cmdlet [set-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob) , assicurandosi di utilizzare il `-Enforce On` parametro obbligatorio.

1. Aggiungere i repository usando il cmdlet [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/add-aipscannerrepository) , con il percorso del repository che si vuole aggiungere.

    > [!TIP]
    > Per impedire che il repository erediti le impostazioni dal processo di analisi del contenuto, aggiungere il `OverrideContentScanJob On` parametro e i valori per le impostazioni aggiuntive.
    >
    > Per modificare i dettagli di un repository esistente, usare il comando [set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository) .
    >
 
1. Usare i cmdlet [Get-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob) e [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/get-aipscannerrepository) per restituire informazioni sulle impostazioni correnti del processo di analisi del contenuto. 

1. Usare il comando [set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository) per aggiornare i dettagli per un repository esistente.

1. Eseguire immediatamente il processo di analisi del contenuto, se necessario, usando il cmdlet [Start-AIPScan](/powershell/module/azureinformationprotection/start-aipscan) . 

    I risultati per i processi di analisi del contenuto offline sono disponibili all'indirizzo: **%LocalAppData%\Microsoft\MSIP\Scanner\Reports**

1. Se è necessario rimuovere un repository o un intero processo di analisi del contenuto, usare i cmdlet seguenti:

    - [Remove-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)
    - [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restrizione: non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

Utilizzare le procedure seguenti per creare manualmente i database e concedere il ruolo **db_owner** , in base alle esigenze.

- [Procedura per il database scanner](#manually-create-a-database-and-user-for-the-scanner-and-grant-db_owner-rights)
- [Procedura per il database di individuazione della rete](#manually-create-a-database-and-user-for-the-network-discovery-service-and-grant-db_owner-rights)

Se è possibile concedere *temporaneamente* il ruolo sysadmin per installare lo scanner, è possibile rimuovere questo ruolo quando l'installazione dello scanner è stata completata.

Eseguire una delle operazioni seguenti, a seconda dei requisiti dell'organizzazione:

|Restrizione  |Descrizione  |
|---------|---------|
|**È possibile avere temporaneamente il ruolo sysadmin**     |  Se si dispone temporaneamente del ruolo sysadmin, il database viene creato automaticamente e all'account di servizio per lo scanner vengono concesse automaticamente le autorizzazioni necessarie. <br><br>Tuttavia, l'account utente che configura lo scanner richiede ancora il ruolo **db_owner** per il database di configurazione dello scanner. Se si ha il ruolo sysadmin solo fino al completamento dell'installazione dello scanner, concedere manualmente il ruolo **db_owner** all'account utente.       |
|**Non è possibile avere il ruolo sysadmin**     |  Se non è possibile concedere il ruolo sysadmin anche temporaneamente, è necessario richiedere un utente con diritti sysadmin per creare manualmente un database prima di installare lo scanner. <br><br>Per questa configurazione, è necessario assegnare il ruolo **db_owner** ai seguenti account: <br>-Account del servizio per lo scanner<br>-Account utente per l'installazione dello scanner<br>-Account utente per la configurazione dello scanner <br><br>In genere, si usa lo stesso account utente per installare e configurare lo scanner, Se si usano account diversi, entrambi richiedono il ruolo **db_owner** per il database di configurazione dello scanner. Creare l'utente e i diritti in base alle esigenze. Se si specifica il nome del proprio cluster, il database di configurazione viene denominato **AIPScannerUL_<cluster_name>**.  |
| | |

Inoltre:

- È necessario essere un amministratore locale nel server che eseguirà lo scanner
- All'account del servizio che eseguirà lo scanner devono essere concesse le autorizzazioni controllo completo per le chiavi del registro di sistema seguenti:

    - `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server`
    - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server`

Se, dopo aver configurato queste autorizzazioni, viene visualizzato un errore durante l'installazione dello scanner, l'errore può essere ignorato ed è possibile avviare manualmente il servizio scanner.

#### <a name="manually-create-a-database-and-user-for-the-scanner-and-grant-db_owner-rights"></a>Creazione manuale di un database e di un utente per lo scanner e concessione dei diritti db_owner

Se è necessario creare manualmente il database dello scanner e/o creare un utente e concedere diritti di **db_owner** per il database, richiedere all'amministratore di sistema di eseguire i passaggi seguenti:

1. Creare un database per lo scanner:

    ```sql
    **CREATE DATABASE AIPScannerUL_[clustername]**

    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```

2. Concedere i diritti all'utente che esegue il comando di installazione e viene usato per eseguire i comandi di gestione dello scanner. Usare lo script seguente:

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. Concedere i diritti per l'account del servizio scanner. Usare lo script seguente:

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="manually-create-a-database-and-user-for-the-network-discovery-service-and-grant-db_owner-rights"></a>Creazione manuale di un database e di un utente per il servizio di individuazione della rete e concessione dei diritti di db_owner

Se è necessario creare manualmente il database di [individuazione della rete](deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview) e/o creare un utente e concedere diritti di **db_owner** per il database, richiedere all'amministratore di sistema di eseguire i passaggi seguenti:

1. Creare un database per il servizio di individuazione della rete:

    ```sql
    **CREATE DATABASE AIPNetworkDiscovery_[clustername]**

    **ALTER DATABASE AIPNetworkDiscovery_[clustername] SET TRUSTWORTHY ON**
    ```

2. Concedere i diritti all'utente che esegue il comando di installazione e viene usato per eseguire i comandi di gestione dello scanner. Usare lo script seguente:

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. Concedere i diritti per l'account del servizio scanner. Usare lo script seguente:

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```
### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restrizione: all'account del servizio per lo scanner non può essere concesso il diritto **Log on locally** (Accesso locale)

Se i criteri dell'organizzazione proibiscono il diritto di **accesso locale** per gli account del servizio, usare il parametro *OnBehalfOf* con set-AIPAuthentication.

Per altre informazioni, vedere [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restrizione: l'account del servizio scanner non può essere sincronizzato con Azure Active Directory, ma il server ha connettività Internet

È possibile usare un account per eseguire il servizio dello scanner e un altro per l'autenticazione in Azure Active Directory:

- **Per l'account del servizio scanner**, utilizzare un account di Windows locale o un account Active Directory.

- **Per l'account Azure Active Directory**, specificare l'account locale per il parametro *OnBehalfOf* con set-AIPAuthentication. Per altre informazioni, vedere [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

### <a name="restriction-your-labels-do-not-have-auto-labeling-conditions"></a>Restrizione: le etichette non hanno condizioni di etichetta automatica

Se le etichette non hanno condizioni di etichetta automatica, pianificare l'uso di una delle opzioni seguenti durante la configurazione dello scanner:

|Opzione  |Descrizione  |
|---------|---------|
|**Individua tutti i tipi di informazioni**     |  Nel [processo di analisi del contenuto](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)impostare l'opzione **tipi di informazioni su individua** su **tutti**. </br></br>Questa opzione imposta il processo di analisi del contenuto per l'analisi del contenuto per tutti i tipi di informazioni riservate.      |
|**Usa l'etichettatura consigliata**     |  Nel [processo di analisi del contenuto](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)impostare l'opzione considera l' **etichetta consigliata come automatica** **su on**.</br></br> Questa impostazione configura lo scanner in modo da applicare automaticamente tutte le etichette consigliate al contenuto.      |
|**Definire un'etichetta predefinita**     |   Definire un'etichetta predefinita nei [criteri](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do), nel [processo di analisi del contenuto](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)o nel [repository](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository). </br></br>In questo caso lo scanner applica l'etichetta predefinita a tutti i file trovati.       |
| | |

## <a name="next-steps"></a>Passaggi successivi

Dopo aver verificato che il sistema è conforme ai prerequisiti dello scanner, continuare con [la distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](deploy-aip-scanner-configure-install.md).

Per una panoramica sullo scanner, vedere [Deploying the Azure Information Protection scanner to classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

**Ulteriori informazioni**:

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari in cui viene usato PowerShell, vedere [uso di PowerShell con il Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md).