---
title: Azure Information Protection le etichette unificate client-cronologia delle versioni & criteri di supporto
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 32d0ac2669e0cc304d0f06c603f64d623c216c68
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117654"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l'assegnazione di etichette unificata client-versione e criteri di supporto

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


È possibile scaricare il Azure Information Protection Unified Labeling client dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Dopo un breve ritardo di genere in un paio di settimane, la versione di disponibilità generale più recente è inclusa anche nel catalogo di Microsoft Update con il nome di un prodotto **Microsoft Azure Information Protection** > **Microsoft Azure Information Protection Unified Labeling client**e la classificazione degli **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [upgradeing and maintaining the Azure Information Protection Unified Labeling client](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione disponibile a livello generale del client Azure Information Protection Unified Labeling è supportata per un massimo di sei mesi dopo il rilascio della versione GA successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versioni di disponibilità generale non più supportate:

|Versione client|Data di rilascio|
|--------------|-------------|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|

Il formato della data usato in questa pagina è *mese/giorno/anno*.


### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per visualizzare le novità o le modifiche apportate a una versione supportata del client Azure Information Protection Unified Labeling per Windows. La versione più recente è elencata per prima. Il formato della data usato in questa pagina è *mese/giorno/anno*.

> [!NOTE]
> Le correzioni secondarie non sono elencate, quindi se si verifica un problema con il client di etichettatura unificata, è consigliabile verificare se è stato risolto con la versione GA più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

Il client sta sostituendo il client di Azure Information Protection (classico). Per confrontare caratteristiche e funzionalità con il client classico, vedere [confrontare i client di assegnazione di etichette per i computer Windows](use-client.md#compare-the-labeling-clients-for-windows-computers).

## <a name="version-261010"></a>Versione 2.6.101.0

**Rilasciato** 1/15/2020

**Nuove funzionalità:**

- La modifica del cmdlet di [PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell) **set-AIPFileLabel** consente di rimuovere la protezione dai file PST, rar, 7zip e msg. 

- È stata aggiunta la possibilità per gli amministratori di Azure Information Protection di controllare quando vengono usate le estensioni. Pfile per i file. Altre informazioni sulla [modifica dei tipi di file protetti](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect). 

- Aggiunto supporto del contrassegno visivo dinamico per le applicazioni e le variabili. Altre informazioni su come [configurare le etichette per i contrassegni visivi](https://docs.microsoft.com/azure/information-protection/configure-policy-markings). 

- Miglioramenti apportati ai [Suggerimenti per i criteri personalizzabili per le etichette automatiche e consigliate](use-client.md).   

- Aggiunto il supporto per la [funzionalità di assegnazione di etichette offline](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers) con le app di Office nel client Unified labeling.

- La nuova proprietà avanzata **WordShapeNameToRemove** consente la rimozione del contrassegno di contenuto nei documenti di Word creati da applicazioni di terze parti. Altre informazioni su come [identificare i nomi delle forme esistenti e definirli per la rimozione usando **WordShapeNameToRemove**](https://docs.microsoft.com/azure/information-protection/clientv2-admin-guide-customizations#remove-headers-and-footers-from-other-labeling-solutions). 

- Funzionalità correlate allo [scanner](../deploy-aip-scanner.md) :
    - [Individuazione più semplice in locale e nel sito secondario di SharePoint](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories). L'impostazione di ciascun sito specifico non è più necessaria. 
    - Proprietà avanzata per il [ridimensionamento del blocco SQL](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server) aggiunto.
    - Gli amministratori hanno ora la possibilità di [arrestare le analisi esistenti ed eseguire una nuova analisi](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan) se è stata apportata una modifica all'etichetta predefinita.
    - Per impostazione predefinita, lo scanner ora imposta la telemetria minima per le analisi più veloci e le dimensioni ridotte del log e i tipi di informazioni sono ora memorizzati nella cache nel database Altre informazioni sull' [ottimizzazione dello scanner](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner). 

**Correzioni**

- Lo scanner supporta ora distribuzioni separate per il database e il servizio, mentre i diritti **sysadmin** sono necessari solo per la distribuzione del database. 
- Nei casi in cui gli utenti hanno tentato di aprire i file TIFF protetti e i file TIFF creati da RightFax, i file TIFF sono ora aperti e rimangono stabili come previsto.  
- Sono stati risolti i danneggiamenti precedenti dei file txt e PDF protetti.
- È stata corretta l'assegnazione di etichette incoerenti tra **automatico** e **manuale** in log Analytics. 
- Sono stati risolti problemi di ereditarietà imprevisti identificati tra i nuovi messaggi di posta elettronica e l'ultimo messaggio di posta elettronica aperto.  
- La protezione dei file con estensione msg come. msg. Pfile ora funziona come previsto. 
- Le autorizzazioni di comproprietario aggiunte dalle impostazioni definite dall'utente di Office sono ora applicate come previsto. 
- Quando si immette la giustificazione del downgrade delle autorizzazioni, non è più possibile immettere il testo quando sono già selezionate altre opzioni. 


## <a name="version-25330"></a>Versione 2.5.33.0

**Rilasciata**: 10/23/2019

**Nuove funzionalità:**

- Versione di anteprima dello [scanner](../deploy-aip-scanner.md)per ispezionare ed etichettare i documenti archivi dati locali. Con questa versione dello scanner:
    
    - Più scanner possono condividere lo stesso database di SQL Server quando si configurano gli scanner per l'uso dello stesso profilo dello scanner. Questa configurazione facilita la gestione di più scanner e comporta tempi di analisi più rapidi. Quando si usa questa configurazione, è sempre necessario attendere il completamento dell'installazione di uno scanner prima di installare un altro scanner con lo stesso profilo.
    
    - È necessario specificare un profilo quando si installa lo scanner e il database dello scanner è denominato **AIPScannerUL_\<profile_name >** . Il parametro *profile* è obbligatorio anche per set-AIPScanner.
    
    - È possibile impostare un'etichetta predefinita su tutti i documenti, anche se i documenti sono già etichettati. Nel profilo scanner o nelle impostazioni del repository, impostare l'opzione **rietichettare i file** **su on** con la nuova casella di controllo **Imponi etichetta predefinita** selezionata.
    
    - È possibile rimuovere le etichette esistenti da tutti i documenti e questo Act include la rimozione della protezione se è stata precedentemente applicata da un'etichetta. La protezione applicata indipendentemente da un'etichetta viene mantenuta. Questa configurazione dello scanner viene eseguita nel profilo dello scanner o nelle impostazioni del repository con le impostazioni seguenti:
        - **Etichettare i file in base al contenuto**: **disattivato**
        - **Etichetta predefinita**: **None**
        - **Rietichettare i file**: **on** con la casella di controllo **Imponi etichetta predefinita** selezionata
    
    - Come per lo scanner del client classico, per impostazione predefinita lo scanner protegge i file di Office e i file PDF. È possibile proteggere altri tipi di file quando si usa un' [impostazione avanzata di PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).
    
    - Gli ID evento per i cicli dello scanner che iniziano e terminano non vengono scritti nel registro eventi di Windows. Usare invece il portale di Azure per queste informazioni.
    
    - Problema noto: le etichette nuove e rinominate non sono disponibili per la selezione come etichetta predefinita per le impostazioni del profilo dello scanner o del repository. Soluzioni alternative:
        - Per le nuove etichette: nella portale di Azure [aggiungere l'etichetta](../configure-policy-add-remove-label.md) che si vuole usare per i criteri globali o un criterio con ambito.
        - Per le etichette rinominate: chiudere e riaprire il portale di Azure.
    
    È possibile aggiornare gli scanner dal client di Azure Information Protection (versione classica). Dopo l'aggiornamento, che crea un nuovo database, lo scanner ripete l'analisi di tutti i file la prima volta che viene eseguito. Per istruzioni, vedere [aggiornamento dello scanner Azure Information Protection](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner) dalla guida dell'amministratore.
    
    Per altre informazioni, vedere il post di Blog sull'annuncio: [Unified Labeling AIP scanner Preview introduce la scalabilità orizzontale e altro ancora.](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)

- Il cmdlet di PowerShell [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) dispone di nuovi parametri (*AppID*, *AppSecret*, *TenantId*, *DelegatedUser*e *OnBehalfOf*) per quando si desidera assegnare etichette ai file in modo non interattivo e anche una nuova procedura per registrare un'app in Azure ad. Gli scenari di esempio includono lo scanner e gli script di PowerShell automatici per etichettare i documenti. Per istruzioni, vedere [come etichettare i file in modo non interattivo](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) dalla guida dell'amministratore.
    
    Si noti che *DelegatedUser* è un nuovo parametro dall'ultima versione di anteprima del client Unified Labeling e che le autorizzazioni API per l'app registrata sono state modificate di conseguenza.

- Nuova impostazione avanzata Criteri etichette di PowerShell per [modificare i tipi di file da proteggere](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

- Nuova impostazione avanzata Criteri etichette di PowerShell per [estendere le regole di migrazione delle etichette alle proprietà di SharePoint](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-sharepoint-properties).

- I tipi di informazioni riservate personalizzate corrispondenti vengono inviati a [Azure Information Protection Analytics](../reports-aip.md).

- L'etichetta applicata Visualizza il colore configurato per l'etichetta, se [è stato configurato un colore](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).

- Quando si aggiungono o si modificano le impostazioni di protezione in un'etichetta, il client riapplica l'etichetta con le impostazioni di protezione più recenti quando il documento viene salvato successivamente. Analogamente, lo scanner riapplica l'etichetta con le impostazioni di protezione più recenti quando il documento viene successivamente sottoposto a scansione in modalità di applicazione.

- [Supporto per i computer disconnessi](clientv2-admin-guide-customizations.md#support-for-disconnected-computers) esportando i file da un client e copiarli manualmente nel computer disconnesso. Si noti che questa configurazione è supportata per l'assegnazione di etichette con Esplora file, PowerShell e lo scanner. Questa configurazione non è supportata per l'assegnazione di etichette alle app di Office.

- Nuovo cmdlet [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)per raccogliere tutti i file di log da%LocalAppData%\Microsoft\MSIP\Logs e salvarli in un singolo file compresso con formato zip. Questo file può quindi essere inviato a supporto tecnico Microsoft se viene richiesto di inviare i file di log per consentire l'analisi di un problema segnalato.

**Correzioni**

- È possibile apportare modifiche a un file protetto tramite Esplora file e fare clic con il pulsante destro del mouse dopo la rimozione di una password per il file.

- È possibile aprire correttamente i file protetti in modo nativo nel Visualizzatore senza richiedere il [diritto di utilizzo](../configure-usage-rights.md#usage-rights-and-descriptions)Salva con nome, Esporta (Export).

- Le etichette e le impostazioni dei criteri si aggiornano come previsto senza dover eseguire [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)o eliminare manualmente la cartella%LocalAppData%\Microsoft\MSIP\mip.

**Modifiche aggiuntive**

- [Reimposta impostazioni](clientv2-admin-guide.md#more-information-about-the-reset-settings-option) ora elimina le cartelle\>%LocalAppData%\Microsoft\MSIP\mip\\ *\<ProcessName. exe* anziché la cartella%LocalAppData%\Microsoft\MSIP\mip\\ *\<ProcessName\>* \mip.

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) include ora l'ID contenuto per un documento protetto.

## <a name="version-22210"></a>Versione 2.2.21.0

**Rilasciata**: 09/03/2019

Supportato tramite 04/23/2020

**Correzioni**

- Quando si usa l'impostazione avanzata [OutlookDefaultLabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook) per impostare un'etichetta predefinita diversa per Outlook e l'etichetta specificata non include etichette secondarie per i criteri di etichetta, l'etichetta viene applicata correttamente.

- Quando il client di Azure Information Protection viene usato in un'app di Office, un utente con un account Active Directory non configurato per Single Sign-On viene richiesto di eseguire l'autenticazione per Azure Information Protection. Una volta eseguita l'autenticazione, lo stato del client passa correttamente a online, che consente la funzionalità di etichettatura.

## <a name="version-22190"></a>Versione 2.2.19.0

**Rilasciata**: 08/06/2019

Supportato tramite 03/03/2020

**Correzioni**

- Il client può scaricare il proprio criterio e visualizzare le etichette di riservatezza correnti. Questa correzione è necessaria dopo l'aggiornamento da una versione precedente e non sono stati configurati tipi di informazioni personalizzate nell'etichettatura Center.

- Miglioramenti di prestazioni e stabilità generali.

## <a name="version-22140"></a>Versione 2.2.14.0

**Rilasciata**: 07/15/2019

Supportato tramite 02/06/2020

**Nuove funzionalità:**

- Supporto per le [Impostazioni avanzate](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) configurate con PowerShell per la Centro sicurezza e conformità.
    
    Queste impostazioni avanzate supportano le seguenti personalizzazioni:
     - [Visualizza la barra di Information Protection nelle app Office](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [Esentare i messaggi di Outlook da un'etichetta obbligatoria](clientv2-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)
    - [Abilitare la classificazione consigliata in Outlook](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [Impostare un'etichetta predefinita diversa per Outlook](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [Disabilitare le autorizzazioni personalizzate in Esplora file](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [Aggiungere "Segnala un problema" per gli utenti](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [Disabilitare l'invio di informazioni riservate individuate nei documenti a Azure Information Protection Analytics](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [Invia corrispondenze del tipo di informazioni a Azure Information Protection Analytics](clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics)
    - [Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [Applicare una proprietà personalizzata quando viene applicata un'etichetta](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [Configurare un'etichetta per applicare la protezione S/MIME in Outlook](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Specificare un'etichetta secondaria predefinita per un'etichetta padre](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Specificare un colore per l'etichetta](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Supporto per le etichette configurate per le autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file. Per ulteriori informazioni, vedere la sezione [consentire agli utenti di assegnare autorizzazioni](/microsoft-365/compliance/encryption-sensitivity-labels#let-users-assign-permissions) nella documentazione di Office.

- Modifiche di PowerShell nel modulo AzureInformationProtection:
    - Nuovo cmdlet: [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -sostituisce New-RMSProtectionLicense per creare un criterio ad hoc per le autorizzazioni personalizzate
    - Nuovi parametri:
        -  *CustomPermissions* e *RemoveProtection* -aggiunta a [set-AIPFileLabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* -aggiunto a [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), da usare al posto del parametro *token* per le sessioni non interattive
        -  *Whatif* e *DiscoveryInfoTypes* -aggiunto a [set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), in modo che questo cmdlet possa essere eseguito in modalità di individuazione senza applicare le etichette
    - Cmdlet deprecati che si connettono direttamente a un servizio di protezione: Clear-RMSAuthentication, Get-Rmsfilestatus successivamente, Get-RMSServer, Get-RMSServerAuthentication, Get-RMSTemplate, Protect-RMSFile, set-RMSServerAuthentication, Unprotect-RMSFile


**Correzioni**

- Supporto per le [corrispondenze di contenuto](../reports-aip.md#content-matches-for-deeper-analysis) per Analytics e [set-AIPFileClassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps) con il parametro *DiscoveryInfoTypes* .

- Dopo aver modificato le impostazioni locali alternative in Windows, è comunque possibile applicare un'etichetta con protezione a un documento PDF.

- Quando un'etichetta viene rimossa dal contenuto, la protezione viene anche rimossa solo quando è stata applicata come parte della configurazione dell'etichetta. Se la protezione è stata applicata indipendentemente dall'etichetta, tale protezione viene mantenuta. Un utente, ad esempio, ha applicato autorizzazioni personalizzate a un file.

- Quando viene configurata l'assegnazione automatica di etichette, l'etichetta viene applicata la prima volta che un documento viene salvato.

- L'etichetta predefinita supporta le etichette secondarie.

## <a name="next-steps"></a>Passaggi successivi

Non si è certi che questo sia il client giusto da installare?  Vedere [scegliere il client di assegnazione di etichette da usare per i computer Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Per ulteriori informazioni sull'installazione e sull'utilizzo del client: 

- Per utenti: [Scaricare e installare il client](install-unifiedlabelingclient-app.md)

- Per gli amministratori: [Azure Information Protection guida dell'amministratore client per l'assegnazione di etichette unificata](clientv2-admin-guide.md)

