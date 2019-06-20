---
title: Azure Information Protection unified client l'assegnazione di etichette - criterio di cronologia e supporto della versione
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: ea360e880e4b6bf0dc4c2f362a82ffa6d21a6c3b
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236811"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection unified client - versione l'assegnazione di etichette cronologia delle versioni e criteri di supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


È possibile scaricare il client di assegnazione di etichette unificato di Azure Information Protection dal [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Dopo un breve intervallo di in genere un paio di settimane, la versione di disponibilità generale più recente è anche inclusa in Microsoft Update Catalog con il nome del prodotto **Microsoft Azure Information Protection**  >  **Microsoft Client Azure Information Protection Unified l'assegnazione di etichette**e la classificazione dei **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [l'aggiornamento e la gestione di Azure Information Protection unified client l'assegnazione di etichette](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione di disponibilità generale (GA) del client Azure Information Protection unified imprevisto delle etichette è supportato per un massimo di sei mesi dopo il rilascio della versione disponibile a livello generale successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

> [!NOTE]
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per vedere cosa è supportato per la versione con disponibilità generale del client Azure Information Protection unified imprevisto delle etichette.

Il client installa un componente aggiuntivo di Office per i computer Windows, un'estensione per Esplora File e un modulo di PowerShell. Questo client ha gli stessi [prerequisiti](../requirements.md) del client Azure Information Protection che scarica i criteri da Azure.

Per confrontare caratteristiche e funzionalità con il client Azure Information Protection, vedere [confrontare i client](use-client.md#compare-the-clients).

## <a name="versions-later-than-207790"></a>Versioni successive alla 2.0.779.0

**Data di rilascio**: 06/20/2019

Se si dispone di una versione 2 del client successiva a quella 2.0.779.0, è una build di anteprima per scopi di test e valutazione. 

**Nuove funzionalità:**

- Supporto per [impostazioni avanzate](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) configurato con PowerShell per il Centro sicurezza e conformità.
    
    Queste impostazioni avanzate supportano le seguenti personalizzazioni:
     - [Visualizza la barra di Information Protection nelle app Office](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [Abilitare la classificazione consigliata in Outlook](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [Impostare un'etichetta predefinita diversa per Outlook](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [Impostare un'etichetta predefinita diversa per Outlook](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [Disabilitare le autorizzazioni personalizzate in Esplora File](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [Aggiungere "Segnala un problema" per gli utenti](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [Abilitare gli strumenti di analisi di Azure Information Protection per individuare informazioni riservate nei documenti](clientv2-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)
    - [Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [Applicare una proprietà personalizzata quando viene applicata un'etichetta](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [Configurare un'etichetta per applicare la protezione S/MIME in Outlook](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Specificare un'etichetta secondaria predefinito per un'etichetta padre](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Specificare un colore per l'etichetta](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Supporto per le etichette configurate per le autorizzazioni definite dall'utente per Word, Excel, PowerPoint e File Explorer:
    - Se sono presenti etichette con questa configurazione dal portale di Azure, sono ora supportati dal client di assegnazione di etichette unificato anche se non è attualmente disponibile nessuna configurazione equivalente nelle interfacce di amministrazione.
    - Quando un utente seleziona un'etichetta con questa configurazione, viene chiesto selezionare utenti e le impostazioni di protezione per il documento.

- Modifiche di PowerShell del modulo AzureInformationProtection:
    - Nuovo cmdlet: [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -sostituisce New-RMSProtectionLicense per creare un criterio ad hoc per le autorizzazioni personalizzate
    - Nuovi parametri:
        -  *CustomPermissions* e *RemoveProtection* - aggiunta a [Set-AIPFileLabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* - aggiunto alla [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), per essere usato al posto del *Token* parametro per le sessioni non interattive
        -  *WhatIf* e *DiscoveryInfoTypes* - aggiunto alla [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), in modo che questo cmdlet è possibile eseguire in modalità di individuazione senza applicare le etichette
    - Cmdlet deprecati: Clear-RMSAuthentication, Get-RMSFileStatus, Get-RMSServer, Get-RMSServerAuthentication, Get-RMSTemplate, Protect-RMSFile, Set-RMSServerAuthentication, Unprotect-RMSFile


**Correzioni:**

- Quando viene configurato l'assegnazione automatica di etichette, l'etichetta applica la prima volta un documento viene salvato.

## <a name="version-207790"></a>Versione 2.0.779.0

**Data di rilascio**: 05/01/2019

Questa versione include una singola correzione per risolvere un problema di race condition in cui in alcuni casi, non le etichette visualizzate nell'app di Office o Esplora File.

## <a name="version-207780"></a>Versione 2.0.778.0

**Data di rilascio**: 04/16/2019

Supportato tramite 11/01/2019

Questa prima versione di disponibilità generale del client di assegnazione di etichette unificata di Azure Information Protection per Windows supporta le funzionalità seguenti: 

- Aggiornamento dal client Azure Information Protection.

- Assegnazione di etichette manuale, automatica e consigliata: Per altre informazioni sulla configurazione dell'assegnazione di etichette automatica e consigliata per questo client, vedere [Applicare automaticamente un'etichetta di riservatezza al contenuto](/Office365/SecurityCompliance/apply_sensitivity_label_automatically).

- Esplora file, azioni con il pulsante destro del mouse per classificare e proteggere i file, rimuovere la protezione e applicare autorizzazioni personalizzate.

- Un visualizzatore per file di testo e di immagine protetti, file PDF protetti e file protetti in modo generico.

- Comandi di PowerShell seguenti per le seguenti operazioni:
    - [Impostare o rimuovere un'etichetta in un documento](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Applicare un'etichetta a un documento dopo averne esaminato il contenuto](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Leggere le informazioni dell'etichetta applicate a un documento](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [Eseguire l'autenticazione per supportare le sessioni automatiche di PowerShell](/powershell/module/azureinformationprotection/set-aipauthentication)

- Il supporto di individuazione dati e l'endpoint per il reporting centralizzato tramite del controllo [analitica di Azure Information Protection](../reports-aip.md).

- Le impostazioni seguenti per etichette e criteri:
    - Contrassegno visivo (intestazioni, piè di pagina, filigrane)
    - Impostazione predefinita l'assegnazione di etichette - è attualmente limitato alle etichette senza le etichette secondarie
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

Per altre informazioni sull'installazione e l'utilizzo di questo client: 

- Per gli utenti: [Scaricare e installare il client](install-unifiedlabelingclient-app.md)

- Per gli amministratori: [Azure Information Protection unified Guida dell'amministratore client l'assegnazione di etichette](clientv2-admin-guide.md)

