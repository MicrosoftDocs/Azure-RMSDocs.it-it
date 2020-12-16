---
title: Azure Information Protection le etichette unificate client-cronologia delle versioni & criteri di supporto
description: Scopri le novità per il client Unified Labeling Azure Information Protection (AIP) per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7da6699fb2640791f78972f4271a6d846405731a
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583677"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l'assegnazione di etichette unificata client-versione e criteri di supporto

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Pertinente per**: [AIP Unified Labeling client only](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [cronologia delle versioni del client classico AIP e i criteri di supporto](client-version-release-history.md). *

È possibile scaricare il Azure Information Protection Unified Labeling client dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).

Dopo un breve ritardo di un paio di settimane, viene anche inclusa la versione di disponibilità generale più recente nel catalogo Microsoft Update. Le versioni Azure Information Protection hanno un nome di prodotto **Microsoft Azure Information Protection**  >  **Microsoft Azure Information Protection client unificato** per l'assegnazione di etichette e una classificazione degli **aggiornamenti**.

L'inclusione Azure Information Protection nel catalogo significa che è possibile aggiornare il client utilizzando WSUS o Configuration Manager o altri meccanismi di distribuzione software che utilizzano Microsoft Update di.

Per altre informazioni, vedere [upgradeing and maintaining the Azure Information Protection Unified Labeling client](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

## <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione disponibile a livello generale del client Azure Information Protection Unified Labeling è supportata per un massimo di sei mesi dopo il rilascio della versione GA successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Si noti che Azure Information Protection funzionalità sono attualmente in anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.

### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versioni di disponibilità generale non più supportate

|Versione client|Data di rilascio|
|--------------|-------------|
|2.5.33.0 |23/10/2019|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|
| | |

Il formato della data usato in questa pagina è *mese/giorno/anno*.

### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per visualizzare le novità o le modifiche apportate a una versione supportata del client Azure Information Protection Unified Labeling per Windows. La versione più recente è elencata per prima. Il formato della data usato in questa pagina è *mese/giorno/anno*.

La versione più recente di Azure Information Protection è attualmente in fase di anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.

> [!NOTE]
> Le correzioni secondarie non sono elencate, quindi se si verifica un problema con il client di etichettatura unificata, è consigliabile verificare se è stato risolto con la versione GA più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

Il client di etichettatura unificata sostituisce il client classico Azure Information Protection. Per confrontare caratteristiche e funzionalità con il client classico, vedere [confrontare le soluzioni per l'assegnazione di etichette per i computer Windows](use-client.md#compare-the-labeling-solutions-for-windows-computers).

## <a name="version-291090-public-preview"></a>Versione 2.9.109.0 (anteprima pubblica)

Scanner unificato per l'assegnazione di etichette e versione client 2.9.109.0

**Versione** 12/16/2020

Questa versione include le nuove funzionalità, le correzioni e i miglioramenti seguenti per lo scanner e il client di Unified Labeling:

- **Nuove funzionalità per lo scanner**:

    - [Supporto di PowerShell per server scanner disconnessi](#powershell-support-for-disconnected-scanner-servers)
    - [Supporto per repository NFS nei processi di analisi dei contenuti](#support-for-nfs-repositories-in-content-scan-jobs)
    - [Aggiunta del supporto per altri tipi di informazioni riservate](#added-support-for-additional-sensitive-information-types)

- **Nuove funzionalità per il client**:

    - [Tenere traccia dell'accesso ai documenti e revocare l'accesso](#track-document-access-and-revoke-access)
    - [Aggiunta del supporto per altri tipi di informazioni riservate](#added-support-for-additional-sensitive-information-types)

- **Correzioni e miglioramenti:**

    - [Correzioni e miglioramenti per lo scanner Unified Labeling](#fixes-and-improvements-for-the-unified-labeling-scanner)
    - [Correzioni e miglioramenti per il client Unified Labeling](#fixes-and-improvements-for-the-unified-labeling-client)

### <a name="powershell-support-for-disconnected-scanner-servers"></a>Supporto di PowerShell per server scanner disconnessi

Lo [scanner locale Azure Information Protection](../deploy-aip-scanner.md) supporta ora la gestione dei processi di analisi del contenuto, per i server scanner che non possono connettersi a Internet tramite PowerShell.

Per supportare i server scanner disconnessi, sono stati aggiunti i nuovi cmdlet seguenti:

|Cmdlet  |Descrizione  |
|---------|---------|
|**[Add-AIPScannerRepository](/powershell/module/azureinformationprotection/add-aipscannerrepository)**     | Aggiunge un nuovo repository al processo di analisi del contenuto.        |
|**[Get-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob)**     |      Ottiene i dettagli sul processo di analisi del contenuto.   |
|**[Get-AIPScannerRepository](/powershell/module/azureinformationprotection/get-aipscannerrepository)**     |  Ottiene i dettagli relativi ai repository definiti per il processo di analisi del contenuto.       |
|**[Remove-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)**       |    Elimina il processo di analisi del contenuto.     |
| **[Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)**    |   Rimuove un repository dal processo di analisi del contenuto.      |
|**[Set-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob)**     |   Definisce le impostazioni per il processo di analisi del contenuto.      |
**[Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository)**     |   Definisce le impostazioni per un repository esistente nel processo di analisi del contenuto.      |
| | |

È stato aggiunto anche il cmdlet [**set-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/set-mipnetworkdiscovery) per fornire supporto aggiuntivo che consente di aggiornare le impostazioni di installazione per il servizio di individuazione della rete tramite PowerShell.

Per ulteriori informazioni, vedere [quando il server dello scanner non può avere la connettività Internet](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) e [configurare lo scanner](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

### <a name="support-for-nfs-repositories-in-content-scan-jobs"></a>Supporto per repository NFS nei processi di analisi dei contenuti

È ora possibile aggiungere repository NFS ai processi di analisi del contenuto, oltre alle condivisioni file SMB e ai repository di SharePoint.

Per supportare le analisi sulle condivisioni NFS, i servizi per NFS devono essere distribuiti nel computer dello scanner:

1. Nel computer passare alla finestra di dialogo Impostazioni **funzionalità Windows (attiva o disattiva funzionalità Windows)** .

1. Selezionare gli elementi seguenti:

    - **Servizi per NFS**
        - **Strumenti di amministrazione**
        - **Client per NFS**

Per altre informazioni, vedere [creare un processo di analisi del contenuto](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job).

### <a name="added-support-for-additional-sensitive-information-types"></a>Aggiunta del supporto per altri tipi di informazioni riservate

È stato aggiunto il supporto per altri tipi di informazioni riservate in Azure Information Protection, ad esempio il **numero aziendale dell'Australia**, il **numero della società Australia** o la **scheda identità austriaca.**

Per ulteriori informazioni, vedere le [definizioni di entità di tipo informazioni riservate](/microsoft-365/compliance/sensitive-information-type-entity-definitions) nella documentazione di Microsoft 365.

### <a name="track-document-access-and-revoke-access"></a>Tenere traccia dell'accesso ai documenti e revocare l'accesso

Una volta eseguito l'aggiornamento alla versione 2.9.109.0, tutti i documenti non ancora registrati per il rilevamento vengono registrati alla successiva apertura in un computer con il client AIP Unified Labeling installato.

La registrazione dei documenti per il rilevamento consente agli amministratori di usare PowerShell per tenere traccia dell'accesso ai documenti e revocare l'accesso, se necessario.

Una volta eseguito l'aggiornamento, gli utenti finali possono anche revocare l'accesso per i documenti protetti. Per revocare l'accesso dalle app Microsoft Office, usare la nuova opzione **Revoca accesso** nel menu di **riservatezza** .

Per altre informazioni, vedere:

- [Guida dell'amministratore: rilevare e revocare l'accesso ai documenti con Azure Information Protection](track-and-revoke-admin.md)
- [Guida dell'utente: revocare l'accesso ai documenti con Azure Information Protection](revoke-access-user.md)
- [Problemi noti per il rilevamento e la revoca dell'accesso ai documenti](../known-issues.md#tracking-and-revoking-document-access-public-preview)

### <a name="fixes-and-improvements-for-the-unified-labeling-scanner"></a>Correzioni e miglioramenti per lo scanner Unified Labeling

Nella versione 2.9.109.0 di [Azure Information Protection scanner Unified Labeling](../deploy-aip-scanner.md)sono state fornite le correzioni seguenti:

- Aggiunta del supporto per i trattini ( **-** ) nei nomi di [database dello scanner](../deploy-aip-scanner-prereqs.md)
- Aggiornamenti nei report per quando l'opzione **[file etichetta basata su contenuto](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job)** è impostata su **off**
- [Miglioramento dell'utilizzo della memoria](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance) per un numero elevato di corrispondenze di tipo informazioni
- Supporto per percorsi [locali di SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) che terminano con una barra ( **/** )
- Maggiore [velocità](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance) di analisi di SharePoint

- Supporto per [evitare un timeout](clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint) durante l'analisi di un server SharePoint.

### <a name="fixes-and-improvements-for-the-unified-labeling-client"></a>Correzioni e miglioramenti per il client Unified Labeling

- Problemi risolti per l' [assegnazione di etichette ai messaggi](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-emails) di posta elettronica da Office MSI, ad esempio quando si risponde o si invia un messaggio di posta elettronica.

- Gli eventi del [log di controllo di NewLabel](../audit-logs.md#new-label-audit-logs) ora includono l'origine dell'azione, per gli eventi generati da messaggi di posta elettronica inviati da Outlook.

- Sono stati risolti i problemi per i quali il criterio non è stato aggiornato senza cancellare la cache, dopo aver [apportato modifiche ai criteri di etichetta in Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).

- La modalità anteprima di Outlook genera ora [i log di controllo per gli eventi di individuazione](../audit-logs.md#discover-audit-logs)

- Le etichette e le [filigrane](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) [consigliate](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) vengono applicate come previsto in Outlook. 

- Aggiunta del supporto per le impostazioni [OutlookBlockTrustedDomains](clientv2-admin-guide-customizations.md#to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels) e [OutlookBlockUntrustedCollaborationLabel](clientv2-admin-guide-customizations.md#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels) per i contatti nelle liste di distribuzione.

    Per configurare questa impostazione, impostare il valore [EnableOutlookDistributionListExpansion](clientv2-admin-guide-customizations.md#to-implement-block-messages-for-recipients-inside-an-outlook-distribution-list-public-preview) su **true**. Potrebbe anche essere necessario aumentare il valore di timeout predefinito, come definito nell'impostazione [OutlookGetEmailAddressesTimeOutMSProperty](clientv2-admin-guide-customizations.md#to-implement-block-messages-for-recipients-inside-an-outlook-distribution-list-public-preview) .

- Aggiornamenti dell' [ordine di precedenza](clientv2-admin-guide-customizations.md#order-of-precedence---how-conflicting-settings-are-resolved) utilizzato quando per un utente sono configurati più criteri di etichetta, ognuno con impostazioni avanzate in conflitto.

    In questi casi, le impostazioni avanzate del primo criterio vengono sempre applicate in base all'ordine dei criteri nell'interfaccia di amministrazione. L'eccezione per *OutlookDefaultLabel* è stata rimossa.

- In uno scenario in cui **% AppData% (AppData\Roaming)** punta a una struttura di cartelle di Windows non predefinita, i file nelle cartelle di cui è stato eseguito il mapping alle directory utente sono ora [esclusi dall'assegnazione di etichette e dalla protezione](clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection) come previsto, in base alla configurazione.

- [Nuova impostazione client avanzata](clientv2-admin-guide-customizations.md#remove-all-shapes-of-a-specific-shape-name) (**PowerPointRemoveAllShapesByShapeName**), aggiunta per rimuovere forme da intestazioni o piè di pagina di PowerPoint, usando il nome della forma anziché il testo all'interno di una forma.

## <a name="version-28850"></a>Versione 2.8.85.0

Scanner unificato per l'assegnazione di etichette e versione client 2.8.85.0

**Rilasciato** 09/22/2020

Questa versione include le nuove funzionalità, le correzioni e i miglioramenti seguenti per lo scanner e il client di Unified Labeling:

- **Nuove funzionalità per lo scanner**:

    - [Ripetizioni complete facoltative per le modifiche rilevate](#optional-full-rescans-for-changes-detected)
    - [Configurare i timeout di SharePoint](#configure-sharepoint-timeouts)
    - [Supporto per l'individuazione della rete](#network-discovery-support)

- **Nuove funzionalità per il client**:

    - [Personalizzazioni dell'amministratore per i popup AIP in Outlook](#administrator-customizations-for-aip-popups-in-outlook)
    - [Personalizzazioni dell'amministratore per richieste di giustificazione](#administrator-customizations-for-justification-prompts)
    - [Aggiornamenti dei log di controllo](#audit-log-updates)
    - [Aggiornamenti delle etichette basate sul modello DKE](#dke-template-based-labeling-updates)

- **Correzioni e miglioramenti:**

    - [Correzioni e miglioramenti dello scanner](#azure-information-protection-scanner-fixed-issues-version-28850)
    - [Correzioni e miglioramenti dei client](#azure-information-protection-client-fixed-issues-version-28850)


### <a name="optional-full-rescans-for-changes-detected"></a>Ripetizioni complete facoltative per le modifiche rilevate

Gli amministratori possono ora ignorare una ripetizione dell'analisi completa dopo avere apportato modifiche ai criteri o ai processi di analisi del contenuto. Ignorando una ripetizione completa si applicano le modifiche solo ai file che sono stati modificati o creati dall'ultima analisi.

Ad esempio, è possibile che siano state apportate modifiche che incidono solo sull'utente finale, ad esempio nei contrassegni visivi, e che non si voglia richiedere il tempo necessario per eseguire immediatamente una ripetizione dell'analisi completa.

Ignorare la ripetizione dell'analisi immediata completa e tornare in seguito per [eseguire una ripetizione dell'analisi completa](../deploy-aip-scanner-manage.md#rescanning-files) e applicare le modifiche nei repository.

> [!IMPORTANT]
> Gli amministratori che apportano modifiche ai criteri e ai processi di analisi dei contenuti devono ora comprendere gli effetti delle modifiche apportate al contenuto e determinare se è necessaria una ripetizione dell'analisi completa.
>
> Se, ad esempio, sono state modificate le impostazioni di **imposizione dei criteri** da **enforce = off** a **Imponi = on**, assicurarsi di eseguire una ripetizione dell'analisi completa per applicare le etichette nel contenuto.
>

### <a name="configure-sharepoint-timeouts"></a>Configurare i timeout di SharePoint

Il timeout predefinito per le interazioni con SharePoint è stato aggiornato a due minuti, dopo il quale l'operazione di tentativo di AIP ha esito negativo.

Gli amministratori AIP possono ora configurare anche i timeout di SharePoint, separatamente per tutte le richieste Web e le richieste Web di file.

Per altre informazioni, vedere [configurare i timeout di SharePoint](clientv2-admin-guide-customizations.md#configure-sharepoint-timeouts).

### <a name="network-discovery-support"></a>Supporto per l'individuazione della rete

Lo scanner Unified Labeling include ora un nuovo servizio di **individuazione della rete** , che consente di analizzare gli indirizzi IP o gli intervalli specificati per le condivisioni file di rete che possono avere contenuto sensibile.

Il servizio di **individuazione della rete** aggiorna i report del **repository** con un elenco di percorsi di condivisione che potrebbero essere a rischio, in base alle autorizzazioni individuate e ai diritti di accesso. Controllare i report del **repository** aggiornati per assicurarsi che i processi di analisi dei contenuti includano tutti i repository che devono essere analizzati.

> [!TIP]
> Per ulteriori informazioni, vedere [cmdlet di individuazione della rete](#network-discovery-cmdlets).

**Per utilizzare il servizio di individuazione della rete**

1. Aggiornare la versione dello scanner e verificare che il cluster dello scanner sia configurato correttamente. Per altre informazioni, vedere:
    - [Aggiornamento dello scanner](../deploy-aip-scanner-configure-install.md#upgrading-your-scanner)
    - [Creare un cluster di scanner](../deploy-aip-scanner-configure-install.md#create-a-scanner-cluster)

1. Assicurarsi di aver abilitato Azure Information Protection Analytics.

    Nella portale di Azure passare a **Azure Information Protection > gestisci > Configura analisi (anteprima).**

    Per ulteriori informazioni, vedere [la pagina relativa alla creazione di report centrali per Azure Information Protection (anteprima pubblica)](../reports-aip.md).

1. Abilitare l'individuazione di rete eseguendo il cmdlet di PowerShell [**Install-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) .

    > [!IMPORTANT]
    > Quando si esegue questo cmdlet, assicurarsi di usare un utente vulnerabile come valore per il parametro **StandardDomainsUserAccount** per assicurarsi che venga segnalato l'accesso pubblico ai repository.
    >
    > Questo utente deve essere membro solo del gruppo **Domain Users** e viene usato per simulare l'accesso pubblico ai repository.

1. Nella portale di Azure passare a Azure Information Protection > processi di **analisi di rete** e [creare processi per analizzare aree specifiche della rete](../deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview).

1. Usare i report generati nel nuovo riquadro [**repository**](../deploy-aip-scanner-configure-install.md#analyze-risky-repositories-found-public-preview) per trovare altre condivisioni file di rete che potrebbero essere a rischio. Aggiungere qualsiasi condivisione file rischiosa ai [processi di analisi del contenuto](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job) per analizzare i repository aggiunti per il contenuto sensibile.

#### <a name="network-discovery-cmdlets"></a>Cmdlet di individuazione della rete

I cmdlet di PowerShell aggiunti per l'individuazione della rete includono:

|Cmdlet  |Descrizione  |
|---------|---------|
|[**Get-MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)     |   Ottiene l'impostazione corrente che indica se il servizio di individuazione della rete estrae i dati di analisi di rete dalla configurazione predefinita, online o da un file offline esportato dal portale di Azure.      |
|[**Get-MIPNetworkDiscoveryJobs**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)     |    Ottiene un elenco di processi di analisi di rete attualmente configurati.     |
|[**Get-MIPNetworkDiscoveryStatus**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)     |     Ottiene lo stato corrente di tutti i processi di analisi di rete configurati nel tenant.    |
| [**Import-MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)     |    Importa la configurazione per un processo di analisi di rete da un file.     |
| [**Install-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)| Installa il servizio di individuazione della rete |
|[**Set-MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)     |   Imposta la configurazione che indica se il servizio di individuazione della rete estrae i dati di analisi della rete dalla configurazione predefinita, online o da un file offline esportato dal portale di Azure.      |
|[**Start-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)     |  Esegue immediatamente un processo di analisi di rete specifico.       |
|[**Uninstall-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)     |  Disinstalla il servizio di individuazione della rete.       |
| | |


### <a name="administrator-customizations-for-aip-popups-in-outlook"></a>Personalizzazioni dell'amministratore per i popup AIP in Outlook

Gli amministratori di AIP possono ora personalizzare i popup visualizzati in Outlook per gli utenti finali, ad esempio i popup per i messaggi di posta elettronica bloccati, i messaggi di avviso e le richieste di giustificazione.

Per altre informazioni, incluse diverse regole di esempio per gli scenari con casi d'uso comuni, vedere [personalizzare i messaggi popup di Outlook](clientv2-admin-guide-customizations.md#customize-outlook-popup-messages).

### <a name="administrator-customizations-for-justification-prompts"></a>Personalizzazioni dell'amministratore per richieste di giustificazione

Gli amministratori di AIP possono ora personalizzare una delle opzioni nelle richieste di giustificazione visualizzate quando gli utenti finali modificano le etichette di classificazione nei documenti e nei messaggi di posta elettronica.

Per altre informazioni, vedere [personalizzare i messaggi di richiesta di giustificazione per le etichette modificate](clientv2-admin-guide-customizations.md#customize-justification-prompt-texts-for-modified-labels).

### <a name="audit-log-updates"></a>Aggiornamenti dei log di controllo

I log di controllo per gli eventi di accesso dal client Unified Labeling vengono ora inviati solo quando gli utenti aprono file con etichetta o protetti, offrendo un'indicazione più chiara dell'accesso degli utenti.

Per altre informazioni, vedere [accedere ai log di controllo](../audit-logs.md#access-audit-logs).

### <a name="dke-template-based-labeling-updates"></a>Aggiornamenti delle etichette basate sul modello DKE

Azure Information Protection supporta ora l'assegnazione di etichette basate su modelli DKE (Double Key Encryption) nello scanner, nonché l'uso di Esplora file e PowerShell.

Per altre informazioni, vedere:

- [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-implement-tenant-key.md)
- [Crittografia a chiave doppia](/microsoft-365/compliance/double-key-encryption) nella documentazione di Microsoft 365

### <a name="azure-information-protection-scanner-fixed-issues-version-28850"></a>Problemi di Azure Information Protection scanner corretti, versione 2.8.85.0

Nella versione 2.8.85.0 di Azure Information Protection scanner Unified Labeling sono state fornite le correzioni seguenti:

- Miglioramenti per l' [analisi dei file con percorsi lunghi](../deploy-aip-scanner-prereqs.md#file-path-requirements)
- Lo scanner AIP ora analizza gli ambienti [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) completi quando sono presenti più ContentDatabases.
- Lo scanner AIP ora supporta i file di [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) con un punto nel percorso, ma senza estensione. Ad esempio, un file con il percorso `https://sharepoint.contoso.com/shared documents/meeting-notes` , senza estensione, viene ora analizzato correttamente.
- Lo scanner AIP supporta ora i [tipi di informazioni riservate personalizzate](../deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types) che vengono creati in Microsoft Security and Compliance Center e non appartengono a nessun criterio.

### <a name="azure-information-protection-client-fixed-issues-version-28850"></a>Problemi fissi del client di Azure Information Protection, versione 2.8.85.0

Nella versione 2.8.85.0 di Azure Information Protection Unified Labeling client sono state fornite le correzioni seguenti:

- Nuova indicazione visualizzata per tutti gli elementi attualmente selezionati dal menu ![icona colonne](../media/selected-sensitivity-options.png "icona colonne") **sensibili** nelle app di Office. Per ulteriori informazioni, vedere la pagina relativa alle [etichette di riservatezza nell'Microsoft 365 docs](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do).
- Correzioni per la visualizzazione dei file JPEG nel [Visualizzatore AIP](clientv2-view-use-files.md)
- Il downgrade di un'etichetta ora include automaticamente il **ProtectionOwnerBefore** negli [eventi di controllo](../audit-logs.md#downgrade-label-audit-logs)
- Gli eventi di modifica ora includono **LastModifiedDate** nei [log di controllo](../audit-logs.md#change-protection-audit-logs)
- Aggiunta del supporto per i file **proxy. PAC** quando si utilizza un proxy per acquisire un token. Per ulteriori informazioni, vedere [firewall e requisiti dell'infrastruttura di rete](../requirements.md#firewalls-and-network-infrastructure).
- Correzioni per l'autenticazione durante l' [aggiornamento dei criteri](../configure-policy.md#making-changes-to-the-policy)
- Correzioni per gli aggiornamenti del [contrassegno di contenuto automatico](../configure-policy-markings.md) per PowerPoint in modalità di sola lettura
- Miglioramenti nei popup e nei testi degli errori
- La descrizione comando viene aggiornata per mostrare la classificazione più elevata [per gli allegati di posta elettronica](../faqs-infoprotect.md#when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling), considerando sia la classificazione del messaggio di posta elettronica che l'allegato.
- Corregge il **report di un** testo del problema quando si modificano i criteri di etichettatura di riservatezza usando il cmdlet [**set-LabelPolicy**](/powershell/module/exchange/set-labelpolicy)
- Corregge gli errori visualizzati quando il cmdlet [**set-AipFileLabel**](/powershell/module/azureinformationprotection/set-aipfilelabel) viene usato con un ID etichetta non valido.
- Correzioni delle prestazioni per la decrittografia di messaggi di posta elettronica SMIME nel riquadro di lettura di Outlook. Per implementare questa correzione, abilitare la proprietà avanzata [**OutlookSkipSmimeOnReadingPaneEnabled**](clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) .
- Correzioni per la [decrittografia dei file PST](clientv2-admin-guide-file-types.md) che contengono file crittografati con password. La decrittografia dei file PST non riesce più se il file PST contiene un file protetto da password.
- La rimozione di un'etichetta di protezione non inclusa nei criteri con ambito consente ora di rimuovere l'etichetta e la protezione dal contenuto.

## <a name="version-271010"></a>Versione 2.7.101.0

Scanner unificato per l'assegnazione di etichette e versione client 2.7.101.0

**Rilasciato** 08/23/2020

**Correzione**:

Correzione di un problema per gli utenti di PPT, Excel e Word che causavano il blocco dei file, l'arresto anomalo o la necessità di ripetere il salvataggio che era correlato a etichette obbligatorie configurate con protezione, filigrana e/o contrassegno di contenuto.

## <a name="version-27990"></a>Versione 2.7.99.0

Scanner unificato per l'assegnazione di etichette e versione client 2.7.99.0

**Rilasciato** 07/20/2020

**Correzioni e miglioramenti**:

Correzione dei problemi nelle azioni di assegnazione di etichette di file per i nuovi log di controllo delle **etichette** .

Per ulteriori informazioni, vedere la pagina relativa alla [versione 2.7.96.0](#version-27960) e [Azure Information Protection riferimento al log di controllo (anteprima pubblica)](../audit-logs.md).

## <a name="version-27960"></a>Versione 2.7.96.0

Scanner unificato per l'assegnazione di etichette e versione client 2.7.96.0

**Rilasciato** 06/29/2020

- [Nuove funzionalità per Unified Labeling client, versione 2.7.96.0](#new-features-for-the-unified-labeling-client-version-27960)
- [Nuove funzionalità per lo scanner Unified Labeling, versione 2.7.96.0](#new-features-for-the-unified-labeling-scanner-version-27960)
- [Nuovi log di controllo generati per i file rimossi](#new-audit-logs-generated-for-removed-files)
- [Imposizione di TLS 1.2](#tls-12-enforcement)
- [Correzioni e miglioramenti, versione 2.7.96.0](#fixes-and-improvements-version-27960)
### <a name="new-features-for-the-unified-labeling-scanner-version-27960"></a>Nuove funzionalità per lo scanner Unified Labeling, versione 2.7.96.0

- [Usare lo scanner per applicare etichette in base alle condizioni consigliate](../deploy-aip-scanner-prereqs.md). I clienti AIP possono ora scegliere di implementare solo l'etichettatura automatica lato servizio. Questa funzionalità consente agli utenti finali di AIP di seguire sempre le raccomandazioni invece dello scenario precedente, che abilitava solo l'assegnazione automatica di etichette sul lato utente.

- [Informazioni sui file individuati in precedenza da scanner eliminati dal repository analizzato](../reports-aip.md) Questi file eliminati non sono stati segnalati in precedenza in AIP Analytics e sono ora disponibili nel report di individuazione dello scanner.

- [Ottenere i report dallo scanner negli errori per applicare gli eventi di azione](../reports-aip.md#friendly-schema-reference-for-event-functions). Usare i report per ottenere informazioni sugli eventi di azione non riusciti e individuare modi per evitare future occorrenze.

- Introduzione dello strumento Analizzatore diagnostica di AIP scanner per il rilevamento e l'analisi degli errori comuni del scanner. Per iniziare a usare la diagnostica dello scanner AIP, [eseguire il nuovo cmdlet **Start-AIPScannerDiagnostics**](../deploy-aip-scanner-manage.md#troubleshooting-using-the-scanner-diagnostic-tool).

- È ora possibile gestire e limitare l'utilizzo massimo della CPU nel computer dello scanner. Informazioni su come impedire il 100% di utilizzo della CPU e gestire l'utilizzo della CPU con [due nuove impostazioni avanzate **ScannerMaxCPU** e **ScannerMinCPU**](./clientv2-admin-guide-customizations.md#limit-cpu-consumption).

- A questo punto è possibile configurare lo scanner Unified Labeling per ignorare i file specifici a seconda degli attributi di file. Definire l'elenco degli attributi di file che attiva un file da ignorare usando la nuova impostazione avanzata di **[ScannerFSAttributesToSkip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes)** .

### <a name="new-features-for-the-unified-labeling-client-version-27960"></a>Nuove funzionalità per Unified Labeling client, versione 2.7.96.0

- Sono ora visualizzati [**popup di giustificazione**](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) per le modifiche apportate alle etichette predefinite nel client di etichettatura unificata.

- Integrazione più uniforme con i contrassegni di contenuto visivi applicati da Office. Per altre informazioni sulla configurazione dei contrassegni di contenuto nei documenti di Office, vedere [come configurare un'etichetta per i contrassegni visivi per Azure Information Protection](../configure-policy-markings.md).

- La nuova proprietà avanzata **WordShapeNameToRemove** consente la rimozione del contrassegno di contenuto nei documenti di Word creati da applicazioni di terze parti. Altre informazioni su come [identificare i nomi delle forme esistenti e definirli per la rimozione usando **WordShapeNameToRemove**](./clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions).

- Supporto per la **crittografia a chiave doppia (DKE)** (anteprima pubblica).

    È ora possibile usare il client Unified Labeling per proteggere il contenuto altamente sensibile mantenendo il controllo completo della chiave. DKE richiede due chiavi per accedere al contenuto protetto: una chiave viene archiviata in Azure e l'altra chiave viene mantenuta dal cliente.

    Per altre informazioni sulle chiavi radice del tenant predefinite basate sul cloud, vedere [pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-implement-tenant-key.md). Per informazioni sull'implementazione della crittografia a chiave doppia, vedere [crittografia a chiave doppia](/microsoft-365/compliance/double-key-encryption) nella documentazione di Microsoft 365.

### <a name="new-audit-logs-generated-for-removed-files"></a>Nuovi log di controllo generati per i file rimossi

I log di controllo vengono ora generati ogni volta che lo scanner rileva che un file precedentemente sottoposto a scansione è stato rimosso.

Per altre informazioni, vedere:

- [Log di controllo rimossi dal file](../audit-logs.md#file-removed-audit-logs)
- [Reporting centralizzato per Azure Information Protection](../reports-aip.md)

> [!IMPORTANT]
> In questa versione le azioni di assegnazione di etichette di file non generano nuovi log di controllo **etichetta** .
> Se si esegue lo scanner in **Imponi = in** modalità, è consigliabile eseguire l'aggiornamento alla [versione 2.7.99.0](#version-27990).
>

### <a name="tls-12-enforcement"></a>Imposizione di TLS 1.2

A partire da questa versione del client di Azure Information Protection, sono supportate solo le versioni di TLS 1,2 o successive.

I clienti che dispongono di un programma di installazione di TLS che non supporta TLS 1,2 devono passare a una configurazione che supporta TLS 1,2 per l'uso di criteri di Azure Information Protection, token, controllo e protezione e per ricevere comunicazioni basate su Azure Information Protection.

Per ulteriori informazioni sui requisiti, vedere [firewall e requisiti dell'infrastruttura di rete](../requirements.md#firewalls-and-network-infrastructure).

### <a name="fixes-and-improvements-version-27960"></a>Correzioni e miglioramenti, versione 2.7.96.0

- Miglioramenti di scanner SQL per:
    - Prestazioni
    - File con un numero elevato di tipi di informazioni

- Miglioramenti dell'analisi di SharePoint per:
    - Analisi delle prestazioni
    - File con caratteri speciali nel percorso
    - Librerie con numero di file di grandi dimensioni

    Per visualizzare una guida introduttiva per l'uso di Azure Information Protection con SharePoint, vedere [Guida introduttiva: trovare le informazioni riservate presenti nei file archiviati in locale](../quickstart-findsensitiveinfo.md).

- Notifiche utente migliorate per i criteri mancanti. Per ulteriori informazioni sui criteri di etichetta per il client Unified Labeling, vedere la pagina relativa ai [criteri delle etichette che possono](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do) essere eseguite nella documentazione Microsoft 365.

- Le [Etichette automatiche](../configure-policy-classification.md) vengono ora applicate in Excel per gli scenari in cui un utente inizia a chiudere un file senza salvarlo, così come avviene quando un utente salva attivamente un file.

- Le intestazioni e i piè di pagina vengono rimossi come previsto e non in ogni salvataggio del documento, quando viene configurata l'impostazione [ExternalContentMarkingToRemove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) .

- Le [variabili utente dinamiche](../configure-policy-markings.md#using-variables-in-the-text-string) sono ora visualizzate nei contrassegni visivi di un documento come previsto.

- Si è verificato un problema per cui solo la prima pagina di contenuto di un file PDF veniva utilizzata per l'applicazione delle regole di classificazione e la classificazione autoclassificazione basata su tutto il contenuto del file PDF ora procede come previsto. Per ulteriori informazioni sulla classificazione e l'assegnazione di etichette, vedere [domande frequenti sulla classificazione e l'assegnazione di etichette](../faqs-infoprotect.md).

- Quando vengono configurati più account di Exchange e il client Azure Information Protection Outlook è abilitato, i messaggi di posta elettronica vengono inviati dall'account secondario come previsto. Per ulteriori informazioni sulla configurazione del client Unified Labeling con Outlook, vedere [prerequisiti aggiuntivi per il Azure Information Protection client Unified Labeling](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

- Quando un documento con un'etichetta di riservatezza superiore viene trascinato e rilasciato in un messaggio di posta elettronica, il messaggio di posta elettronica riceve automaticamente l'etichetta di riservatezza superiore come previsto. Per ulteriori informazioni sull'assegnazione di etichette alle funzionalità client, vedere la [tabella di confronto dei client con etichetta](use-client.md#compare-the-labeling-solutions-for-windows-computers).

- Le autorizzazioni personalizzate vengono ora applicate ai messaggi di posta elettronica come previsto, quando gli indirizzi di posta elettronica includono un apostrofo (') e un punto (.) Per ulteriori informazioni sulla configurazione del client Unified Labeling con Outlook, vedere [prerequisiti aggiuntivi per il Azure Information Protection client Unified Labeling](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

- Per impostazione predefinita, il proprietario NTFS di un file viene perso quando il file viene identificato dallo scanner di etichette unificato, da PowerShell o dall'estensione di Esplora file. A questo punto è possibile configurare il sistema per la conservazione del proprietario NTFS del file impostando la nuova impostazione avanzata **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** su **true**.

    L'impostazione avanzata **UseCopyAndPreserveNTFSOwner** richiede una connessione di rete affidabile e a bassa latenza tra lo scanner e il repository analizzato.

## <a name="version-261110"></a>Versione 2.6.111.0

**Rilasciato** 03/09/2020

Supportato tramite 12/29/2020

### <a name="new-features-version-261110"></a>Nuove funzionalità, versione 2.6.111.0

- Versione di disponibilità generale dello [scanner](../deploy-aip-scanner.md)per esaminare ed etichettare i documenti negli archivi dati locali.

- Correlate allo [scanner](../deploy-aip-scanner.md) :
    - [Individuazione più semplice in locale e nel sito secondario di SharePoint](../quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories). L'impostazione di ciascun sito specifico non è più necessaria.
    - Proprietà avanzata per il [ridimensionamento del blocco SQL](../deploy-aip-scanner-prereqs.md#storage-requirements-and-capacity-planning-for-sql-server) aggiunto.
    - Gli amministratori hanno ora la possibilità di [arrestare le analisi esistenti ed eseguire una ripetizione dell'analisi](../deploy-aip-scanner-manage.md#stopping-a-scan) se è stata apportata una modifica all'etichetta predefinita.
    - Per impostazione predefinita, lo scanner ora imposta la telemetria minima per le analisi più veloci e le dimensioni ridotte del log e i tipi di informazioni sono ora memorizzati nella cache nel database Altre informazioni sull' [ottimizzazione dello scanner](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance).
    - Lo scanner supporta ora distribuzioni separate per il database e il servizio, mentre i diritti **sysadmin** sono necessari solo per la distribuzione del database.
    - Miglioramenti apportati alle prestazioni dello scanner.

- Modifica del cmdlet di [PowerShell](./clientv2-admin-guide-powershell.md) **set-AIPFileLabel** per abilitare la rimozione della protezione dai file PST, rar, 7zip e msg. Questa funzionalità è disabilitata per impostazione predefinita e deve essere attivata usando il cmdlet [set-LabelPolicy](./clientv2-admin-guide-customizations.md) , come descritto [qui](./clientv2-admin-guide-customizations.md#enable-removal-of-protection-from-compressed-files).  

- È stata aggiunta la possibilità per gli amministratori di Azure Information Protection di controllare quando vengono usate le estensioni. Pfile per i file. Altre informazioni sulla [modifica dei tipi di file protetti](./clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

- Aggiunto supporto del contrassegno visivo dinamico per le applicazioni e le variabili. Altre informazioni su come [configurare le etichette per i contrassegni visivi](../configure-policy-markings.md).

- Miglioramenti apportati ai [Suggerimenti per i criteri personalizzabili per le etichette automatiche e consigliate](use-client.md).

- Aggiunto il supporto per la [funzionalità di assegnazione di etichette offline](./clientv2-admin-guide-customizations.md#support-for-disconnected-computers) con le app di Office nel client Unified labeling.

### <a name="fixes-and-improvements-version-261110"></a>Correzioni e miglioramenti, versione 2.6.111.0

- Nei casi in cui gli utenti hanno tentato di aprire i file TIFF protetti e i file TIFF creati da RightFax, i file TIFF sono ora aperti e rimangono stabili come previsto.  
- Sono stati risolti i danneggiamenti precedenti dei file txt e PDF protetti.
- È stata corretta l'assegnazione di etichette incoerenti tra **automatico** e **manuale** in log Analytics.
- Sono stati risolti problemi di ereditarietà imprevisti identificati tra i nuovi messaggi di posta elettronica e l'ultimo messaggio di posta elettronica aperto.  
- La protezione dei file con **estensione msg** come **. msg. Pfile** ora funziona come previsto.
- Le autorizzazioni di comproprietario aggiunte dalle impostazioni definite dall'utente di Office sono ora applicate come previsto.
- Quando si immette la giustificazione del downgrade delle autorizzazioni, non è più possibile immettere il testo quando sono già selezionate altre opzioni.

## <a name="next-steps"></a>Passaggi successivi

Se non si è certi che l'etichetta unificata sia il client giusto da installare,  Vedere [scegliere la soluzione di etichettatura di Windows](use-client.md#choose-your-windows-labeling-solution).

Per ulteriori informazioni sull'installazione e l'utilizzo del client Unified Labeling:

- Per utenti: [Scaricare e installare il client](install-unifiedlabelingclient-app.md)

- Per gli amministratori: [Azure Information Protection guida dell'amministratore client per l'assegnazione di etichette unificata](clientv2-admin-guide.md)
