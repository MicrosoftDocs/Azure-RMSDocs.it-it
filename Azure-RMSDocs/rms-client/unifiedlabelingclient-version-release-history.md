---
title: Azure Information Protection le etichette unificate client-cronologia delle versioni & criteri di supporto
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7e3ac45d3665d342ddee3f1523b964c2f768db84
ms.sourcegitcommit: b7c4a6c3c343b53775cc4ffdecb966c32766dd6a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716080"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l'assegnazione di etichette unificata client-versione e criteri di supporto

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> **I clienti con supporto Microsoft esteso per Windows 7 e Office 2010 possono anche ottenere supporto Azure Information Protection per queste versioni. Per i dettagli completi, rivolgersi al contatto di supporto.*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

È possibile scaricare il Azure Information Protection Unified Labeling client dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).

Dopo un breve ritardo di genere in un paio di settimane, la versione di disponibilità generale più recente è inclusa anche nel catalogo di Microsoft Update con il nome di un prodotto **Microsoft Azure Information Protection**  >  **Microsoft Azure Information Protection client unificato**per l'assegnazione di etichette e la classificazione degli **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [upgradeing and maintaining the Azure Information Protection Unified Labeling client](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione disponibile a livello generale del client Azure Information Protection Unified Labeling è supportata per un massimo di sei mesi dopo il rilascio della versione GA successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versioni di disponibilità generale non più supportate:

|Versione client |Data di rilascio|
|--------------|-------------|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
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

## <a name="version-27960"></a>Versione 2.7.96.0 

Scanner unificato per l'assegnazione di etichette e versione client 2.7.96.0

**Rilasciato** 06/29/2020

**Nuove funzionalità per lo scanner Unified Labeling:**

