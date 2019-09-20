---
title: Azure Information Protection le etichette unificate client-cronologia delle versioni & criteri di supporto
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/19/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8934e23594ba51248e691ce2e52d69308cb320e5
ms.sourcegitcommit: d5f046e34de0ad79b64d3f412999145b7d097e75
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/19/2019
ms.locfileid: "71127547"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l'assegnazione di etichette unificata client-versione e criteri di supporto

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


È possibile scaricare il Azure Information Protection Unified Labeling client dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Dopo un breve ritardo di in genere un paio di settimane, la versione di disponibilità generale più recente è inclusa anche nel catalogo di Microsoft Update con il nome del prodotto **Microsoft Azure Information Protection** > **informazioni Microsoft Azure Protezione Unified Labeling client**e la classificazione degli **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [upgradeing and maintaining the Azure Information Protection Unified Labeling client](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione disponibile a livello generale del client Azure Information Protection Unified Labeling è supportata per un massimo di sei mesi dopo il rilascio della versione GA successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

> [!NOTE]
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per visualizzare le novità o le modifiche apportate a una versione supportata del client Azure Information Protection Unified Labeling per Windows. La versione più recente è elencata per prima. Il formato della data usato in questa pagina è *mese/giorno/anno*.

> [!NOTE]
> Le correzioni secondarie non sono elencate, quindi se si verifica un problema con il client di etichettatura unificata, è consigliabile verificare se è stato risolto con la versione GA più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

Il client sta sostituendo il client di Azure Information Protection (classico). Per confrontare caratteristiche e funzionalità con il client classico, vedere [confrontare i client](use-client.md#compare-the-clients).

## <a name="versions-later-than-22210"></a>Versioni successive a 2.2.21.0

Se si dispone di una versione 2 del client successiva a 2.2.21.0, si tratta di una build di anteprima a scopo di test e valutazione.

**Data di rilascio**: 09/17/2019

**Nuove funzionalità:**

- Supporto per lo [scanner](../deploy-aip-scanner.md), per ispezionare ed etichettare i documenti archivi dati locali. Con questa versione dello scanner:
    
    - Più scanner possono condividere lo stesso database di SQL Server quando si configurano gli scanner per l'uso dello stesso profilo dello scanner. Questa configurazione facilita la gestione di più scanner e comporta tempi di analisi più rapidi. Quando si usa questa configurazione, è sempre necessario attendere il completamento dell'installazione di uno scanner prima di installare un altro scanner con lo stesso profilo.
    
    - È necessario specificare un profilo quando si installa lo scanner e il database dello scanner è **denominato\<AIPScannerUL_ profile_name >** . Il parametro *profile* è obbligatorio anche per set-AIPScanner.
    
    - È possibile impostare un'etichetta predefinita su tutti i documenti, anche se i documenti sono già etichettati. Nel profilo scanner o nelle impostazioni del repository, impostare l'opzione **rietichettare i file** **su on** con la nuova casella di controllo **Imponi etichetta predefinita** selezionata.
    
    - È possibile rimuovere le etichette esistenti da tutti i documenti e questo Act include la rimozione della protezione se è stata precedentemente applicata da un'etichetta. La protezione applicata indipendentemente da un'etichetta viene mantenuta. Questa configurazione dello scanner viene eseguita nel profilo dello scanner o nelle impostazioni del repository con le impostazioni seguenti:
        - **Etichetta i file in base al contenuto**: **Disattivato**
        - **Etichetta predefinita**: **Nessuno**
        - **Applica una nuova etichetta ai file**: **In** con la casella di controllo **Applica etichetta predefinita** selezionata
    
    - Come per lo scanner del client classico, lo scanner protegge i file di Office e i file PDF. Attualmente, non è possibile configurare altri tipi di file da proteggere con questa versione dello scanner.
    
    - Problema noto: Le etichette nuove e rinominate non sono disponibili per la selezione come etichetta predefinita per il profilo dello scanner o le impostazioni del repository. Soluzioni alternative
        - Per le nuove etichette: Nella portale di Azure [aggiungere l'etichetta](../configure-policy-add-remove-label.md) che si vuole usare per i criteri globali o un criterio con ambito.
        - Per le etichette rinominate: Nella portale di Azure passare a **Azure Information Protection** > **Gestisci** > **etichetta unificata**e selezionare **pubblica**.
    
    È possibile aggiornare gli scanner dal client di Azure Information Protection (versione classica). Dopo l'aggiornamento, che crea un nuovo database, lo scanner ripete l'analisi di tutti i file la prima volta che viene eseguito. Per istruzioni, vedere [aggiornamento dello scanner Azure Information Protection](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner) dalla guida dell'amministratore.
    
    Per ulteriori informazioni, vedere il post di Blog relativo all'annuncio: [Unified Labeling AIP scanner Preview introduce la scalabilità orizzontale e altro ancora.](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)

- Il cmdlet di PowerShell [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) include nuovi parametri per le etichette dei [file in modo non interattivo](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)e una [nuova procedura per registrare un'app in Azure ad](clientv2-admin-guide-powershell.md#to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication---preview-client). Gli scenari di esempio includono lo scanner e gli script di PowerShell automatici per etichettare i documenti.

- I tipi di informazioni riservate personalizzate corrispondenti vengono inviati a [Azure Information Protection Analytics](../reports-aip.md).

- L'etichetta applicata Visualizza il colore configurato per l'etichetta, se [è stato configurato un colore](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).

- Quando si aggiungono o si modificano le impostazioni di protezione in un'etichetta, il client riapplica l'etichetta con le impostazioni di protezione più recenti quando il documento viene salvato successivamente. Analogamente, lo scanner riapplica l'etichetta con le impostazioni di protezione più recenti quando il documento viene successivamente sottoposto a scansione in modalità di applicazione.

- Nuovo cmdlet [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)per raccogliere tutti i file di log da%LocalAppData%\Microsoft\MSIP\Logs e salvarli in un singolo file compresso con formato zip. Questo file può quindi essere inviato a supporto tecnico Microsoft se viene richiesto di inviare i file di log per consentire l'analisi di un problema segnalato.

**Correzioni**

- È possibile apportare modifiche a un file protetto tramite Esplora file e fare clic con il pulsante destro del mouse dopo la rimozione di una password per il file.


## <a name="version-22210"></a>Versione 2.2.21.0

**Data di rilascio**: 09/03/2019

**Correzioni**

- Quando si usa l'impostazione avanzata [OutlookDefaultLabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook) per impostare un'etichetta predefinita diversa per Outlook e l'etichetta specificata non include etichette secondarie per i criteri di etichetta, l'etichetta viene applicata correttamente.

- Quando il client di Azure Information Protection viene usato in un'app di Office, un utente con un account Active Directory non configurato per Single Sign-On viene richiesto di eseguire l'autenticazione per Azure Information Protection. Una volta eseguita l'autenticazione, lo stato del client passa correttamente a online, che consente la funzionalità di etichettatura.

## <a name="version-22190"></a>Versione 2.2.19.0

**Data di rilascio**: 08/06/2019

Supportato tramite 03/03/2020

**Correzioni**

- Il client può scaricare il proprio criterio e visualizzare le etichette di riservatezza correnti. Questa correzione è necessaria dopo l'aggiornamento da una versione precedente e non sono stati configurati tipi di informazioni personalizzate nell'etichettatura Center.

- Miglioramenti di prestazioni e stabilità generali.

## <a name="version-22140"></a>Versione 2.2.14.0

**Data di rilascio**: 07/15/2019

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
    - [Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [Applicare una proprietà personalizzata quando viene applicata un'etichetta](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [Configurare un'etichetta per applicare la protezione S/MIME in Outlook](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Specificare un'etichetta secondaria predefinita per un'etichetta padre](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Specificare un colore per l'etichetta](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Supporto per le etichette configurate per le autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file. Per ulteriori informazioni, vedere la sezione [consentire agli utenti di assegnare autorizzazioni](/Office365/SecurityCompliance/encryption-sensitivity-labels#let-users-assign-permissions) nella documentazione di Office.

- Modifiche di PowerShell nel modulo AzureInformationProtection:
    - Nuovo cmdlet: [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -sostituisce New-RMSProtectionLicense per creare un criterio ad hoc per le autorizzazioni personalizzate
    - Nuovi parametri:
        -  *CustomPermissions* e *RemoveProtection* -aggiunta a [set-AIPFileLabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* -aggiunto a [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), da usare al posto del parametro *token* per le sessioni non interattive
        -  *Whatif* e *DiscoveryInfoTypes* -aggiunto a [set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), in modo che questo cmdlet possa essere eseguito in modalità di individuazione senza applicare le etichette
    - Cmdlet deprecati che si connettono direttamente a un servizio di protezione: Clear-RMSAuthentication, Get-Rmsfilestatus successivamente, Get-RMSServer, Get-RMSServerAuthentication, Get-RMSTemplate, Protect-RMSFile, set-RMSServerAuthentication, Unprotect-RMSFile


**Correzioni**

- Supporto per le corrispondenze di [contenuto](../reports-aip.md#content-matches-for-deeper-analysis) per Analytics e [set-AIPFileClassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps) con il parametro *DiscoveryInfoTypes* .

- Dopo aver modificato le impostazioni locali alternative in Windows, è comunque possibile applicare un'etichetta con protezione a un documento PDF.

- Quando un'etichetta viene rimossa dal contenuto, la protezione viene anche rimossa solo quando è stata applicata come parte della configurazione dell'etichetta. Se la protezione è stata applicata indipendentemente dall'etichetta, tale protezione viene mantenuta. Un utente, ad esempio, ha applicato autorizzazioni personalizzate a un file.

- Quando viene configurata l'assegnazione automatica di etichette, l'etichetta viene applicata la prima volta che un documento viene salvato.

- L'etichetta predefinita supporta le etichette secondarie.

## <a name="version-207790"></a>Versione 2.0.779.0

**Data di rilascio**: 05/01/2019

Supportato tramite 02/15/2020

Questa versione include una singola correzione per risolvere un problema di race condition in cui talvolta non vengono visualizzate etichette nelle app di Office o in Esplora file.

## <a name="version-207780"></a>Versione 2.0.778.0

**Data di rilascio**: 04/16/2019

Supportato tramite 11/01/2019

Questa prima versione disponibile a livello generale del client di Azure Information Protection Unified Labeling per Windows supporta le funzionalità seguenti: 

- Aggiornamento dal client Azure Information Protection.

- Assegnazione di etichette manuale, automatica e consigliata: Per altre informazioni sulla configurazione dell'assegnazione di etichette automatica e consigliata per questo client, vedere [Applicare automaticamente un'etichetta di riservatezza al contenuto](/Office365/SecurityCompliance/apply-sensitivity-label-automatically).

- Esplora file, azioni con il pulsante destro del mouse per classificare e proteggere i file, rimuovere la protezione e applicare autorizzazioni personalizzate.

- Un visualizzatore per file di testo e di immagine protetti, file PDF protetti e file protetti in modo generico.

- Comandi di PowerShell seguenti per le seguenti operazioni:
    - [Impostare o rimuovere un'etichetta in un documento](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Applicare un'etichetta a un documento dopo averne esaminato il contenuto](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Leggere le informazioni dell'etichetta applicate a un documento](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [Eseguire l'autenticazione per supportare le sessioni automatiche di PowerShell](/powershell/module/azureinformationprotection/set-aipauthentication)

- Controllo dei dati e del supporto per l'individuazione di endpoint per la creazione di report centrali usando [Azure Information Protection Analytics](../reports-aip.md).

- Le impostazioni seguenti per etichette e criteri:
    - Contrassegno visivo (intestazioni, piè di pagina, filigrane)
    - Assegnazione di etichette predefinita-attualmente limitata alle etichette senza etichette secondarie
    - Etichette che applicano Non inoltrare e vengono visualizzate solo in Outlook
    - Richieste di giustificazione se gli utenti abbassano il livello di classificazione o rimuovono un'etichetta
    - Colori per le etichette

- Aggiornamento di criteri dai centri di amministrazione:
    - Ogni volta che viene avviata un'app Office e ogni 4 ore
    - Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella
    - Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione

- Una finestra di dialogo Guida e commenti che include impostazioni per il ripristino e l'esportazione di log.


## <a name="next-steps"></a>Passaggi successivi

Per informazioni dettagliate, vedere le [tabelle di confronto](use-client.md#compare-the-clients).

Per ulteriori informazioni sull'installazione e sull'utilizzo del client: 

- Per gli utenti: [Scaricare e installare il client](install-unifiedlabelingclient-app.md)

- Per gli amministratori: [Guida dell'amministratore client per l'assegnazione di etichette unificata Azure Information Protection](clientv2-admin-guide.md)