- [Usare lo scanner per applicare etichette in base alle condizioni consigliate](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#prerequisites-for-the-azure-information-protection-scanner). I clienti AIP possono ora scegliere di implementare l'etichettatura automatica lato servizio. Questa funzionalità consente agli utenti finali di AIP di seguire sempre le raccomandazioni invece dello scenario precedente, che abilitava solo l'assegnazione automatica di etichette sul lato utente.

- [Informazioni sui file individuati in precedenza da scanner eliminati dal repository analizzato](https://docs.microsoft.com/azure/information-protection/reports-aip) Questi file eliminati non sono stati segnalati in precedenza in AIP Analytics e sono ora disponibili nel report di individuazione dello scanner.

- [Ottenere i report dallo scanner negli errori per applicare gli eventi di azione](https://docs.microsoft.com/azure/information-protection/reports-aip#friendly-schema-reference-for-event-functions). Usare i report per ottenere informazioni sugli eventi di azione non riusciti e individuare modi per evitare future occorrenze. 

- Introduzione dello strumento Analizzatore diagnostica di AIP scanner per il rilevamento e l'analisi degli errori comuni del scanner. Per iniziare a usare la diagnostica dello scanner AIP, [eseguire il nuovo cmdlet **Start-AIPScannerDiagnostics** ](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#troubleshooting-using-scanner-diagnostic-tool). 

- È ora possibile gestire e limitare l'utilizzo massimo della CPU nel computer dello scanner. Informazioni su come impedire il 100% di utilizzo della CPU e gestire l'utilizzo della CPU con [due nuove impostazioni avanzate **ScannerMaxCPU**e **ScannerMinCPU**](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#limit-cpu-consumption). 

- A questo punto è possibile configurare lo scanner Unified Labeling per ignorare i file specifici a seconda degli attributi di file. Definire l'elenco degli attributi di file che attiva un file da ignorare usando la nuova impostazione avanzata di **[ScannerFSAttributesToSkip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes)** .

**Nuove funzionalità per il client Unified Labeling:**

- Sono ora visualizzati [popup di giustificazione](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) per le modifiche apportate alle etichette predefinite nel client di etichettatura unificata.
    
- Integrazione più uniforme con i contrassegni di contenuto visivi applicati da Office. Per altre informazioni sulla configurazione dei contrassegni di contenuto nei documenti di Office, vedere [come configurare un'etichetta per i contrassegni visivi per Azure Information Protection](../configure-policy-markings.md).

- La nuova proprietà avanzata **WordShapeNameToRemove** consente la rimozione del contrassegno di contenuto nei documenti di Word creati da applicazioni di terze parti. Altre informazioni su come [identificare i nomi delle forme esistenti e definirli per la rimozione usando **WordShapeNameToRemove**](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#remove-headers-and-footers-from-other-labeling-solutions).

**Nuovi log di controllo generati per i file rimossi**

I log di controllo vengono ora generati ogni volta che lo scanner rileva che un file precedentemente sottoposto a scansione è stato rimosso.

Per altre informazioni, vedere:
- [Log di controllo rimossi dal file](../audit-logs.md#file-removed-audit-logs)
- [Reporting centralizzato per Azure Information Protection](../reports-aip.md)

**Imposizione di TLS 1.2**

A partire da questa versione del client di Azure Information Protection, sono supportate solo le versioni di TLS 1,2 o successive.
    
I clienti che dispongono di un programma di installazione di TLS che non supporta TLS 1,2 devono passare al programma di installazione che supporta TLS 1,2 per l'uso di criteri di Azure Information Protection, token, controllo e protezione e per ricevere comunicazioni basate su Azure Information Protection. 
    
Per ulteriori informazioni sui requisiti, vedere [firewall e requisiti dell'infrastruttura di rete](../requirements.md#firewalls-and-network-infrastructure).

**Correzioni e miglioramenti** 
- Miglioramenti di scanner SQL per:
    - Prestazioni
    - File con un numero elevato di tipi di informazioni
    
- Miglioramenti dell'analisi di SharePoint per:
    - Analisi delle prestazioni
    - File con caratteri speciali nel percorso
    - Librerie con numero di file di grandi dimensioni
    
    Per visualizzare una guida introduttiva per l'uso di Azure Information Protection con SharePoint, vedere [Guida introduttiva: trovare le informazioni riservate presenti nei file archiviati in locale](../quickstart-findsensitiveinfo.md).
        
- Notifiche utente migliorate per i criteri mancanti. Per ulteriori informazioni sui criteri di etichetta per il client Unified Labeling, vedere la pagina relativa ai [criteri delle etichette che possono](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do) essere eseguite nella documentazione Microsoft 365.

- Le [Etichette automatiche](../configure-policy-classification.md) vengono ora applicate in Excel per gli scenari in cui un utente inizia a chiudere un file senza salvarlo, così come avviene quando un utente salva attivamente un file.

- Le intestazioni e i piè di pagina vengono rimossi come previsto e non in ogni salvataggio del documento, quando viene configurata l'impostazione [ExternalContentMarkingToRemove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) .

- Le [variabili utente dinamiche](../configure-policy-markings.md#using-variables-in-the-text-string) sono ora visualizzate nei contrassegni visivi di un documento come previsto.

- Problema per cui è stata risolta solo la prima pagina di contenuto di un file PDF per l'applicazione delle regole di classificazione automatica e la classificazione automatica basata su tutto il contenuto nel file PDF ora procede come previsto. Per ulteriori informazioni sulla classificazione e l'assegnazione di etichette, vedere [domande frequenti sulla classificazione e l'assegnazione di etichette](https://docs.microsoft.com/azure/information-protection/faqs-infoprotect). 

- Quando vengono configurati più account di Exchange e il client Azure Information Protection Outlook è abilitato, i messaggi di posta elettronica vengono inviati dall'account secondario come previsto. Per ulteriori informazioni sulla configurazione del client Unified Labeling con Outlook, vedere [prerequisiti aggiuntivi per il Azure Information Protection client Unified Labeling](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

- Quando un documento con un'etichetta di riservatezza superiore viene trascinato e rilasciato in un messaggio di posta elettronica, il messaggio di posta elettronica riceve automaticamente l'etichetta di riservatezza superiore come previsto. Per ulteriori informazioni sull'assegnazione di etichette alle funzionalità client, vedere la [tabella di confronto dei client con etichetta](use-client.md#compare-the-labeling-clients-for-windows-computers).

- Le autorizzazioni personalizzate vengono ora applicate ai messaggi di posta elettronica come previsto, quando gli indirizzi di posta elettronica includono un apostrofo (') e un punto (.) Per ulteriori informazioni sulla configurazione del client Unified Labeling con Outlook, vedere [prerequisiti aggiuntivi per il Azure Information Protection client Unified Labeling](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

- Per impostazione predefinita, il proprietario NTFS di un file viene perso quando il file viene identificato dallo scanner di etichette unificato, da PowerShell o dall'estensione di Esplora file. A questo punto è possibile configurare il sistema per la conservazione del proprietario NTFS del file impostando la nuova impostazione avanzata **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** su **true**. 

    L'impostazione avanzata **UseCopyAndPreserveNTFSOwner** richiede una connessione di rete affidabile e a bassa latenza tra lo scanner e il repository analizzato.

## <a name="version-261110"></a>Versione 2.6.111.0 

**Rilasciato** 03/09/2020

Supportato tramite 12/29/2020

**Nuove funzionalità:**

- Versione di disponibilità generale dello [scanner](../deploy-aip-scanner.md)per esaminare ed etichettare i documenti negli archivi dati locali. 

- Correlate allo [scanner](../deploy-aip-scanner.md) :
    - [Individuazione più semplice in locale e nel sito secondario di SharePoint](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo#permission-users-to-scan-sharepoint-repositories). L'impostazione di ciascun sito specifico non è più necessaria. 
    - Proprietà avanzata per il [ridimensionamento del blocco SQL](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server) aggiunto.
    - Gli amministratori hanno ora la possibilità di [arrestare le analisi esistenti ed eseguire una nuova analisi](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan) se è stata apportata una modifica all'etichetta predefinita.
    - Per impostazione predefinita, lo scanner ora imposta la telemetria minima per le analisi più veloci e le dimensioni ridotte del log e i tipi di informazioni sono ora memorizzati nella cache nel database Altre informazioni sull' [ottimizzazione dello scanner](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner). 
    - Lo scanner supporta ora distribuzioni separate per il database e il servizio, mentre i diritti **sysadmin** sono necessari solo per la distribuzione del database.
    - Miglioramenti apportati alle prestazioni dello scanner. 

- Modifica del cmdlet di [PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell) **set-AIPFileLabel** per abilitare la rimozione della protezione da file PST, rar, 7zip e msg. Questa funzionalità è disabilitata per impostazione predefinita e deve essere attivata usando il cmdlet [set-LabelPolicy](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations) , come descritto [qui](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#enable-removal-of-protection-from-compressed-files).  

- È stata aggiunta la possibilità per gli amministratori di Azure Information Protection di controllare quando vengono usate le estensioni. Pfile per i file. Altre informazioni sulla [modifica dei tipi di file protetti](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect). 

- Aggiunto supporto del contrassegno visivo dinamico per le applicazioni e le variabili. Altre informazioni su come [configurare le etichette per i contrassegni visivi](https://docs.microsoft.com/azure/information-protection/configure-policy-markings). 

- Miglioramenti apportati ai [Suggerimenti per i criteri personalizzabili per le etichette automatiche e consigliate](use-client.md).   

- Aggiunto il supporto per la [funzionalità di assegnazione di etichette offline](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers) con le app di Office nel client Unified labeling.

**Correzioni**

- Nei casi in cui gli utenti hanno tentato di aprire i file TIFF protetti e i file TIFF creati da RightFax, i file TIFF sono ora aperti e rimangono stabili come previsto.  
- Sono stati risolti i danneggiamenti precedenti dei file txt e PDF protetti.
- È stata corretta l'assegnazione di etichette incoerenti tra **automatico** e **manuale** in log Analytics. 
- Sono stati risolti problemi di ereditarietà imprevisti identificati tra i nuovi messaggi di posta elettronica e l'ultimo messaggio di posta elettronica aperto.  
- La protezione dei file con estensione msg come. msg. Pfile ora funziona come previsto. 
- Le autorizzazioni di comproprietario aggiunte dalle impostazioni definite dall'utente di Office sono ora applicate come previsto. 
- Quando si immette la giustificazione del downgrade delle autorizzazioni, non è più possibile immettere il testo quando sono già selezionate altre opzioni. 


## <a name="version-25330"></a>Versione 2.5.33.0

**Rilasciata**: 10/23/2019

Supportato tramite 09/09/2020

**Nuove funzionalità:**

- Versione di anteprima dello [scanner](../deploy-aip-scanner.md)per ispezionare ed etichettare i documenti archivi dati locali. Con questa versione dello scanner:
    
    - Più scanner possono condividere lo stesso database di SQL Server quando si configurano gli scanner per l'uso dello stesso profilo dello scanner. Questa configurazione facilita la gestione di più scanner e comporta tempi di analisi più rapidi. Quando si usa questa configurazione, è sempre necessario attendere il completamento dell'installazione di uno scanner prima di installare un altro scanner con lo stesso profilo.
    
    - È necessario specificare un profilo quando si installa lo scanner e il database dello scanner è **denominato \<profile_name> AIPScannerUL_**. Il parametro *profile* è obbligatorio anche per set-AIPScanner.
    
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

- [Reimposta impostazioni](clientv2-admin-guide.md#more-information-about-the-reset-settings-option) ora elimina le \\ *\<ProcessName.exe\>* cartelle%LocalAppData%\Microsoft\MSIP\mip anziché la cartella%LocalAppData%\Microsoft\MSIP\mip \\ *\<ProcessName\>* \mip

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) include ora l'ID contenuto per un documento protetto.


## <a name="next-steps"></a>Passaggi successivi

Se non si è certi che l'etichetta unificata sia il client giusto da installare,  Vedere [scegliere il client di assegnazione di etichette da usare per i computer Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Per ulteriori informazioni sull'installazione e l'utilizzo del client Unified Labeling: 

- Per utenti: [Scaricare e installare il client](install-unifiedlabelingclient-app.md)

- Per gli amministratori: [Azure Information Protection guida dell'amministratore client per l'assegnazione di etichette unificata](clientv2-admin-guide.md)

