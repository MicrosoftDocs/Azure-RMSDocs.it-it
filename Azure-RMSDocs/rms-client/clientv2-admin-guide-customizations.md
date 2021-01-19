---
title: Configurazioni personalizzate-Azure Information Protection client per l'assegnazione di etichette unificata
description: Informazioni sulla personalizzazione del client di Azure Information Protection Unified Labeling per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/18/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 553646119c5e83bbc475d77ab35a83ce5866e858
ms.sourcegitcommit: d2fdba748daf47ee9aeadbdf3ce154ef399eadaf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2021
ms.locfileid: "98569096"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client di etichettatura unificata di Azure Information Protection

<!-- Notes for contributors: In this file, you can add new settings on at the bottom of the page to simplify the content editing. However, remember to add the xref by setting AND by feature to the reference sections at the top. 

There are two types of reference sections - the legacy table by setting name, and a newer section of reference by feature type. This newer section helps admins understand and configure settings that are relevant to eachother, possibly in a sort of a flow. 

FUTURE task - reorganize this topic by feature type so that admins can read related settings together. NOT recommended to reorganize this page into sub-pages as there are too many xrefs out there to this page and you'll need a lot of redirects. Additionally, users might just search for their setting or text on a single page. It would help to have related settings documented one right after the other to help with scrolling. -->

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Pertinente per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'amministratore del client classico](client-admin-guide-customizations.md). *

Usare le informazioni seguenti per le configurazioni avanzate necessarie per scenari o utenti specifici quando si gestisce il client di assegnazione unificata di AIP.

> [!NOTE]
> Per queste impostazioni è necessario modificare il registro di sistema o specificare impostazioni avanzate. Le impostazioni avanzate usano [Office 365 Security & Compliance Center PowerShell](/powershell/exchange/office-365-scc/office-365-scc-powershell).
> 



## <a name="configuring-advanced-settings-for-the-client-via-powershell"></a>Configurazione delle impostazioni avanzate per il client tramite PowerShell

Usare il Microsoft 365 Security & Compliance Center PowerShell per configurare le impostazioni avanzate per la personalizzazione dei criteri etichette e delle etichette. 

In entrambi i casi, dopo la [connessione a Office 365 Security & Compliance Center PowerShell](/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell), specificare il parametro **AdvancedSettings** con l'identità (nome o GUID) del criterio o dell'etichetta, con le coppie chiave/valore in una [tabella hash](/powershell/module/microsoft.powershell.core/about/about_hash_tables). 

Per rimuovere un'impostazione avanzata, usare la stessa sintassi del parametro **AdvancedSettings** , ma specificare un valore di stringa null. 

> [!IMPORTANT]
> Non usare spazi vuoti nei valori stringa. Le stringhe bianche in questi valori stringa impediranno l'applicazione delle etichette.

Per altre informazioni, vedere:

- [Sintassi delle impostazioni avanzate dei criteri etichette](#label-policy-advanced-settings-syntax)
- [Etichetta sintassi impostazioni avanzate](#label-advanced-settings-syntax)
- [Verifica delle impostazioni avanzate correnti](#checking-your-current-advanced-settings)
- [Esempi per l'impostazione di impostazioni avanzate](#examples-for-setting-advanced-settings)
- [Specifica del criterio etichetta o dell'identità dell'etichetta](#specifying-the-label-policy-or-label-identity)
- [Ordine di precedenza-come vengono risolte le impostazioni in conflitto](#order-of-precedence---how-conflicting-settings-are-resolved)
- [Riferimenti a impostazioni avanzate](#advanced-setting-references)
### <a name="label-policy-advanced-settings-syntax"></a>Sintassi delle impostazioni avanzate dei criteri etichette

Un esempio di impostazione avanzata dei criteri di etichetta è l'impostazione per visualizzare la barra di Information Protection nelle app di Office.

**Per un singolo valore stringa**, usare la sintassi seguente:

```PowerShell
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}
```

**Per un valore di stringa multipla per la stessa chiave**, usare la sintassi seguente:

```PowerShell
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

### <a name="label-advanced-settings-syntax"></a>Etichetta sintassi impostazioni avanzate

Un esempio di impostazione avanzata etichetta è l'impostazione per specificare il colore di un'etichetta.

**Per un singolo valore stringa**, usare la sintassi seguente:

```PowerShell
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}
```

**Per un valore di stringa multipla per la stessa chiave**, usare la sintassi seguente:

```PowerShell
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```



### <a name="checking-your-current-advanced-settings"></a>Verifica delle impostazioni avanzate correnti

Per verificare che le impostazioni avanzate correnti siano attive, eseguire i comandi seguenti:

**Per verificare le impostazioni avanzate dei *criteri di etichetta***, usare la sintassi seguente:

Per un criterio etichetta denominato **globale**:

```PowerShell
(Get-LabelPolicy -Identity Global).settings
```

**Per controllare le impostazioni avanzate dell' *etichetta***, usare la sintassi seguente:

Per un'etichetta denominata **public**:

```powershell
(Get-Label -Identity Public).settings
```

### <a name="examples-for-setting-advanced-settings"></a>Esempi per l'impostazione di impostazioni avanzate

**Esempio 1**: impostare un'impostazione avanzata dei criteri per le etichette per un singolo valore stringa:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

**Esempio 2**: impostare un'impostazione avanzata etichetta per un valore stringa singolo:

```PowerShell
Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}
```

**Esempio 3**: impostare un'impostazione avanzata etichetta per più valori stringa:

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

**Esempio 4**: rimuovere un'impostazione avanzata dei criteri di etichetta specificando un valore stringa null:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}
```

### <a name="specifying-the-label-policy-or-label-identity"></a>Specifica del criterio etichetta o dell'identità dell'etichetta

Trovare il nome dei criteri di etichetta per il parametro **Identity** di PowerShell è semplice perché nell'interfaccia di amministrazione di assegnazione delle etichette è presente un solo nome di criterio.

Tuttavia, per le etichette, i centri di amministrazione delle etichette mostrano sia il **nome** che il valore del **nome visualizzato** . In alcuni casi, questi valori saranno uguali, ma potrebbero essere diversi. Per configurare le impostazioni avanzate per le etichette, utilizzare il valore **nome** .

Per identificare l'etichetta nell'immagine seguente, ad esempio, usare la sintassi seguente nel comando di PowerShell: `-Identity "All Company"` :

![Usare "Name" invece di "nome visualizzato" per identificare un'etichetta di riservatezza](../media/labelname_scc.png)

Se si preferisce specificare il **GUID** dell'etichetta, questo valore *non* viene visualizzato nell'interfaccia di amministrazione di assegnazione delle etichette. Usare il comando [get-Label](/powershell/module/exchange/get-label) per trovare questo valore, come indicato di seguito:

```PowerShell
Get-Label | Format-Table -Property DisplayName, Name, Guid
```

Per ulteriori informazioni sull'assegnazione di etichette ai nomi e ai nomi visualizzati:

- **Nome** è il nome originale dell'etichetta ed è univoco in tutte le etichette. 

    Questo valore rimane invariato anche se il nome dell'etichetta è stato modificato in un secondo momento. Per le etichette di riservatezza di cui è stata eseguita la migrazione da Azure Information Protection, è possibile che venga visualizzato l'ID etichetta originale del portale di Azure.

- **Nome visualizzato** è il nome attualmente visualizzato agli utenti per l'etichetta e non è necessario che sia univoco in tutte le etichette. 

    Ad esempio, potrebbe essere presente un nome visualizzato di **tutti i dipendenti** per un'etichetta secondaria sotto l'etichetta **riservata** e un altro nome visualizzato di  **tutti i dipendenti** per un'etichetta secondaria sotto l'etichetta **riservatezza elevata** . Queste etichette secondarie visualizzano entrambi lo stesso nome, ma non hanno la stessa etichetta e hanno impostazioni diverse.

### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Ordine di precedenza-come vengono risolte le impostazioni in conflitto

È possibile usare i centri di amministrazione per configurare le impostazioni dei criteri di etichetta seguenti:

- **Per impostazione predefinita, applicare questa etichetta ai documenti e ai messaggi di posta elettronica**

- **Gli utenti devono fornire la giustificazione per rimuovere un'etichetta o un'etichetta di classificazione inferiore**

- **Richiedi agli utenti di applicare un'etichetta al messaggio di posta elettronica o al documento**

- **Fornire agli utenti un collegamento a una pagina della Guida personalizzata**

Quando per un utente sono configurati più criteri di etichetta, ognuno con impostazioni di criteri potenzialmente diverse, l'ultima impostazione dei criteri viene applicata in base all'ordine dei criteri nell'interfaccia di amministrazione. Per ulteriori informazioni, vedere [priorità dei criteri delle etichette (ordine degli ordini)](/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters)

Le impostazioni avanzate dei criteri di etichetta vengono applicate usando la stessa logica, usando l'ultima impostazione dei criteri.

## <a name="advanced-setting-references"></a>Riferimenti a impostazioni avanzate

Le sezioni seguenti illustrano le impostazioni avanzate disponibili per le etichette e i criteri di etichetta:

- [Guida di riferimento alle impostazioni avanzate per funzionalità](#advanced-setting-reference-by-feature)
- [Riferimento alle impostazioni avanzate dei criteri etichette](#label-policy-advanced-setting-reference)
- [Riferimento alle impostazioni avanzate etichetta](#label-advanced-setting-reference)
### <a name="advanced-setting-reference-by-feature"></a>Guida di riferimento alle impostazioni avanzate per funzionalità

Le sezioni seguenti elencano le impostazioni avanzate descritte in questa pagina per integrazione di prodotti e funzionalità:

|Funzionalità  |Impostazioni avanzate  |
|---------|---------|
|**Impostazioni di Outlook e posta elettronica**     | - [Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook) <br> - [Personalizzare i messaggi popup di Outlook](#customize-outlook-popup-messages) <br>- [Abilita classificazione consigliata in Outlook](#enable-recommended-classification-in-outlook)<br> - [Esentare i messaggi di Outlook da un'etichetta obbligatoria](#exempt-outlook-messages-from-mandatory-labeling) <br>- [Per i messaggi di posta elettronica con allegati, applicare un'etichetta che corrisponda alla classificazione più elevata di tali allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)<br>- [Espandi elenchi di distribuzione di Outlook durante la ricerca di destinatari di posta elettronica](#expand-outlook-distribution-lists-when-searching-for-email-recipients) <br>- [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) <br>- [Impedisci problemi di prestazioni di Outlook con messaggi di posta elettronica S/MIME](#prevent-outlook-performance-issues-with-smime-emails)   <br>- [Imposta un'etichetta predefinita diversa per Outlook](#set-a-different-default-label-for-outlook)     |
|**Impostazioni di PowerPoint** | - [Evitare di rimuovere forme da PowerPoint che contengono testo specificato e non sono intestazioni/piè di pagina](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers)<br>- [Rimuovere in modo esplicito i contrassegni di contenuto esterno dall'interno dei layout personalizzati di PowerPoint](#extend-external-marking-removal-to-custom-layouts)<br>- [Rimuovere tutte le forme di un nome di forma specifico dalle intestazioni e dai piè di pagina, anziché rimuovere forme per testo all'interno della forma](#remove-all-shapes-of-a-specific-shape-name)  |
|**Impostazioni di Esplora file**     | - [Visualizza sempre le autorizzazioni personalizzate per gli utenti in Esplora file](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) <br>  - [Disabilitare le autorizzazioni personalizzate in Esplora file](#disable-custom-permissions-in-file-explorer)      |
|**Impostazioni di miglioramento delle prestazioni**     | - [Limita utilizzo CPU](#limit-cpu-consumption) <br>- [Limitare il numero di thread usati dallo scanner](#limit-the-number-of-threads-used-by-the-scanner) <br>- [Impedisci problemi di prestazioni di Outlook con messaggi di posta elettronica S/MIME](#prevent-outlook-performance-issues-with-smime-emails)        |
|**Impostazioni per le integrazioni con altre soluzioni di assegnazione di etichette**     | - [Eseguire la migrazione di etichette da isole sicure e altre soluzioni di assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions) <br> - [Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione di etichette](#remove-headers-and-footers-from-other-labeling-solutions)    |
|**Impostazioni di AIP Analytics**     |   - [Disabilitare l'invio di dati di controllo a Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) <br>- [Invia corrispondenze del tipo di informazioni a Azure Information Protection Analytics](#send-information-type-matches-to-azure-information-protection-analytics)      |
|**Impostazioni generali**     | - [Aggiungere "segnala un problema" per gli utenti](#add-report-an-issue-for-users) <br>- [Applicare una proprietà personalizzata quando viene applicata un'etichetta](#apply-a-custom-property-when-a-label-is-applied) <br>-  [Modificare il livello di registrazione locale](#change-the-local-logging-level) <br>- [Modificare i tipi di file da proteggere](#change-which-file-types-to-protect)<br>- [Configurare i timeout di SharePoint](#configure-sharepoint-timeouts)<br>- [Personalizzare i testi della richiesta di giustificazione per le etichette modificate](#customize-justification-prompt-texts-for-modified-labels)<br>-  [Visualizzare la barra di Information Protection nelle app di Office](#display-the-information-protection-bar-in-office-apps) <br>- [Abilitare la rimozione della protezione dai file compressi](#enable-removal-of-protection-from-compressed-files) <br>-  [Mantieni i proprietari NTFS durante l'assegnazione di etichette (anteprima pubblica)](#preserve-ntfs-owners-during-labeling-public-preview) <br> -  [Rimuovere "non ora" per i documenti quando si usa l'etichettatura obbligatoria](#remove-not-now-for-documents-when-you-use-mandatory-labeling) <br>-  [Ignora o ignora i file durante le analisi a seconda degli attributi di file](#skip-or-ignore-files-during-scans-depending-on-file-attributes) <br>-  [Specificare un colore per l'etichetta](#specify-a-color-for-the-label)<br>-  [Specificare un'etichetta secondaria predefinita per un'etichetta padre](#specify-a-default-sublabel-for-a-parent-label)<br>-  [Supporto per la modifica \<EXT> . Da PFILE a P\<EXT>](#additionalpprefixextensions)  <br>-  [Supporto per i computer disconnessi](#support-for-disconnected-computers)     <br>-  [Attivare la classificazione per l'esecuzione continua in background](#turn-on-classification-to-run-continuously-in-the-background) <br>- [Disattiva le funzionalità di rilevamento dei documenti (anteprima pubblica)](#turn-off-document-tracking-features-public-preview)   |
|     |         |


### <a name="label-policy-advanced-setting-reference"></a>Riferimento alle impostazioni avanzate dei criteri etichette

Usare il parametro *AdvancedSettings* con [New-LabelPolicy](/powershell/module/exchange/policy-and-compliance/new-labelpolicy) e [set-LabelPolicy](/powershell/module/exchange/policy-and-compliance/set-labelpolicy) per definire le impostazioni seguenti:

|Impostazione|Scenario e istruzioni|
|----------------|---------------|
|**AdditionalPPrefixExtensions**|[Supporto per la modifica \<EXT> . PFILE a P \<EXT> utilizzando questa proprietà avanzata](#additionalpprefixextensions)
|**AttachmentAction**|[Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|**AttachmentActionTip**|[Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|**DisableMandatoryInOutlook**|[Esentare i messaggi di Outlook da un'etichetta obbligatoria](#exempt-outlook-messages-from-mandatory-labeling)
|**EnableAudit**|[Disabilitare l'invio di dati di controllo a Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|**EnableContainerSupport**|[Consente di rimuovere la protezione dai file PST, rar, 7zip e MSG](#enable-removal-of-protection-from-compressed-files)
|**EnableCustomPermissions**|[Disabilitare le autorizzazioni personalizzate in Esplora file](#disable-custom-permissions-in-file-explorer)|
|**EnableCustomPermissionsForCustomProtectedFiles**|[Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|**EnableLabelByMailHeader**|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|**EnableLabelBySharePointProperties**|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
| **EnableOutlookDistributionListExpansion** | [Espandi elenchi di distribuzione di Outlook durante la ricerca di destinatari di posta elettronica](#expand-outlook-distribution-lists-when-searching-for-email-recipients) |
| **EnableTrackAndRevoke** | [Disattiva le funzionalità di rilevamento dei documenti (anteprima pubblica)](#turn-off-document-tracking-features-public-preview) |
|**HideBarByDefault**|[Visualizza la barra di Information Protection nelle app Office](#display-the-information-protection-bar-in-office-apps)|
|**JustificationTextForUserText** | [Personalizzare i testi della richiesta di giustificazione per le etichette modificate](#customize-justification-prompt-texts-for-modified-labels) |
|**LogMatchedContent**|[Invia corrispondenze del tipo di informazioni a Azure Information Protection Analytics](#send-information-type-matches-to-azure-information-protection-analytics)|
|**OutlookBlockTrustedDomains**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookBlockUntrustedCollaborationLabel**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookCollaborationRule**| [Personalizzare i messaggi popup di Outlook](#customize-outlook-popup-messages)|
|**OutlookDefaultLabel**|[Impostare un'etichetta predefinita diversa per Outlook](#set-a-different-default-label-for-outlook)|
|**OutlookGetEmailAddressesTimeOutMSProperty** | [Modificare il timeout per l'espansione di una lista di distribuzione in Outlook quando si implementano messaggi di blocco per i destinatari negli elenchi di distribuzione](#expand-outlook-distribution-lists-when-searching-for-email-recipients) |
|**OutlookJustifyTrustedDomains**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookJustifyUntrustedCollaborationLabel**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookRecommendationEnabled**|[Abilitare la classificazione consigliata in Outlook](#enable-recommended-classification-in-outlook)|
|**OutlookOverrideUnlabeledCollaborationExtensions**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookSkipSmimeOnReadingPaneEnabled** | [Impedisci problemi di prestazioni di Outlook con messaggi di posta elettronica S/MIME](#prevent-outlook-performance-issues-with-smime-emails)|
|**OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookWarnTrustedDomains**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookWarnUntrustedCollaborationLabel**|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**PFileSupportedExtensions**|[Modificare i tipi di file da proteggere](#change-which-file-types-to-protect)|
|**PostponeMandatoryBeforeSave**|[Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
| **PowerPointRemoveAllShapesByShapeName**|[Rimuovere tutte le forme di un nome di forma specifico dalle intestazioni e dai piè di pagina, anziché rimuovere forme per testo all'interno della forma](#remove-all-shapes-of-a-specific-shape-name) |
|**PowerPointShapeNameToRemove** |[Evitare di rimuovere forme da PowerPoint che contengono testo specificato e non sono intestazioni/piè di pagina](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers) |
|**RemoveExternalContentMarkingInApp**|[Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions)|
|**RemoveExternalMarkingFromCustomLayouts**|[Rimuovere in modo esplicito i contrassegni di contenuto esterno dall'interno dei layout personalizzati di PowerPoint](#extend-external-marking-removal-to-custom-layouts) |
|**ReportAnIssueLink**|[Aggiungere "Segnala un problema" per gli utenti](#add-report-an-issue-for-users)|
|**RunPolicyInBackground**|[Attivare l'esecuzione continua della classificazione in background](#turn-on-classification-to-run-continuously-in-the-background)
|**ScannerMaxCPU** | [Limita utilizzo CPU](#limit-cpu-consumption) |
|**ScannerMinCPU** | [Limita utilizzo CPU](#limit-cpu-consumption) |
|**ScannerConcurrencyLevel**|[Limitare il numero di thread usati dallo scanner](#limit-the-number-of-threads-used-by-the-scanner)|
|**ScannerFSAttributesToSkip** | [Ignora o ignora i file durante le analisi a seconda degli attributi di file](#skip-or-ignore-files-during-scans-depending-on-file-attributes)
|**SharepointWebRequestTimeout**| [Configurare i timeout di SharePoint](#configure-sharepoint-timeouts)|
|**SharepointFileWebRequestTimeout** |[Configurare i timeout di SharePoint](#configure-sharepoint-timeouts)|
|**UseCopyAndPreserveNTFSOwner** | [Mantieni proprietari NTFS durante l'assegnazione di etichette](#preserve-ntfs-owners-during-labeling-public-preview)
| | |


### <a name="label-advanced-setting-reference"></a>Riferimento alle impostazioni avanzate etichetta

Usare il parametro *AdvancedSettings* con [New-Label](/powershell/module/exchange/policy-and-compliance/new-label) e [set-label](/powershell/module/exchange/policy-and-compliance/set-label).

|Impostazione|Scenario e istruzioni|
|----------------|---------------|
|**color**|[Specificare un colore per l'etichetta](#specify-a-color-for-the-label)|
|**customPropertiesByLabel**|[Applicare una proprietà personalizzata quando viene applicata un'etichetta](#apply-a-custom-property-when-a-label-is-applied)|
|**DefaultSubLabelId**|[Specificare un'etichetta secondaria predefinita per un'etichetta padre](#specify-a-default-sublabel-for-a-parent-label) 
|**labelByCustomProperties**|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|**SMimeEncrypt**|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|**SMimeSign**|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|


## <a name="display-the-information-protection-bar-in-office-apps"></a>Visualizza la barra di Information Protection nelle app Office

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, gli utenti devono selezionare l'opzione **Mostra barra** dal pulsante **sensibilità** per visualizzare la barra di Information Protection nelle app di Office. Usare la chiave **HideBarByDefault** e impostare il valore su **false** per visualizzare automaticamente questa barra per gli utenti in modo che sia possibile selezionare le etichette dalla barra o dal pulsante. 

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **HideBarByDefault**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}
```

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Esentare i messaggi di Outlook da un'etichetta obbligatoria

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, quando si Abilita l'impostazione dei criteri di etichetta di **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, tutti i documenti salvati e i messaggi di posta elettronica inviati devono avere un'etichetta applicata. Quando si configura l'impostazione avanzata seguente, l'impostazione dei criteri si applica solo ai documenti di Office e non ai messaggi di Outlook.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **DisableMandatoryInOutlook**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}
```

## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **OutlookRecommendationEnabled**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}
```

## <a name="enable-removal-of-protection-from-compressed-files"></a>Abilitare la rimozione della protezione dai file compressi

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si configura questa impostazione, il cmdlet di  [PowerShell](./clientv2-admin-guide-powershell.md) **set-AIPFileLabel** è abilitato per consentire la rimozione della protezione da file PST, rar, 7zip e msg.

- Chiave: **EnableContainerSupport**

- Valore: **true**

Comando di PowerShell di esempio in cui è abilitato il criterio:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableContainerSupport="True"}
```

## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata come impostazione dei criteri per l'opzione **applica questa etichetta per impostazione predefinita a documenti e messaggi di posta elettronica**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **OutlookDefaultLabel**

- Valore: \<**label GUID**> o **None**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}
```

## <a name="change-which-file-types-to-protect"></a>Modificare i tipi di file da proteggere

Queste configurazioni usano un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, il client Azure Information Protection Unified Labeling protegge tutti i tipi di file e lo scanner dal client protegge solo i tipi di file di Office e i file PDF.

È possibile modificare questo comportamento predefinito per i criteri di etichetta selezionati, specificando uno degli elementi seguenti:

### <a name="pfilesupportedextension"></a>PFileSupportedExtension

- Chiave: **PFileSupportedExtensions**

- Valore **\<string value>** 

Usare la tabella seguente per identificare il valore stringa da specificare:

| Valore stringa| Client| Scanner|
|-------------|-------|--------|
|\*|Valore predefinito: applicare la protezione a tutti i tipi di file|Applicare la protezione a tutti i tipi di file|
|ConvertTo-JSON (". jpg", ". png")|Oltre ai tipi di file di Office e ai file PDF, applicare la protezione alle estensioni di file specificate | Oltre ai tipi di file di Office e ai file PDF, applicare la protezione alle estensioni di file specificate
| | | |

**Esempio 1**: comando di PowerShell per lo scanner per proteggere tutti i tipi di file, in cui il criterio dell'etichetta è denominato "scanner":

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**Esempio 2**: comando di PowerShell per lo scanner per proteggere i file con estensione txt e CSV, oltre ai file di Office e PDF, in cui il criterio dell'etichetta è denominato "scanner":

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}
```

Con questa impostazione è possibile modificare i tipi di file protetti, ma non è possibile modificare il livello di protezione predefinito da nativo a generico. Ad esempio, per gli utenti che eseguono il client di etichettatura unificata, è possibile modificare l'impostazione predefinita in modo che siano protetti solo i file di Office e i file PDF anziché tutti i tipi di file. Tuttavia, non è possibile modificare questi tipi di file in modo da essere protetti in modo generico con un'estensione di file. Pfile.

### <a name="additionalpprefixextensions"></a>AdditionalPPrefixExtensions

Il client di etichettatura unificata supporta la modifica \<EXT> . PFILE a P \<EXT> utilizzando la proprietà Advanced, **AdditionalPPrefixExtensions**. Questa proprietà avanzata è supportata da Esplora file, PowerShell e dallo scanner. Tutte le app hanno un comportamento simile.   

- Chiave: **AdditionalPPrefixExtensions**

- Valore **\<string value>** 

Usare la tabella seguente per identificare il valore stringa da specificare:

| Valore stringa| Client e scanner|
|-------------|---------------|
|\*|Tutte le estensioni PFile diventano P\<EXT>|
|\<null value>| Il valore predefinito si comporta come il valore di protezione predefinito.|
|ConvertTo-JSON (". dwg", ". zip")|Oltre all'elenco precedente, ". dwg" e ". zip" diventano P\<EXT>| 

Con questa impostazione, le estensioni seguenti diventano sempre **P \<EXT>**: ". txt", ". xml", ". bmp", ". JT", ". jpg", ". jpeg", ". jpe", ". jif", ". JFIF", ". JFI", ". png", ". TIF", ". TIFF", ". gif"). Un'esclusione rilevante è che "ptxt" non diventa "txt. Pfile". 

**AdditionalPPrefixExtensions** funziona solo se è abilitata la protezione di Pfile con la proprietà avanzata- [**PFileSupportedExtension**](#pfilesupportedextension) . 

**Esempio 1**: comando di PowerShell per comportarsi come il comportamento predefinito in cui Protect ". dwg" diventa ". dwg. Pfile":

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =""}
```

**Esempio 2**: comando di PowerShell per modificare tutte le estensioni Pfile dalla protezione generica (DWG. Pfile) alla protezione nativa (. pdwg) quando i file sono protetti:

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions ="*"}
```

**Esempio 3**: comando di PowerShell per impostare ". dwg" su ". pdwg" quando si usa questo servizio per proteggere questo file:

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =ConvertTo-Json(".dwg")}
```



## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si usa l'impostazione dei criteri di etichetta di **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, agli utenti viene richiesto di selezionare un'etichetta quando salvano per la prima volta un documento di Office e quando inviano un messaggio di posta elettronica da Outlook.

Per i documenti, gli utenti possono selezionare **Non ora** per chiudere temporaneamente la richiesta di selezionare un'etichetta e tornare al documento. Non possono però chiudere il documento salvato senza etichettarlo. 

Quando si configura l'impostazione **PostponeMandatoryBeforeSave** , l'opzione **non ora** viene rimossa, in modo che gli utenti debbano selezionare un'etichetta quando il documento viene salvato per la prima volta.

> [!TIP]
> L'impostazione **PostponeMandatoryBeforeSave** garantisce inoltre che i documenti condivisi vengano etichettati prima di essere inviati tramite posta elettronica. 
>
>Per impostazione predefinita, anche se **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta** abilitata nel criterio, gli utenti vengono promossi solo per etichettare i file allegati ai messaggi di posta elettronica all'interno di Outlook.  
> 
Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **PostponeMandatoryBeforeSave**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}
```

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette

Questa configurazione USA [le impostazioni avanzate](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Esistono due metodi per rimuovere le classificazioni da altre soluzioni di assegnazione di etichette:

|Impostazione  |Descrizione  |
|---------|---------|
|**WordShapeNameToRemove**     |  Rimuove qualsiasi forma dai documenti di Word in cui il nome della forma corrisponde al nome definito nella proprietà avanzata **WordShapeNameToRemove** .  <br><br>Per ulteriori informazioni, vedere [utilizzare la proprietà avanzata WordShapeNameToRemove](#use-the-wordshapenametoremove-advanced-property).     |
|**RemoveExternalContentMarkingInApp** <br><br>**ExternalContentMarkingToRemove**   |    Consente di rimuovere o sostituire intestazioni o piè di pagina basati su testo da documenti di Word, Excel e PowerPoint. <br><br>Per altre informazioni, vedere: <br>- [Usare la proprietà avanzata RemoveExternalContentMarkingInApp](#use-the-removeexternalcontentmarkinginapp-advanced-property)<br>- [Come configurare ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove).    |
|     |         |

### <a name="use-the-wordshapenametoremove-advanced-property"></a>Usare la proprietà avanzata WordShapeNameToRemove

*La proprietà avanzata **WordShapeNameToRemove** è supportata dalla versione 2.6.101.0 e successive*

Questa impostazione consente di rimuovere o sostituire etichette basate su forme da documenti di Word quando tali contrassegni visivi sono stati applicati da un'altra soluzione di assegnazione di etichette. Ad esempio, la forma contiene il nome di un'etichetta precedente a cui è stata eseguita la migrazione in etichette di riservatezza per usare un nuovo nome di etichetta e la relativa forma.

Per usare questa proprietà avanzata, è necessario trovare il nome della forma nel documento di Word e quindi definirli nell'elenco delle proprietà avanzate **WordShapeNameToRemove** di forme. Il servizio rimuoverà qualsiasi forma in Word che inizia con un nome definito nell'elenco di forme in questa proprietà avanzata.

Evitare di rimuovere le forme che contengono il testo che si desidera ignorare, definendo il nome di tutte le forme da rimuovere ed evitando di controllare il testo in tutte le forme, ovvero un processo che richiede un utilizzo intensivo delle risorse.

> [!NOTE]
> Se non si specificano le forme parola in questa impostazione aggiuntiva di proprietà avanzata e Word viene incluso nel valore della chiave **RemoveExternalContentMarkingInApp** , verranno controllate tutte le forme per il testo specificato nel valore [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) . 
>

**Per trovare il nome della forma che si sta utilizzando e si desidera escludere**:

1. In Word visualizzare il riquadro di **selezione** : **scheda Home** > gruppo di **modifica** > **selezionare** l'opzione > riquadro di **selezione**.

2. Selezionare la forma nella pagina che si desidera contrassegnare per la rimozione. Il nome della forma contrassegnata è ora evidenziato nel riquadro di **selezione** .

Usare il nome della forma per specificare un valore stringa per la chiave * * * * WordShapeNameToRemove * * * *. 

Esempio: il nome della forma è **DC**. Per rimuovere la forma con questo nome, specificare il valore: `dc`.

- Chiave: **WordShapeNameToRemove**

- Valore: \<**Word shape name**> 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}
```

Quando si dispone di più di una forma di parola da rimuovere, specificare tutti i valori disponibili per la rimozione delle forme.

### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>Usare la proprietà avanzata RemoveExternalContentMarkingInApp

Questa impostazione consente di rimuovere o sostituire intestazioni o piè di pagina basati su testo da documenti quando tali contrassegni visivi sono stati applicati da un'altra soluzione di assegnazione di etichette. Il piè di pagina precedente, ad esempio, contiene il nome di una vecchia etichetta a cui è stata eseguita la migrazione in etichette di riservatezza per usare un nuovo nome di etichetta e il relativo piè di pagina.

Quando il client di etichettatura unificata ottiene questa configurazione nel criterio, le intestazioni e i piè di pagina precedenti vengono rimossi o sostituiti quando il documento viene aperto nell'app di Office ed è applicata qualsiasi etichetta di riservatezza al documento.

Questa configurazione non è supportata per Outlook e tenere presente che quando viene usata con Word, Excel e PowerPoint, può influire negativamente sulle prestazioni di queste app per gli utenti. La configurazione consente di definire le impostazioni per ogni applicazione, ad esempio la ricerca di testo nelle intestazioni e nei piè di pagina di documenti di Word, ma non nei fogli di calcolo di Excel o nelle presentazioni di PowerPoint.

Poiché la corrispondenza dei criteri influiscono sulle prestazioni degli utenti, è consigliabile limitare i tipi di applicazioni di Office (**W** Ord, E **X** cel, **P** owerPoint) solo a quelli che devono essere cercati.
Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **RemoveExternalContentMarkingInApp**

- Valore: \<**Office application types WXP**> 

Esempi:

- Per eseguire la ricerca solo in documenti di Word, specificare **W**.

- Per eseguire la ricerca in documenti di Word e presentazioni di PowerPoint, specificare **WP**.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}
```

Sarà necessaria almeno un'altra impostazione client avanzata, [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove), per specificare il contenuto dell'intestazione o del piè di pagina e il modo in cui rimuoverlo o sostituirlo.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Come configurare ExternalContentMarkingToRemove

Quando si specifica il valore stringa per la chiave **ExternalContentMarkingToRemove** , sono disponibili tre opzioni che usano le espressioni regolari. Per ognuno di questi scenari, utilizzare la sintassi illustrata nella colonna **valore di esempio** della tabella seguente:

|Opzione  |Descrizione di esempio |Valore di esempio|
|---------|---------|---------|
|**Corrispondenza parziale per rimuovere tutti gli elementi nell'intestazione o nel piè di pagina**     | Le intestazioni o i piè di pagina contengono il testo della stringa **da rimuovere** e si desidera rimuovere completamente tali intestazioni o piè di pagina.   |`*TEXT*`  | 
|**Completa la corrispondenza per rimuovere solo parole specifiche nell'intestazione o nel piè di pagina**     |    Le intestazioni o i piè di pagina contengono il testo della stringa **da rimuovere** e si vuole rimuovere solo il **testo** della parola, lasciando la stringa dell'intestazione o del piè di pagina come **da rimuovere**.      |`TEXT ` |
|**Completa la corrispondenza per rimuovere tutti gli elementi nell'intestazione o nel piè di pagina**     |Le intestazioni o i piè di pagina hanno il testo della stringa **da rimuovere**. Per rimuovere le intestazioni o i piè di pagina che contengono esattamente questa stringa,         |`^TEXT TO REMOVE$`|
|     |         | |


I criteri di ricerca per la stringa specificata non fanno distinzione tra maiuscole e minuscole. La lunghezza massima della stringa è di 255 caratteri e non può contenere spazi vuoti. 

Poiché alcuni documenti potrebbero includere caratteri invisibili o tipi diversi di spazi o tabulazioni, la stringa specificata per una frase potrebbe non essere rilevata. Quando possibile, specificare una singola parola distintiva per il valore e assicurarsi di testare i risultati prima della distribuzione nell'ambiente di produzione.

Per gli stessi criteri di etichetta specificare le stringhe seguenti:

- Chiave: **ExternalContentMarkingToRemove**

- Valore: \<**string to match, defined as regular expression**> 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}
```

Per altre informazioni, vedere:

- [Intestazioni o piè di pagina su più righe](#multiline-headers-or-footers)
- [Ottimizzazione per PowerPoint](#optimization-for-powerpoint)

#### <a name="multiline-headers-or-footers"></a>Intestazioni o piè di pagina su più righe

Se il testo di un'intestazione o un piè di pagina è su più righe, creare una chiave e un valore per ogni riga. Ad esempio, se si ha il piè di pagina seguente con due righe:

**The file is classified as Confidential**

**Label applied manually**

Per rimuovere il piè di pagina su più righe, creare le due voci seguenti per gli stessi criteri di etichetta:

- Chiave: **ExternalContentMarkingToRemove**

- Valore chiave 1: **\* riservato***

- Valore chiave 2: **\* etichetta applicata*** 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}
```

#### <a name="optimization-for-powerpoint"></a>Ottimizzazione per PowerPoint

Le intestazioni e i piè di pagina in PowerPoint sono implementati come forme. Per i tipi di forma **msoTextBox**, **msoTextEffect**, **msoPlaceholder** e **msoAutoShape** , le impostazioni avanzate seguenti forniscono ottimizzazioni aggiuntive:

- [PowerPointShapeNameToRemove](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers)
- [RemoveExternalMarkingFromCustomLayouts](#extend-external-marking-removal-to-custom-layouts)

Inoltre, [PowerPointRemoveAllShapesByShapeName](#remove-all-shapes-of-a-specific-shape-name) può rimuovere qualsiasi tipo di forma, in base al nome della forma.

Per ulteriori informazioni, vedere [trovare il nome della forma che si sta utilizzando come intestazione o piè di](#find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer)pagina.

##### <a name="avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers"></a>Evitare di rimuovere forme da PowerPoint che contengono testo specificato e non sono intestazioni/piè di pagina

Per evitare di rimuovere le forme che contengono il testo specificato, ma non le intestazioni o i piè di pagina, usare un'impostazione client avanzata aggiuntiva denominata **PowerPointShapeNameToRemove**. 

È consigliabile usare questa impostazione anche per evitare di controllare il testo in tutte le forme, essendo un processo a elevato utilizzo di risorse. 

- Se non si specifica questa impostazione client avanzata aggiuntiva e PowerPoint è incluso nel valore della chiave [RemoveExternalContentMarkingInApp](#remove-headers-and-footers-from-other-labeling-solutions), il testo specificato nel valore [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) verrà ricercato in tutte le forme. 

- Se si specifica questo valore, verranno rimosse solo le forme che soddisfano i criteri del nome della forma e il testo che corrisponde alla stringa fornita con [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) .

Esempio:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}
```

##### <a name="extend-external-marking-removal-to-custom-layouts"></a>Estendi la rimozione del contrassegno esterno ai layout personalizzati

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, la logica usata per rimuovere i contrassegni di contenuto esterni ignora i layout personalizzati configurati in PowerPoint. Per estendere questa logica ai layout personalizzati, impostare la proprietà avanzata **RemoveExternalMarkingFromCustomLayouts** su **true**.

- Chiave: **RemoveExternalMarkingFromCustomLayouts**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalMarkingFromCustomLayouts="True"}
```

##### <a name="remove-all-shapes-of-a-specific-shape-name"></a>Rimuovere tutte le forme di un nome di forma specifico

Se si usano layout personalizzati di PowerPoint e si desidera rimuovere tutte le forme di un nome di forma specifico dalle intestazioni e dai piè di pagina, usare l'impostazione avanzata **PowerPointRemoveAllShapesByShapeName** con il nome della forma che si vuole rimuovere.

Se si utilizza l'impostazione **PowerPointRemoveAllShapesByShapeName** , il testo all'interno delle forme viene ignorato e viene utilizzato il nome della forma per identificare le forme che si desidera rimuovere.

Esempio:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointRemoveAllShapesByShapeName="Arrow: Right"}
```

> [!NOTE]
> Per definire l'impostazione **PowerPointRemoveAllShapesByShapeName** , è necessario attualmente definire anche l'impostazione [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) , anche se non è necessaria la funzionalità fornita da **ExternalContentMarkingToRemove**.
>
> Se si desidera definire **PowerPointRemoveAllShapesByShapeName**, è consigliabile definire sia [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) che [PowerPointShapeNameToRemove](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers) per evitare di rimuovere più forme di quelle desiderate.
>

Per altre informazioni, vedere:

- [Trovare il nome della forma che si sta utilizzando come intestazione o piè di pagina](#find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer)
- [Rimuovere il contrassegno di contenuto esterno da layout personalizzati in PowerPoint](#remove-external-content-marking-from-custom-layouts-in-powerpoint)

##### <a name="find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer"></a>Trovare il nome della forma che si sta utilizzando come intestazione o piè di pagina

1. In PowerPoint visualizzare il riquadro **Selezione**: scheda **Formato** > gruppo **Disponi** > **Riquadro di selezione**.

2. Selezionare la forma sulla diapositiva contenente l'intestazione o il piè di pagina. Il nome della forma selezionata viene evidenziato nel riquadro **Selezione**.

Usare il nome della forma per specificare un valore stringa per la chiave **PowerPointShapeNameToRemove**. 

**Esempio**: il nome della forma è **FC**. Per rimuovere la forma con questo nome, specificare il valore: `fc`.

- Chiave: **PowerPointShapeNameToRemove**

- Valore: \<**PowerPoint shape name**> 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}
```

Quando si dispone di più di una forma di PowerPoint da rimuovere, specificare tutti i valori disponibili per le forme da rimuovere.

Per impostazione predefinita, il testo delle intestazioni e dei piè di pagina viene cercato solo negli schemi diapositiva. Per estendere la ricerca a tutte le diapositive, che è un processo con un utilizzo maggiore di risorse, usare un'impostazione client avanzata aggiuntiva denominata **RemoveExternalContentMarkingInAllSlides**:

- Chiave: **RemoveExternalContentMarkingInAllSlides**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}
```

##### <a name="remove-external-content-marking-from-custom-layouts-in-powerpoint"></a>Rimuovere il contrassegno di contenuto esterno da layout personalizzati in PowerPoint

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, la logica usata per rimuovere i contrassegni di contenuto esterni ignora i layout personalizzati configurati in PowerPoint. Per estendere questa logica ai layout personalizzati, impostare la proprietà avanzata **RemoveExternalMarkingFromCustomLayouts** su **true**.

- Chiave: **RemoveExternalMarkingFromCustomLayouts**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalMarkingFromCustomLayouts="True"}
```

## <a name="disable-custom-permissions-in-file-explorer"></a>Disabilitare le autorizzazioni personalizzate in Esplora file

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, gli utenti visualizzano un'opzione denominata **Proteggi con autorizzazioni personalizzate** quando fanno clic con il pulsante destro del mouse in Esplora file e scelgono **classifica e proteggi**. Questa opzione consente di impostare impostazioni di protezione personalizzate che possono sostituire le impostazioni di protezione che potrebbero essere state incluse con una configurazione di etichetta. Gli utenti possono visualizzare anche un'opzione per rimuovere la protezione. Quando si configura questa impostazione, gli utenti non visualizzano queste opzioni.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableCustomPermissions**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si configura l'impostazione client avanzata per [disabilitare le autorizzazioni personalizzate in Esplora file](#disable-custom-permissions-in-file-explorer), per impostazione predefinita gli utenti non sono in grado di visualizzare o modificare le autorizzazioni personalizzate già impostate in un documento protetto.

Tuttavia, esiste un'altra impostazione client avanzata che è possibile specificare in modo che in questo scenario gli utenti possano visualizzare e modificare le autorizzazioni personalizzate per un documento protetto quando usano Esplora file e fare clic con il pulsante destro del mouse sul file.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableCustomPermissionsForCustomProtectedFiles**

- Valore: **true**

Esempio di comando di PowerShell:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}
```

## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)

Questa configurazione USA [le impostazioni avanzate](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Questa impostazione è destinata al momento in cui gli utenti alleghino i documenti con etichetta a un messaggio di posta elettronica e non etichettano il messaggio. In questo scenario viene selezionata automaticamente un'etichetta, in base alle etichette di classificazione applicate agli allegati. Viene selezionata l'etichetta di classificazione più alta.

L'allegato deve essere un file fisico e non può essere un collegamento a un file (ad esempio, un collegamento a un file in Microsoft SharePoint o OneDrive).

È possibile configurare questa impostazione su **consigliato**, in modo che agli utenti venga richiesto di applicare l'etichetta selezionata al messaggio di posta elettronica con una descrizione comando personalizzabile. Gli utenti possono accettare il suggerimento o ignorarlo. In alternativa, è possibile configurare questa impostazione su **automatica**, in cui l'etichetta selezionata viene applicata automaticamente, ma gli utenti possono rimuovere l'etichetta o selezionare un'etichetta diversa prima di inviare il messaggio di posta elettronica.

> [!NOTE]
> Quando l'allegato con l'etichetta di classificazione più alta è configurato per la protezione con l'impostazione delle autorizzazioni definite dall'utente:
> 
> - Quando le autorizzazioni definite dall'utente dell'etichetta includono Outlook (non inviare), tale etichetta è selezionata e non viene applicata la protezione in diretta al messaggio di posta elettronica.
> - Quando le autorizzazioni definite dall'utente dell'etichetta sono destinate solo a Word, Excel, PowerPoint ed Esplora file, tale etichetta non viene applicata al messaggio di posta elettronica e nessuna delle due è la protezione.
> 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave 1: **AttachmentAction**

- Valore chiave 1: **consigliato** o **automatico**

- Chiave 2: **AttachmentActionTip**

- Valore chiave 2: " \<customized tooltip> "

La descrizione comando personalizzata supporta solo un solo linguaggio.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}
```

## <a name="add-report-an-issue-for-users"></a>Aggiungere "Segnala un problema" per gli utenti

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si specifica la seguente impostazione client avanzata, gli utenti visualizzano l'opzione **Segnala un problema**, che può essere selezionata dalla finestra di dialogo **Guida e commenti** del client. Specificare una stringa HTTP per il collegamento. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **ReportAnIssueLink**

- Valore **\<HTTP string>**

Valore di esempio per un sito Web: `https://support.contoso.com`

Valore di esempio per un indirizzo di posta elettronica: `mailto:helpdesk@contoso.com`

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}
```

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica

Questa configurazione USA [le impostazioni avanzate](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si creano e configurano le impostazioni client avanzate seguenti, gli utenti visualizzano messaggi popup di Outlook che possono avvertirli prima dell'invio di un messaggio di posta elettronica, chiedere di giustificare il motivo dell'invio o impedire l'invio di un messaggio di posta elettronica per uno degli scenari seguenti:

- **Il messaggio di posta elettronica o un suo allegato hanno un'etichetta specifica**:
    - L'allegato può essere qualsiasi tipo di file

- **Il messaggio di posta elettronica o l'allegato non hanno un'etichetta**:
    - L'allegato può essere un documento di Office o un documento PDF

Quando vengono soddisfatte queste condizioni, l'utente visualizza un messaggio popup con una delle azioni seguenti:

|Type  |Description  |
|---------|---------|
|**Avvertire**     | l'utente può confermare e inviare oppure annullare.        |
|**Giustificare**     |  All'utente viene richiesta la giustificazione (opzioni predefinite o formato libero) e l'utente può quindi inviare o annullare il messaggio. <br>Il testo della giustificazione viene scritto nell'intestazione x del messaggio di posta elettronica, in modo che possa essere letto da altri sistemi, ad esempio i servizi di prevenzione della perdita dei dati (DLP).       |
|**Bloccato**     |    all'utente viene impedito di inviare il messaggio di posta elettronica finché la condizione persiste. <br>Il messaggio include il motivo del blocco del messaggio di posta elettronica in modo che l'utente possa risolvere il problema, <br>ad esempio rimuovendo destinatari specifici o assegnando un'etichetta al messaggio di posta elettronica.     |
|     |         | 

Quando i messaggi popup sono per un'etichetta specifica, è possibile configurare le eccezioni per i destinatari in base al nome di dominio.

Per un esempio di procedura dettagliata su come configurare queste impostazioni, vedere il video [Azure Information Protection configurazione popup di Outlook](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/) .

> [!TIP]
> Per assicurarsi che i popup vengano visualizzati anche quando i documenti vengono condivisi dall'esterno di Outlook **(File > condivisione > alleghino una copia)**, configurare anche l'impostazione avanzata di [PostponeMandatoryBeforeSave](#remove-not-now-for-documents-when-you-use-mandatory-labeling) .

Per altre informazioni, vedere:

- [Per implementare avvisi, giustificare o bloccare messaggi popup per etichette specifiche](#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels)
- [Per implementare l'avviso, giustificare o bloccare i messaggi popup per i messaggi di posta elettronica o gli allegati che non hanno un'etichetta](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label)

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Per implementare avvisi, giustificare o bloccare messaggi popup per etichette specifiche

Per i criteri selezionati, creare una o più delle seguenti impostazioni avanzate con le chiavi seguenti. Per i valori, specificare una o più etichette in base ai relativi GUID, separate da una virgola.

Valore di esempio per più GUID etichetta come stringa delimitata da virgole: 

```sh
dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f
```

|Tipo di messaggio  |Chiave/valore  |
|---------|---------|
|**Avvertire**     |  Chiave: **OutlookWarnUntrustedCollaborationLabel** <br><br>Valore: \<**label GUIDs, comma-separated**>       |
|**Giustificare**     |  Chiave: **OutlookJustifyUntrustedCollaborationLabel** <br><br>Valore: \<**label GUIDs, comma-separated**>       |
|**Bloccato**     | Chiave: **OutlookBlockUntrustedCollaborationLabel** <br><br>Valore: \<**label GUIDs, comma-separated**>       |
|     |         |



Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}
```

Per ulteriori personalizzazioni, è anche possibile [esentare i nomi di dominio per i messaggi popup configurati per etichette specifiche](#to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels).

> [!NOTE]
> Le impostazioni avanzate in questa sezione (**OutlookWarnUntrustedCollaborationLabel**, **OutlookJustifyUntrustedCollaborationLabel** e **OutlookBlockUntrustedCollaborationLabel**) sono relative al momento in cui è in uso un'etichetta *specifica* .
> 
> Per implementare i messaggi popup predefiniti per il contenuto non *etichettato* , usare l'impostazione avanzata **[OutlookUnlabeledCollaborationAction](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label)** . Per personalizzare i messaggi popup per il contenuto senza etichetta, usare un file con **estensione JSON** per definire le impostazioni avanzate. 
>
>Per altre informazioni, vedere [personalizzare i messaggi popup di Outlook](#customize-outlook-popup-messages).
> 
> [!TIP]
> Per assicurarsi che i messaggi di blocco vengano visualizzati in base alle esigenze, anche per un destinatario che si trova all'interno di una lista di distribuzione di Outlook, assicurarsi di aggiungere l'impostazione avanzata [EnableOutlookDistributionListExpansion](#expand-outlook-distribution-lists-when-searching-for-email-recipients) .
>

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>Per esentare i nomi di dominio per i messaggi popup configurati per etichette specifiche

Per le etichette specificate con questi messaggi popup, è possibile esentare i nomi di dominio specifici in modo che gli utenti non visualizzino i messaggi per i destinatari che hanno il nome di dominio incluso nell'indirizzo di posta elettronica. In questo caso, i messaggi di posta elettronica vengono inviati senza interruzioni. Per specificare più domini, aggiungerli come stringa singola, delimitata da virgole.

Una configurazione tipica consiste nel rendere visualizzabili i messaggi popup solo dai destinatari che sono esterni all'organizzazione o che non sono partner autorizzati dell'organizzazione. In questo caso, specificare tutti i domini di posta elettronica usati dall'organizzazione e dai partner.

Per gli stessi criteri di etichetta, creare le seguenti impostazioni client avanzate e, per il valore, specificare uno o più domini, ciascuno separato da una virgola.

Valore di esempio per più domini sotto forma di stringa delimitata da virgole: `contoso.com,fabrikam.com,litware.com`

|Tipo di messaggio  |Chiave/valore  |
|---------|---------|
|**Avvertire**     |  Chiave: **OutlookWarnTrustedDomains** <br><br>Valore **\<**domain names, comma separated**>**     |
|**Giustificare**     | Chiave: **OutlookJustifyTrustedDomains** <br><br>Valore **\<**domain names, comma separated**>**       |
|**Bloccato**     | Chiave: **OutlookBlockTrustedDomains** <br><br>Valore **\<**domain names, comma separated**>**      |
|     |         |


Si immagini, ad esempio, che sia stata specificata l'impostazione **OutlookBlockUntrustedCollaborationLabel** Advanced client per l'etichetta **Confidential \ All Employees** . 

È ora possibile specificare l'impostazione client avanzata aggiuntiva di **OutlookBlockTrustedDomains** con **contoso.com**. Di conseguenza, un utente può inviare un messaggio di posta elettronica a `john@sales.contoso.com` quando viene etichettato come **riservato \ tutti i dipendenti**, ma l'invio di un messaggio di posta elettronica con la stessa etichetta a un account Gmail verrà bloccato.

Comandi di PowerShell di esempio, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="contoso.com"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}
```

> [!NOTE]
> Per assicurarsi che i messaggi di blocco vengano visualizzati in base alle esigenze, anche per un destinatario che si trova all'interno di una lista di distribuzione di Outlook, assicurarsi di aggiungere l'impostazione avanzata [EnableOutlookDistributionListExpansion](#expand-outlook-distribution-lists-when-searching-for-email-recipients) .
>

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Per implementare l'avviso, giustificare o bloccare i messaggi popup per i messaggi di posta elettronica o gli allegati che non hanno un'etichetta

Per gli stessi criteri di etichetta, creare l'impostazione client avanzata seguente con uno dei valori seguenti:

|Tipo di messaggio  |Chiave/valore  |
|---------|---------|
|**Avvertire**     |  Chiave: **OutlookUnlabeledCollaborationAction** <br><br>Valore: **avviso**     |
|**Giustificare**     |Chiave: **OutlookUnlabeledCollaborationAction**<br><br>Valore: **giustifica**       |
|**Bloccato**     | Chiave: **OutlookUnlabeledCollaborationAction** <br><br>Valore: **blocco**      |
|  **Disattiva messaggi**   |   Chiave: **OutlookUnlabeledCollaborationAction** <br><br>Valore: **disattivato**      |
| | |


Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}
```

Per ulteriori personalizzazioni, vedere:

- [Per definire estensioni di file specifiche per i messaggi popup di avviso, giustificazione o blocco per gli allegati di posta elettronica che non hanno un'etichetta](#to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label)
- [Per specificare un'azione diversa per i messaggi di posta elettronica senza allegati](#to-specify-a-different-action-for-email-messages-without-attachments)
- [Personalizzare i messaggi popup di Outlook](#customize-outlook-popup-messages)

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Per definire estensioni di file specifiche per i messaggi popup di avviso, giustificazione o blocco per gli allegati di posta elettronica che non hanno un'etichetta

Per impostazione predefinita, i messaggi popup avvisa, giustifica o blocca si applicano a tutti i documenti di Office e PDF. È possibile affinare questo elenco specificando quali estensioni di file devono visualizzare i messaggi di avviso, di giustificazione o di blocco con un'impostazione avanzata aggiuntiva e un elenco delimitato da virgole di estensioni di file.

Valore di esempio per più estensioni di file da definire come stringa delimitata da virgole: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

In questo esempio un documento PDF senza etichetta non comporterà l'avviso, la giustificazione o il blocco dei messaggi popup.

Per gli stessi criteri di etichetta, immettere le stringhe seguenti: 


- Chiave: **OutlookOverrideUnlabeledCollaborationExtensions**

- Valore **\<**file name extensions to display messages, comma separated**>**


Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}
```

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>Per specificare un'azione diversa per i messaggi di posta elettronica senza allegati

Per impostazione predefinita, il valore specificato per [OutlookUnlabeledCollaborationAction](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label) per avvisare, giustificare o bloccare i messaggi popup si applica ai messaggi di posta elettronica o agli allegati che non hanno un'etichetta. 

È possibile perfezionare questa configurazione specificando un'altra impostazione avanzata per i messaggi di posta elettronica che non dispongono di allegati.

Creare l'impostazione client avanzata seguente con uno dei valori seguenti:

|Tipo di messaggio  |Chiave/valore  |
|---------|---------|
|**Avvertire**     | Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valore: **avviso**
     |
|**Giustificare**     |Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valore: **giustifica**      |
|**Bloccato**     | Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valore: **blocco**     |
|  **Disattiva messaggi**   |    Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valore: **disattivato**    |
| | |


Se non si specifica questa impostazione client, il valore specificato per [OutlookUnlabeledCollaborationAction](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label) viene usato per i messaggi di posta elettronica senza etichetta senza allegati, nonché per i messaggi di posta elettronica senza etichetta con allegati.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}
```

## <a name="expand-outlook-distribution-lists-when-searching-for-email-recipients"></a>Espandi elenchi di distribuzione di Outlook durante la ricerca di destinatari di posta elettronica

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per estendere il supporto da altre impostazioni avanzate ai destinatari all'interno delle liste di distribuzione di Outlook, impostare l'impostazione avanzata **EnableOutlookDistributionListExpansion** su **true**.

- Chiave: **EnableOutlookDistributionListExpansion**
- Valore: **true**

Ad esempio, se sono state configurate le impostazioni avanzate [OutlookBlockTrustedDomains](#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels), [OutlookBlockUntrustedCollaborationLabel](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) e quindi si configura l'impostazione **EnableOutlookDistributionListExpansion** , Outlook è abilitato per espandere la lista di distribuzione per garantire che un messaggio di blocco venga visualizzato in base alle esigenze.

Il timeout predefinito per l'espansione della lista di distribuzione è pari a **2000** millisecondi.

Per modificare questo timeout, creare l'impostazione avanzata seguente per i criteri selezionati:

- Chiave: **OutlookGetEmailAddressesTimeOutMSProperty**
- Valore: *Integer, in millisecondi*

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableOutlookDistributionListExpansion="true"} @{OutlookGetEmailAddressesTimeOutMSProperty="3000"}
```

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Disabilitare l'invio di dati di controllo a Azure Information Protection Analytics

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Il client per l'assegnazione di etichette unificata di Azure Information Protection supporta il reporting centrale e, per impostazione predefinita, invia i dati di controllo a [Azure Information Protection Analytics](../reports-aip.md). Per ulteriori informazioni sulle informazioni inviate e archiviate, vedere la sezione [informazioni raccolte e inviate a Microsoft](../reports-aip.md#information-collected-and-sent-to-microsoft) dalla documentazione centrale per la creazione di report.

Per modificare questo comportamento in modo che queste informazioni non vengano inviate dal client Unified Labeling, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableAudit**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}
```

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>Invia corrispondenze del tipo di informazioni a Azure Information Protection Analytics
 
Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, il client di etichettatura unificata non invia corrispondenze di contenuto per i tipi di informazioni riservate a [Azure Information Protection Analytics](../reports-aip.md). Per ulteriori informazioni su queste informazioni aggiuntive che possono essere inviate, vedere la sezione relativa alle [corrispondenze per un'analisi più approfondita](../reports-aip.md#content-matches-for-deeper-analysis) dalla documentazione centrale per la creazione di report.

Per inviare le corrispondenze di contenuto quando si inviano tipi di informazioni riservate, creare l'impostazione client avanzata seguente in un criterio etichetta: 

- Chiave: **LogMatchedContent**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}
```

## <a name="limit-cpu-consumption"></a>Limita utilizzo CPU

AIP Unified Labeling scanner limita il consumo di risorse per garantire che la CPU complessiva del computer non sia mai superiore al 85%. 

A partire dalla versione di scanner 2.7. x. x, è consigliabile limitare l'utilizzo della CPU tramite il metodo di impostazioni avanzate **ScannerMaxCPU** e **ScannerMinCPU** . 

> [!IMPORTANT]
> Quando il criterio di limitazione dei thread seguente è in uso, le impostazioni avanzate di **ScannerMaxCPU** e **ScannerMinCPU** vengono ignorate. Per limitare l'utilizzo della CPU tramite le impostazioni avanzate **ScannerMaxCPU** e **ScannerMinCPU** , annullare l'uso di criteri che limitano il numero di thread. 

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per limitare l'utilizzo della CPU nel computer dello scanner, è possibile gestirlo creando due impostazioni avanzate: 

- **ScannerMaxCPU**: 

    Per impostazione predefinita, impostare su **100** , il che significa che non esiste alcun limite di utilizzo massimo della CPU. In questo caso, il processo dello scanner tenterà di usare tutto il tempo disponibile per la CPU per ottimizzare le frequenze di analisi. 

    Se si imposta **ScannerMaxCPU** su un valore inferiore a 100, lo scanner monitorerà il consumo di CPU negli ultimi 30 minuti e se la CPU max supera il limite impostato, inizierà a ridurre il numero di thread allocati per i nuovi file. 

    Il limite per il numero di thread continuerà fino a quando l'utilizzo della CPU è superiore al limite impostato per **ScannerMaxCPU**.

- **ScannerMinCPU**:

    Verificare solo se **ScannerMaxCPU** non è uguale a 100 e non può essere impostato su un numero maggiore del valore di  **ScannerMaxCPU** .  Si consiglia di mantenere **ScannerMinCPU** impostare almeno 15 punti più in basso rispetto al valore di  **ScannerMaxCPU**.    
    
    Per impostazione predefinita, impostare su **50** , il che significa che se il consumo di CPU negli ultimi 30 minuti è inferiore a questo valore, lo scanner inizierà ad aggiungere nuovi thread per analizzare altri file in parallelo, fino a quando l'utilizzo della CPU non raggiunge il livello impostato per **ScannerMaxCPU**-15. 


## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>Limitare il numero di thread usati dallo scanner

> [!IMPORTANT]
> Quando il criterio di limitazione dei thread seguente è in uso, le impostazioni avanzate di **ScannerMaxCPU** e **ScannerMinCPU** vengono ignorate. Per limitare l'utilizzo della CPU tramite le impostazioni avanzate **ScannerMaxCPU** e **ScannerMinCPU** , annullare l'utilizzo di criteri che limitano il numero di thread. 

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, lo scanner usa tutte le risorse del processore disponibili nel computer che esegue il servizio scanner. Se è necessario limitare l'utilizzo della CPU durante l'analisi di questo servizio, creare l'impostazione avanzata seguente in un criterio di etichetta. 

Come valore specificare il numero di thread simultanei che lo scanner può eseguire in parallelo. Lo scanner usa un thread separato per ogni file analizzato, quindi questa configurazione della limitazione definisce anche il numero di file che possono essere analizzati in parallelo. 

Quando si configura il valore per il test per la prima volta, è consigliabile specificare 2 per ogni core e quindi monitorare i risultati. Se ad esempio si esegue lo scanner in un computer con 4 core, impostare prima il valore su 8. Se necessario, aumentare o diminuire questo numero, in base alle prestazioni risultanti richieste per il computer dello scanner e la velocità di analisi. 

- Chiave: **ScannerConcurrencyLevel**

- Valore **\<number of concurrent threads>**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "scanner":

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}
```

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) delle etichette che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Questa configurazione non è compatibile con i file PDF protetti con estensione Ppdf. Questi file non possono essere aperti dal client usando Esplora file o PowerShell.

Per i documenti di Office etichettati con le isole sicure, è possibile rietichettare questi documenti con un'etichetta di riservatezza usando un mapping definito dall'utente. È anche possibile usare questo metodo per riutilizzare le etichette da altre soluzioni quando sono applicate a documenti di Office. 

In seguito a questa opzione di configurazione, la nuova etichetta di riservatezza viene applicata dal client Azure Information Protection Unified Labeling come indicato di seguito:

- **Per i documenti di Office**: quando il documento viene aperto nell'app desktop, la nuova etichetta di riservatezza viene visualizzata come impostata e viene applicata quando il documento viene salvato.

- **Per PowerShell**: [set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) possono applicare la nuova etichetta di riservatezza.

- **Per Esplora file**: nella finestra di dialogo Azure Information Protection, la nuova etichetta di riservatezza viene visualizzata ma non è impostata.

Per questa configurazione è necessario specificare un'impostazione avanzata denominata **labelByCustomProperties** per ogni etichetta di riservatezza di cui si vuole eseguire il mapping all'etichetta precedente. Per ogni voce impostare quindi il valore usando la sintassi seguente:

```PowerShell
[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]
```

Specificare un nome di regola di migrazione a propria scelta. Usare un nome descrittivo che consenta di identificare la modalità di mapping di una o più etichette della soluzione di assegnazione di etichette precedente all'etichetta di riservatezza.

Si noti che questa impostazione non comporta la rimozione dell'etichetta originale dal documento o di tutti i contrassegni visivi nel documento che l'etichetta originale potrebbe aver applicato. Per rimuovere intestazioni e piè di pagina, vedere [rimuovere intestazioni e piè di pagina da altre soluzioni](#remove-headers-and-footers-from-other-labeling-solutions)per l'assegnazione di etichette.

Esempi:

- [Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta](#example-1-one-to-one-mapping-of-the-same-label-name)
- [Esempio 2: Mapping uno-a-uno per un altro nome di etichetta](#example-2-one-to-one-mapping-for-a-different-label-name)
- [Esempio 3: Mapping molti-a-uno di nomi di etichetta](#example-3-many-to-one-mapping-of-label-names)
- [Esempio 4: più regole per la stessa etichetta](#example-4-multiple-rules-for-the-same-label)

Per ulteriori personalizzazioni, vedere:

- [Estendi le regole di migrazione delle etichette ai messaggi di posta elettronica](#extend-your-label-migration-rules-to-emails)
- [Estendere le regole di migrazione delle etichette alle proprietà di SharePoint](#extend-your-label-migration-rules-to-sharepoint-properties)

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta

Requisito: i documenti con un'etichetta di isole sicure "riservato" devono essere rietichettati come "riservati" da Azure Information Protection.

In questo esempio:

- L'etichetta di Secure Islands è **Riservato** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

Impostazione avanzata:

- Chiave: **labelByCustomProperties**

- Valore: l' **etichetta Secure Islands è riservata, classificazione, riservata**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "Confidential":

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}
```

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Esempio 2: Mapping uno-a-uno per un altro nome di etichetta

Requisito: i documenti contrassegnati come "sensibili" dalle isole sicure devono essere rietichettati come "riservatezza elevata" da Azure Information Protection.

In questo esempio:

- L'etichetta di Secure Islands è **Sensibile** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

Impostazione avanzata:

- Chiave: **labelByCustomProperties**

- Valore: l' **etichetta Secure Islands è sensibile, classificazione, sensibile**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "highly Confidential":

```PowerShell
Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}
```

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>Esempio 3: Mapping molti-a-uno di nomi di etichetta

Requisito: sono presenti due etichette di isole sicure che includono la parola "Internal" e si vuole che i documenti che contengono una di queste etichette di isole sicure vengano rietichettati come "General" dal client Azure Information Protection Unified labeling.

In questo esempio:

- Le etichette di Secure Islands includono la parola **Interno** e sono archiviate nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

- Chiave: **labelByCustomProperties**

- Valore: l' **etichetta Secure Islands contiene Internal, Classification,. \* Interno. \***

Esempio di comando di PowerShell, in cui l'etichetta è denominata "generale":

```PowerShell
Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}
```

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Esempio 4: più regole per la stessa etichetta

Quando sono necessarie più regole per la stessa etichetta, definire più valori stringa per la stessa chiave. 

In questo esempio, le etichette delle isole sicure denominate "Confidential" e "Secret" vengono archiviate nella proprietà personalizzata denominata **Classification** e si vuole che il client Azure Information Protection Unified Labeling applichi l'etichetta di riservatezza denominata "Confidential":

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

### <a name="extend-your-label-migration-rules-to-emails"></a>Estendi le regole di migrazione delle etichette ai messaggi di posta elettronica

È possibile usare la configurazione definita con l'impostazione avanzata [*labelByCustomProperties*](#migrate-labels-from-secure-islands-and-other-labeling-solutions) per i messaggi di posta elettronica di Outlook, oltre ai documenti di Office, specificando un'impostazione avanzata dei criteri di etichetta aggiuntiva. 

Tuttavia, questa impostazione ha un impatto negativo noto sulle prestazioni di Outlook. Configurare quindi questa impostazione aggiuntiva solo quando si dispone di un requisito aziendale sicuro e ricordarsi di impostarla su un valore stringa null dopo aver completato la migrazione dall'altra soluzione di assegnazione di etichette.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableLabelByMailHeader**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}
```

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>Estendere le regole di migrazione delle etichette alle proprietà di SharePoint

È possibile utilizzare la configurazione definita con l'impostazione avanzata [*labelByCustomProperties*](#migrate-labels-from-secure-islands-and-other-labeling-solutions) per le proprietà di SharePoint che è possibile esporre come colonne agli utenti specificando un'impostazione avanzata dei criteri di etichetta aggiuntiva.

Questa impostazione è supportata quando si usano Word, Excel e PowerPoint.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableLabelBySharePointProperties**

- Valore: **true**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}
```

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Applicare una proprietà personalizzata quando viene applicata un'etichetta

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) delle etichette che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Potrebbero essere presenti alcuni scenari in cui si desidera applicare una o più proprietà personalizzate a un documento o a un messaggio di posta elettronica oltre ai metadati applicati da un'etichetta di riservatezza.

Esempio:

- È in corso la [migrazione da un'altra soluzione di assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions), ad esempio le isole sicure. Per l'interoperabilità durante la migrazione, si desidera che le etichette di riservatezza applichino anche una proprietà personalizzata utilizzata dall'altra soluzione di assegnazione di etichette.

- Per il sistema di gestione dei contenuti (ad esempio SharePoint o una soluzione di gestione dei documenti di un altro fornitore) si vuole usare un nome di proprietà personalizzato coerente con valori diversi per le etichette e con nomi descrittivi anziché il GUID dell'etichetta.

Per i documenti di Office e i messaggi di posta elettronica di Outlook che gli utenti etichettano usando il Azure Information Protection client Unified Labeling, è possibile aggiungere una o più proprietà personalizzate definite dall'utente. È anche possibile usare questo metodo per il client di etichettatura unificata per visualizzare una proprietà personalizzata come etichetta di altre soluzioni per il contenuto che non è ancora etichettato dal client di etichettatura unificata.

In seguito a questa opzione di configurazione, tutte le proprietà personalizzate aggiuntive vengono applicate dal client Azure Information Protection Unified Labeling come indicato di seguito:

|Ambiente  | Description  |
|---------|---------|
|**Documenti di Office**    | Quando il documento viene etichettato nell'app desktop, le proprietà personalizzate aggiuntive vengono applicate quando il documento viene salvato.        |
|**Messaggi di posta elettronica di Outlook**     |    Quando il messaggio di posta elettronica viene contrassegnato in Outlook, le proprietà aggiuntive vengono applicate all'intestazione x quando viene inviato il messaggio di posta elettronica.     |
|**PowerShell**     |  [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) applica le proprietà personalizzate aggiuntive quando il documento viene etichettato e salvato. <br><br>[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) Visualizza le proprietà personalizzate come etichetta mappata se non viene applicata un'etichetta di riservatezza.  |
|**Esplora file**     |     Quando l'utente fa clic con il pulsante destro del mouse sul file e applica l'etichetta, vengono applicate le proprietà personalizzate.     |
|     |         |


Per questa configurazione è necessario specificare un'impostazione avanzata denominata **customPropertiesByLabel** per ogni etichetta di riservatezza a cui si desidera applicare le proprietà personalizzate aggiuntive. Per ogni voce impostare quindi il valore usando la sintassi seguente:

```sh
[custom property name],[custom property value]
```

> [!IMPORTANT]
> L'uso di spazi vuoti nella stringa impedisce l'applicazione delle etichette.

Esempio:

- [Esempio 1: aggiungere un'unica proprietà personalizzata per un'etichetta](#example-1-add-a-single-custom-property-for-a-label)
- [Esempio 2: aggiungere più proprietà personalizzate per un'etichetta](#example-2-add-multiple-custom-properties-for-a-label)
#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Esempio 1: aggiungere un'unica proprietà personalizzata per un'etichetta

Requisito: i documenti etichettati come "riservati" dal client Azure Information Protection Unified Labeling devono avere la proprietà personalizzata aggiuntiva denominata "classificazione" con il valore "Secret".

In questo esempio:

- L'etichetta di riservatezza è denominata **Confidential** e crea una proprietà personalizzata denominata **classificazione** con il valore **Secret**.

Impostazione avanzata:

- Chiave: **customPropertiesByLabel**

- Valore: **classificazione, segreto**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "Confidential":

```PowerShell
    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}
```

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Esempio 2: aggiungere più proprietà personalizzate per un'etichetta

Per aggiungere più di una proprietà personalizzata per la stessa etichetta, è necessario definire più valori stringa per la stessa chiave.

Esempio di comando di PowerShell, in cui l'etichetta è denominata "generale" e si vuole aggiungere una proprietà personalizzata denominata **classificazione** con il valore **generale** e una seconda proprietà personalizzata denominata **Sensitivity** con il valore **Internal**:

```PowerShell
Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}
```

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurare un'etichetta per applicare la protezione S/MIME in Outlook

Questa configurazione USA [le impostazioni avanzate](#configuring-advanced-settings-for-the-client-via-powershell) di etichetta che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Usare queste impostazioni solo quando si dispone di una [distribuzione S/MIME](/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption) funzionante e si vuole che un'etichetta applichi automaticamente questo metodo di protezione per i messaggi di posta elettronica anziché Rights Management la protezione da Azure Information Protection. La protezione risultante è identica a quella applicata quando un utente seleziona manualmente le opzioni di S/MIME da Outlook.

|Configurazione  |Chiave/valore  |
|---------|---------|
|**Firma digitale S/MIME**     |   Per configurare un'impostazione avanzata per una firma digitale S/MIME, immettere le stringhe seguenti per l'etichetta selezionata: <br><br>-Key: **SMimeSign** <br><br>-Valore: **true**      |
|**Crittografia S/MIME**     |   Per configurare un'impostazione avanzata per la crittografia S/MIME, immettere le stringhe seguenti per l'etichetta selezionata:<br><br>-Key: **SMimeEncrypt**<br><br>-Valore: **true**      |
|     |         |

Se l'etichetta specificata è configurata per la crittografia, per il client Azure Information Protection Unified Labeling, S/MIME Protection sostituisce la protezione Rights Management solo in Outlook. Il client continua a usare le impostazioni di crittografia specificate per l'etichetta nell'interfaccia di amministrazione. 

Per le app di Office con etichette predefinite, non applicano la protezione S/MIME, bensì applicano la protezione non **inoltrare** .

Se si vuole che l'etichetta sia visibile solo in Outlook, configurare l'etichetta in modo da applicare la crittografia **solo ai messaggi di posta elettronica in Outlook**.

Comandi di PowerShell di esempio, in cui l'etichetta è denominata "solo destinatari":

```PowerShell
Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}
```

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Specificare un'etichetta secondaria predefinita per un'etichetta padre

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) delle etichette che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Quando si aggiunge un'etichetta secondaria a un'etichetta, gli utenti non possono più applicare l'etichetta padre a un documento o a un messaggio di posta elettronica. Per impostazione predefinita, gli utenti selezionano l'etichetta padre per visualizzare le etichette secondarie che possono essere applicate, quindi selezionare una delle etichette secondarie. Se si configura questa impostazione avanzata, quando gli utenti selezionano l'etichetta padre, viene automaticamente selezionata e applicata un'etichetta secondaria: 

- Chiave: **DefaultSubLabelId**

- Valore **\<sublabel GUID>**

Esempio di comando di PowerShell, in cui l'etichetta padre è denominata "Confidential" e l'etichetta secondaria "All Employees" ha un GUID di 8faca7b8-8d20-48A3-8ea2-0f96310a848e:

```PowerShell
Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
```

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>Attivare l'esecuzione continua della classificazione in background

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) delle etichette che è necessario configurare usando Office 365 Security & Compliance Center PowerShell. 

Quando si configura questa impostazione, viene modificato il comportamento predefinito del client di Azure Information Protection Unified labeling che applica le etichette automatiche e consigliate ai documenti:

Per Word, Excel e PowerPoint, la classificazione automatica viene eseguita in modo continuo in background.

Il comportamento rimane invariato per Outlook.

Quando il client di assegnazione di etichette unificato di Azure Information Protection controlla periodicamente i documenti per le regole di condizione specificate, questo comportamento Abilita la classificazione automatica e consigliata e la protezione per i documenti di Office archiviati in SharePoint o OneDrive, purché sia attivato il salvataggio automatico. Anche i file di grandi dimensioni sono stati salvati più rapidamente perché le regole di condizione sono già state eseguite.

Le regole di condizione non vengono eseguite in tempo reale durante la digitazione. Vengono eseguite periodicamente come attività in background se il documento viene modificato.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **RunPolicyInBackground**
- Valore: **true**

Esempio di comando di PowerShell: 

```PowerShell
Set-LabelPolicy -Identity PolicyName -AdvancedSettings @{RunPolicyInBackground = "true"}
```

> [!NOTE]
> Questa funzionalità è attualmente disponibile in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
> 

## <a name="specify-a-color-for-the-label"></a>Specificare un colore per l'etichetta

Questa configurazione USA [le impostazioni avanzate](#configuring-advanced-settings-for-the-client-via-powershell) di etichetta che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Usare questa impostazione avanzata per impostare un colore per un'etichetta. Per specificare il colore, immettere un codice di tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, #40e0d0 è il valore esadecimale RGB per il turchese.

Se è necessario un riferimento per questi codici, è possibile trovare una tabella utile dalla [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) pagina della documentazione Web di MSDN. Questi codici sono disponibili anche in molte applicazioni che consentono di modificare le immagini. Ad esempio quando in Microsoft Paint si sceglie un colore personalizzato in una tavolozza vengono visualizzati automaticamente i valori RGB corrispondenti ed è possibile copiarli.

Per configurare l'impostazione avanzata per il colore di un'etichetta, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **colore**

- Valore **\<RGB hex value>**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "public":

```PowerShell
Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}
```

## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

L'accesso con più utenti non è supportato da AIP in produzione. Questa procedura descrive come eseguire l'accesso come utente diverso solo a scopo di test.

È possibile verificare l'account a cui si è attualmente connessi usando la finestra di dialogo **Microsoft Azure Information Protection** : aprire un'applicazione di Office e nella scheda **Home** , selezionare il pulsante **sensibilità** , quindi selezionare **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'utilizzo dell'account errato include il mancato download delle etichette o la mancata visualizzazione delle etichette o del comportamento previsto.

**Per accedere come utente diverso**:

1. Passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzata una richiesta nell'applicazione di Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e selezionare **Accedi** dalla sezione **stato client** aggiornato.

Inoltre:

|Scenario  |Descrizione  |
|---------|---------|
|**Ancora eseguito l'accesso all'account precedente**     |  Se il client Azure Information Protection Unified Labeling è ancora connesso con l'account precedente dopo aver completato questi passaggi, eliminare tutti i cookie da Internet Explorer, quindi ripetere i passaggi 1 e 2.       |
|**Utilizzo di Single Sign-On**    |    Se si usa la funzione Single Sign-On, è necessario uscire da Windows e accedere con un account utente diverso dopo aver eliminato il file del token. <br><br>Il Azure Information Protection client per l'assegnazione di etichette unificata viene quindi autenticato automaticamente utilizzando l'account utente attualmente connesso.     |
|**Tenant diversi**     |  Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. <br><br>Per testare Azure Information Protection con più tenant, usare computer diversi.       |
|**Reimpostare le impostazioni**     | È possibile usare l'opzione **Reimposta impostazioni** da **Guida e commenti e suggerimenti** per disconnettersi ed eliminare le etichette e le impostazioni dei criteri attualmente scaricate da Office 365 Security & Compliance Center, il Centro sicurezza Microsoft 365 o il Microsoft 365 Compliance Center.        |
|     |         |

## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

> [!IMPORTANT]
> I computer disconnessi sono supportati per gli scenari di assegnazione di etichette seguenti: Esplora file, PowerShell, le app di Office e lo scanner.

Per impostazione predefinita, il client di Azure Information Protection Unified Labeling prova automaticamente a connettersi a Internet per scaricare le etichette e le impostazioni dei criteri di etichetta dal centro di gestione delle etichette (il Centro sicurezza & conformità di 365 Office, il Centro sicurezza Microsoft 365 o il Microsoft 365 Compliance Center). 

Se si dispone di computer che non possono connettersi a Internet per un certo periodo di tempo, è possibile esportare e copiare i file che gestiscono manualmente i criteri per il client di etichettatura unificata.

**Per supportare i computer disconnessi dal client Unified Labeling**:

1. Scegliere o creare un account utente in Azure AD che si utilizzerà per scaricare le etichette e le impostazioni dei criteri che si desidera utilizzare nel computer disconnesso.

2. Come impostazione dei criteri di etichetta aggiuntiva per questo account, [disabilitare l'invio dei dati di controllo a Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) usando l'impostazione avanzata **EnableAudit** .
    
    Si consiglia di eseguire questo passaggio perché se il computer disconnesso presenta una connettività Internet periodica, invierà le informazioni di registrazione a Azure Information Protection Analytics che include il nome utente del passaggio 1. Tale account utente potrebbe essere diverso dall'account locale in uso nel computer disconnesso.

3. Da un computer con connettività Internet con il client Unified Labeling installato e connesso con l'account utente del passaggio 1, scaricare le etichette e le impostazioni dei criteri.

4. Da questo computer esportare i file di log.
    
    Ad esempio, eseguire il cmdlet [Export-AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) oppure usare l'opzione **Esporta log** dalla finestra di dialogo [Guida e commenti](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client) del client. 
    
    I file di log vengono esportati come un singolo file compresso.

5.  Aprire il file compresso, quindi copiare i file con estensione XML dalla cartella MSIP.

6. Incollare questi file nella cartella **%LocalAppData%\Microsoft\MSIP** del computer disconnesso.

7. Se l'account utente scelto è uno che in genere si connette a Internet, abilitare di nuovo l'invio dei dati di controllo, impostando il valore di **EnableAudit** su **true**.

Tenere presente che se un utente del computer seleziona l'opzione **Reimposta impostazioni** da [Guida e commenti e suggerimenti](clientv2-admin-guide.md#help-and-feedback-section), questa azione Elimina i file di criteri e rende il client inutilizzabile fino a quando non si sostituiscono manualmente i file o il client si connette a Internet e Scarica i file.

Se il computer disconnesso esegue lo scanner Azure Information Protection, è necessario eseguire passaggi di configurazione aggiuntivi. Per altre informazioni, vedere [restrizione: il server dello scanner non può avere connettività Internet](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) dalle istruzioni per la distribuzione dello scanner.

## <a name="change-the-local-logging-level"></a>Modificare il livello di registrazione locale

Per impostazione predefinita, il client di Azure Information Protection Unified Labeling scrive i file di log del client nella cartella **%LocalAppData%\Microsoft\MSIP** . Questi file sono destinati al supporto tecnico Microsoft per la risoluzione dei problemi.
 
Per modificare il livello di registrazione per questi file, individuare il nome del valore seguente nel registro di sistema e impostare i dati del valore sul livello di registrazione richiesto:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

Impostare il livello di registrazione su uno dei valori seguenti:

- **Disattivato**: nessuna registrazione locale.

- **Errore**: solo errori.

- **Avviso**: errori e avvisi.

- **Info**: registrazione minima, che non include ID evento (impostazione predefinita per lo scanner).

- **Debug**: informazioni complete.

- **Trace**: registrazione dettagliata (impostazione predefinita per i client).

Questa impostazione del registro di sistema non modifica le informazioni inviate a Azure Information Protection per la [creazione di report centrali](../reports-aip.md).

## <a name="skip-or-ignore-files-during-scans-depending-on-file-attributes"></a>Ignora o ignora i file durante le analisi a seconda degli attributi di file

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, il Azure Information Protection scanner Unified Labeling analizza tutti i file rilevanti. Tuttavia, è possibile definire file specifici da ignorare, ad esempio per i file archiviati o i file che sono stati spostati. 

Consentire allo scanner di ignorare file specifici in base ai rispettivi attributi di file usando l'impostazione avanzata **ScannerFSAttributesToSkip** . Nel valore impostazione, elencare gli attributi di file che consentiranno di ignorare il file quando sono tutti impostati su **true**. Questo elenco di attributi di file usa la logica e.

I comandi di PowerShell di esempio seguenti illustrano come usare questa impostazione avanzata con un'etichetta denominata "Global".

**Ignorare i file di sola lettura e archiviati**

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY, FILE_ATTRIBUTE_ARCHIVE"}
```

**Ignorare i file di sola lettura o archiviati**

Per usare una logica o, eseguire più volte la stessa proprietà. Esempio:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY"}
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_ARCHIVE"}
```

> [!TIP]
> Si consiglia di provare ad abilitare lo scanner per ignorare i file con gli attributi seguenti:
> * FILE_ATTRIBUTE_SYSTEM
> * FILE_ATTRIBUTE_HIDDEN
> * FILE_ATTRIBUTE_DEVICE
> * FILE_ATTRIBUTE_OFFLINE
> * FILE_ATTRIBUTE_RECALL_ON_DATA_ACCESS
> * FILE_ATTRIBUTE_RECALL_ON_OPEN
> * FILE_ATTRIBUTE_TEMPORARY

Per un elenco di tutti gli attributi di file che possono essere definiti nell'impostazione avanzata **ScannerFSAttributesToSkip** , vedere [costanti degli attributi dei file Win32](/windows/win32/fileio/file-attribute-constants) .

## <a name="preserve-ntfs-owners-during-labeling-public-preview"></a>Mantieni i proprietari NTFS durante l'assegnazione di etichette (anteprima pubblica)

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

Per impostazione predefinita, lo scanner, PowerShell e l'etichetta di estensione di Esplora file non conservano il proprietario NTFS definito prima dell'assegnazione di etichette. 

Per assicurarsi che il valore del proprietario NTFS venga mantenuto, impostare l'impostazione avanzata **UseCopyAndPreserveNTFSOwner** su **true** per i criteri etichetta selezionati.

> [!CAUTION]
> Definire questa impostazione avanzata solo quando è possibile garantire una connessione di rete affidabile e a bassa latenza tra lo scanner e il repository sottoposto a scansione. Un errore di rete durante il processo di assegnazione automatica di etichette può causare la perdita del file.

Comando di PowerShell di esempio, quando il criterio dell'etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ UseCopyAndPreserveNTFSOwner ="true"}
```

> [!NOTE]
> Questa funzionalità è attualmente disponibile in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
> 

## <a name="customize-justification-prompt-texts-for-modified-labels"></a>Personalizzare i testi della richiesta di giustificazione per le etichette modificate

Personalizzare le richieste di giustificazione visualizzate in Office e nel client AIP, quando gli utenti finali cambiano le etichette di classificazione nei documenti e nei messaggi di posta elettronica.

Ad esempio, in qualità di amministratore, è consigliabile ricordare agli utenti di non aggiungere informazioni di identificazione dei clienti in questo campo:

:::image type="content" source="../media/justification-office.png" alt-text="Testo della richiesta di giustificazione personalizzata":::

Per modificare l' **altro** testo predefinito visualizzato, usare la proprietà avanzata **JustificationTextForUserText** con il cmdlet [set-LabelPolicy](/powershell/module/exchange/set-labelpolicy) . Impostare il valore sul testo che si desidera utilizzare.

Comando di PowerShell di esempio, quando il criterio dell'etichetta è denominato "globale":

``` PowerShell

[Set-LabelPolicy](/powershell/module/exchange/set-labelpolicy) -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
```

## <a name="customize-outlook-popup-messages"></a>Personalizzare i messaggi popup di Outlook

Gli amministratori di AIP possono personalizzare i messaggi popup visualizzati dagli utenti finali in Outlook, ad esempio:

- Messaggi per i messaggi di posta elettronica bloccati
- Messaggi di avviso che richiedono agli utenti di verificare il contenuto che stanno inviando
- Giustificare i messaggi che richiedono agli utenti di giustificare il contenuto che stanno inviando

> [!IMPORTANT]
> Questa procedura sostituirà tutte le impostazioni già definite usando la proprietà avanzata [OutlookUnlabeledCollaborationAction](#to-specify-a-different-action-for-email-messages-without-attachments) .
>
> In produzione è consigliabile evitare complicazioni *usando la* proprietà avanzata [OutlookUnlabeledCollaborationAction](#to-specify-a-different-action-for-email-messages-without-attachments) per definire le regole *o* definendo regole complesse con un file **JSON** come definito di seguito, ma non entrambi.
>

**Per personalizzare i messaggi popup di Outlook**:

1. Creare file con **estensione JSON** , ognuno con una regola che configura il modo in cui Outlook Visualizza i messaggi popup agli utenti. Per altre informazioni, vedere la [sintassi Rule value. JSON](#rule-value-json-syntax) e il [codice di esempio di personalizzazione di popup. JSON](#sample-popup-customization-json-code).

1. Usare PowerShell per definire le impostazioni avanzate che controllano i messaggi popup che si sta configurando. Eseguire un set separato di comandi per ogni regola che si desidera configurare.

    Ogni set di comandi di PowerShell deve includere il nome del criterio che si sta configurando, nonché la chiave e il valore che definisce la regola.

    Usare la sintassi seguente:

    ```PowerShell
    $filedata = Get-Content "<Path to json file>”
    Set-LabelPolicy -Identity <Policy name> -AdvancedSettings @{<Key> ="$filedata"}
    ```
    Dove: 

    - `<Path to json file>` è il percorso del file JSON creato. Ad esempio: **C:\Users\msanchez\Desktop\ \dlp\OutlookCollaborationRule_1.json**.
    - `<Policy name>` nome dei criteri che si desidera configurare. 
    - `<Key>` è un nome per la regola. Usare la sintassi seguente, dove **<#>** è il numero di serie della regola: 
    
        `OutlookCollaborationRule_<x>` 

    Per altre informazioni, vedere [ordering your Outlook Customization Rules](#ordering-your-outlook-customization-rules) and [Rule value JSON Syntax](#rule-value-json-syntax).

   
> [!TIP]
> Per un'organizzazione aggiuntiva, assegnare un nome al file con la stessa stringa della chiave usata nel comando di PowerShell. Ad esempio, denominare il file **OutlookCollaborationRule_1.json**, quindi usare anche **OutlookCollaborationRule_1** come chiave.
>
> Per assicurarsi che i popup vengano visualizzati anche quando i documenti vengono condivisi dall'esterno di Outlook **(File > condivisione > alleghino una copia)**, configurare anche l'impostazione avanzata di [PostponeMandatoryBeforeSave](#remove-not-now-for-documents-when-you-use-mandatory-labeling) .
> 

### <a name="ordering-your-outlook-customization-rules"></a>Ordinamento delle regole di personalizzazione di Outlook

AIP usa il numero di serie nella chiave immessa per determinare l'ordine in cui vengono elaborate le regole. Quando si definiscono le chiavi usate per ogni regola, definire le regole più restrittive con i numeri più bassi, seguite da regole meno restrittive con numeri più alti.

Quando viene trovata una corrispondenza di regola specifica, AIP interrompe l'elaborazione delle regole ed esegue l'azione associata alla regola di corrispondenza. (**Prima corrispondenza-> logica di uscita** )
    
**Esempio**:

Si consiglia di configurare tutti i messaggi di posta elettronica **interni** con un messaggio di **avviso** specifico, ma in genere non si desidera bloccarli. Tuttavia, si desidera impedire agli utenti di inviare allegati classificati come **segreti**, anche come messaggi di posta elettronica **interni** . 

In questo scenario, ordinare la chiave del **blocco Secret** Rule, che è la regola più specifica, prima dell'avviso più generico sulla chiave della regola **interna** :
- Per il messaggio di **blocco** : **OutlookCollaborationRule_1**
- Per il messaggio di **avviso** : **OutlookCollaborationRule_2**

### <a name="rule-value-json-syntax"></a>Sintassi value. JSON della regola

Definire la sintassi JSON della regola come segue:

``` JSON
"type" : "And",
"nodes" : []
```

È necessario disporre di almeno due nodi, il primo che rappresenta la condizione della regola e l'ultimo che rappresenta l'azione della regola. Per altre informazioni, vedere:

- [Sintassi della condizione della regola](#rule-condition-syntax)
- [Sintassi azione regola](#rule-action-syntax)

##### <a name="rule-condition-syntax"></a>Sintassi della condizione della regola

I nodi della condizione della regola devono includere il tipo di nodo e quindi le stesse condizioni. 

I tipi di nodo supportati includono:

|Tipo di nodo  |Descrizione  |
|---------|---------|
| **And**   | Esegue *e* in tutti i nodi figlio     |
| **Or**    |Esegue *o* in tutti i nodi figlio       |
| **Non**   | *Non* viene eseguito per il proprio figlio      |
| **Ad eccezione**    | Restituisce *not* per il proprio elemento figlio, facendo in modo che si comporti come **tutti**        |
| **SentTo**, seguito da **domini: listOfDomains**    |Verifica uno dei seguenti elementi: <br>-Se l'elemento padre è **except**, controlla se **tutti** i destinatari si trovano in uno dei domini<br>-Se l'elemento padre è qualsiasi altra **eccezione**, **verifica se uno dei destinatari** si trova in uno dei domini.   |
| **EMailLabel**, seguito da Label | I tipi validi sono:  <br>: ID etichetta <br>-null, se non con etichetta             |
| **AttachmentLabel**, seguito da **Label** ed **estensioni** supportate   | I tipi validi sono:  <br><br>**true**: <br>-Se l'elemento padre è **except**, controlla se **tutti** gli allegati con un'estensione supportata esistono nell'etichetta<br>-Se l'elemento padre è qualsiasi altra **eccezione**, verifica se **uno degli allegati** con un'estensione supportata esiste nell'etichetta <br>-Se non è etichettato e **Label = null** <br><br> **false**: per tutti gli altri casi <br><br>**Nota**: se la proprietà **Extensions** è vuota o mancante, nella regola vengono inclusi tutti i tipi di file supportati (estensioni).
| | |

#### <a name="rule-action-syntax"></a>Sintassi azione regola

Le azioni regola possono essere una delle seguenti:

|Azione  |Sintassi  |Messaggio di esempio  |
|---------|---------|---------|
|**Bloccato**     |    `Block (List<language, [title, body]>)`     |    **_Posta elettronica bloccata_* _<br /><br />  _You stanno per inviare contenuto classificato come **segreto** a uno o più destinatari non attendibili: *<br />* `rsinclair@contoso.com` *<br /><br />* i criteri dell'organizzazione non consentono questa operazione. Provare a rimuovere questi destinatari o a sostituire il contenuto. *|
|**Avvertire**     | `Warn (List<language,[title,body]>)`        |  **_Conferma richiesta_* _<br /><br />_You stanno per inviare contenuti classificati come **generali** a uno o più destinatari non attendibili: *<br />* `rsinclair@contoso.com` *<br /><br />* i criteri dell'organizzazione richiedono la conferma dell'invio del contenuto. *       |
|**Giustificare**     | `Justify (numOfOptions, hasFreeTextOption, List<language, [Title, body, options1,options2….]> )` <br /><br />Sono incluse fino a tre opzioni.        |  **_Giustificazione richiesta_* _ <br /><br />Per _Your criteri dell'organizzazione è necessario giustificare l'invio di contenuto classificato come **generale** a destinatari non attendibili. *<br /><br />* -Confermo che i destinatari sono approvati per condividere questo contenuto *<br />* : la condivisione approvata dal responsabile del contenuto *<br />* , come illustrato * |
| | | |

##### <a name="action-parameters"></a>Parametri di azione

Se per un'azione non viene specificato alcun parametro, i popup avranno il testo predefinito. 

Tutti i testi supportano i parametri dinamici seguenti: 

|Parametro  |Description  |
|---------|---------|
| `${MatchedRecipientsList}`  | Ultima corrispondenza per le condizioni di **SentTo**       |
| `${MatchedLabelName}`      | **Etichetta** posta/allegato, con il nome localizzato del criterio               |
| `${MatchedAttachmentName}` | Nome dell'allegato dall'ultima corrispondenza per la condizione **AttachmentLabel** |
| | |

> [!NOTE]
> Tutti i messaggi includono l'opzione **altre informazioni** , nonché le finestre di dialogo **Guida** e **Commenti** .
>
> Il **linguaggio** è il nome delle **impostazioni cultura** per il nome delle impostazioni locali, ad esempio: **inglese**  =  `en-us` ; **Spagnolo** = `es-es`
>
> Sono supportati anche i nomi di lingua solo padre, ad esempio `en` .
> 

### <a name="sample-popup-customization-json-code"></a>Esempio di personalizzazione di popup. codice JSON

I set di codice **JSON** seguenti illustrano come è possibile definire una serie di regole che controllano la modalità di visualizzazione dei messaggi popup per gli utenti in Outlook.

- [**Esempio 1**: bloccare i messaggi di posta elettronica o gli allegati interni](#example-1-block-internal-emails-or-attachments)
- [**Esempio 2**: bloccare gli allegati di Office non classificati](#example-2-block-unclassified-office-attachments)
- [**Esempio 3**: richiedere all'utente di accettare l'invio di un messaggio di posta elettronica o un allegato riservato](#example-3-require-the-user-to-accept-sending-a-confidential-email-or-attachment)
- [**Esempio 4**: avvisare la posta elettronica senza etichetta e un allegato con un'etichetta specifica](#example-4-warn-on-mail-with-no-label-and-an-attachment-with-a-specific-label)
- [**Esempio 5**: richiedere una giustificazione, con due opzioni predefinite e un'opzione aggiuntiva per il testo libero](#example-5-prompt-for-a-justification-with-two-predefined-options-and-an-extra-free-text-option)

#### <a name="example-1-block-internal-emails-or-attachments"></a>Esempio 1: bloccare i messaggi di posta elettronica o gli allegati interni

Il codice **JSON** seguente bloccherà i messaggi di posta elettronica o gli allegati classificati come **interni** da impostati su destinatari esterni.

In questo esempio, **89a453df-5df4-4976-8191-259d0cf9560a** è l'ID dell'etichetta **interna** e i domini interni includono **contoso.com** e **Microsoft.com**.

Poiché non è specificata alcuna estensione specifica, vengono inclusi tutti i tipi di file supportati.

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
              "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",             
                    "LabelId" : "89a453df-5df4-4976-8191-259d0cf9560a"      
                },{                     
                    "type" : "EmailLabel",                  
                    "LabelId" : "89a453df-5df4-4976-8191-259d0cf9560a"              
                }
            ]
        },      
        {           
            "type" : "Block",           
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "The email or at least one of the attachments is classified as <Bold>${MatchedLabelName}</Bold>. Documents classified as <Bold> ${MatchedLabelName}</Bold> cannot be sent to external recipients (${MatchedRecipientsList}).<br><br>List of attachments classified as <Bold>${MatchedLabelName}</Bold>:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance with classification requirements as per Contoso’s policies."               
                },              
                "es-es": {                
                    "Title": "Correo electrónico bloqueado",                  
                    "Body": "El correo electrónico o al menos uno de los archivos adjuntos se clasifica como <Bold> ${MatchedLabelName}</Bold>."                
                }           
            },          
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-2-block-unclassified-office-attachments"></a>Esempio 2: bloccare gli allegati di Office non classificati

Il codice **JSON** seguente blocca l'invio di messaggi di posta elettronica o allegati di Office non classificati a destinatari esterni.

Nell'esempio seguente, l'elenco degli allegati che richiede l'assegnazione di etichette è: **. doc,. docm,. docx,. dot,. dotm,. dotx, potm, potx, PPS, ppsm, PPSX, PPT, pptm, pptx, VDW, VSD, vsdm, vsdx, VSS, vssm,. VST,. vstm,. vssx,. vstx,. xls,. xlsb,. xlt,. xlsm,. xlsx,. xltm,. xltx**

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                    "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".doc",
                                    ".docm",
                                    ".docx",
                                    ".dot",
                                    ".dotm",
                                    ".dotx",
                                    ".potm",
                                    ".potx",
                                    ".pps",
                                    ".ppsm",
                                    ".ppsx",
                                    ".ppt",
                                    ".pptm",
                                    ".pptx",
                                    ".vdw",
                                    ".vsd",
                                    ".vsdm",
                                    ".vsdx",
                                    ".vss",
                                    ".vssm",
                                    ".vst",
                                    ".vstm",
                                    ".vssx",
                                    ".vstx",
                                    ".xls",
                                    ".xlsb",
                                    ".xlt",
                                    ".xlsm",
                                    ".xlsx",
                                    ".xltm",
                                    ".xltx"
                                 ]
                    
                },{                     
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Emailed Blocked",                   
                    "Body": "Classification is necessary for attachments to be sent to external recipients.<br><br>List of attachments that are not classified:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>For MS Office documents, classify and send again.<br><br>For PDF files, classify the document or classify the email (using the most restrictive classification level of any single attachment or the email content) and send again."               
                },              
                "es-es": {                
                    "Title": "Correo electrónico bloqueado",                  
                    "Body": "La clasificación es necesaria para que los archivos adjuntos se envíen a destinatarios externos."              
                }           
            },          
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-3-require-the-user-to-accept-sending-a-confidential-email-or-attachment"></a>Esempio 3: richiedere all'utente di accettare l'invio di un messaggio di posta elettronica o un allegato riservato

Nell'esempio seguente Outlook visualizza un messaggio che avvisa l'utente che sta inviando un messaggio di posta elettronica o un allegato **riservato** ai destinatari esterni e richiede **anche che l'utente selezioni accetto**. 

Questo tipo di messaggio di avviso viene tecnicamente considerato una giustificazione, in quanto l'utente deve **selezionare Accetto**.

Poiché non è specificata alcuna estensione specifica, vengono inclusi tutti i tipi di file supportati.

``` PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                    "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",             
                    "LabelId" : "3acd2acc-2072-48b1-80c8-4da23e245613"      
                },{                     
                    "type" : "EmailLabel",                  
                    "LabelId" : "3acd2acc-2072-48b1-80c8-4da23e245613"              
                }
            ]
        },      
        {           
            "type" : "Justify",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Warning",                   
                    "Body": "You are sending a document that is classified as <Bold>${MatchedLabelName}</Bold> to at least one external recipient. Please make sure that the content is correctly classified and that the recipients are entitled to receive this document.<br><br>List of attachments classified as <Bold>${MatchedLabelName}</Bold>:<br><br>${MatchedAttachmentName}<br><br><Bold>List of external email addresses:</Bold><br>${MatchedRecipientsList})<br><br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br><Bold>Acknowledgement</Bold><br>By clicking <Bold>I accept<\Bold> below, you confirm that the recipient is entitled to receive the content and the communication complies with CS Policies and Standards",
                    "Options": [                        
                        "I accept"              
                    ] 
                },              
                "es-es": {                
                    "Title": "Advertencia",                   
                    "Body": "Está enviando un documento clasificado como <Bold>${MatchedLabelName}</Bold> a al menos un destinatario externo. Asegúrese de que el contenido esté correctamente clasificado y que los destinatarios tengan derecho a recibir este documento.",
                    "Options": [                        
                        "Acepto"                    
                    ]                   
                }           
            },          
            "HasFreeTextOption":"false",            
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-4-warn-on-mail-with-no-label-and-an-attachment-with-a-specific-label"></a>Esempio 4: avvisare la posta elettronica senza etichetta e un allegato con un'etichetta specifica

Il **codice JSON** seguente fa in modo che Outlook avvisi l'utente quando invia un messaggio di posta elettronica interno senza etichetta, con un allegato con un'etichetta specifica. 

In questo esempio, **bcbef25a-c4db-446b-9496-1b558d9edd0e** è l'ID dell'etichetta dell'allegato e la regola si applica ai file con estensione docx, xlsx e PPTX.

Per impostazione predefinita, i messaggi di posta elettronica con allegati con etichetta non ricevono automaticamente la stessa etichetta.

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "EmailLabel",
                     "LabelId" : null           
        },
        {
          "type": "AttachmentLabel",
          "LabelId": "bcbef25a-c4db-446b-9496-1b558d9edd0e",
          "Extensions": [
                ".docx",
                ".xlsx",
                ".pptx"
             ]
        },
    {           
            "type" : "SentTo",              
            "Domains" : [               
                "contoso.com",              
            ]           
        },      
        {           
            "type" : "Warn" 
        }   
    ] 
}
```

#### <a name="example-5-prompt-for-a-justification-with-two-predefined-options-and-an-extra-free-text-option"></a>Esempio 5: richiedere una giustificazione, con due opzioni predefinite e un'opzione aggiuntiva per il testo libero

Il codice **JSON** seguente causa la richiesta da parte di Outlook all'utente di una giustificazione per l'azione. Il testo della giustificazione include due opzioni predefinite, oltre a una terza opzione di testo libero.

Poiché non è specificata alcuna estensione specifica, vengono inclusi tutti i tipi di file supportati.

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                                  
                ]               
            }       
        },      
        {           
            "type" : "EmailLabel",          
            "LabelId" : "34b8beec-40df-4219-9dd4-553e1c8904c1"      
        },      
        {           
            "type" : "Justify",             
            "LocalizationData": {               
                "en-us": {                  
                    "Title": "Justification Required",                  
                    "Body": "Your organization policy requires justification for you to send content classified as <Bold> ${MatchedLabelName}</Bold>,to untrusted recipients:<br>Recipients are: ${MatchedRecipientsList}",                     
                    "Options": [                        
                        "I confirm the recipients are approved for sharing this content",                   
                        "My manager approved sharing of this content",                      
                        "Other, as explained"                   
                    ]               
                },              
                "es-es": {                  
                    "Title": "Justificación necesaria",                     
                    "Body": "La política de su organización requiere una justificación para que envíe contenido clasificado como <Bold> ${MatchedLabelName}</Bold> a destinatarios que no sean de confianza.",                  
                    "Options": [                        
                        "Confirmo que los destinatarios están aprobados para compartir este contenido.",
                        "Mi gerente aprobó compartir este contenido",
                        "Otro, como se explicó"                     
                    ]               
                }           
            },          
            "HasFreeTextOption":"true",             
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

## <a name="configure-sharepoint-timeouts"></a>Configurare i timeout di SharePoint

Per impostazione predefinita, il timeout per le interazioni di SharePoint è di due minuti, dopo il quale l'operazione di AIP tentata ha esito negativo.

A partire dalla [versione 2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850), gli amministratori di AIP possono controllare questo timeout usando le proprietà avanzate seguenti, usando una sintassi **hh: mm: SS** per definire i timeout:

- **SharepointWebRequestTimeout**. Determina il timeout per tutte le richieste Web AIP a SharePoint. Impostazione predefinita = 2 minuti.

    Ad esempio, se il criterio è denominato **Global**, il seguente comando di PowerShell di esempio aggiorna il timeout della richiesta Web a 5 minuti.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{SharepointWebRequestTimeout="00:05:00"}
    ```

- **SharepointFileWebRequestTimeout**. Determina il timeout specifico per i file di SharePoint tramite le richieste Web AIP. Impostazione predefinita = 15 minuti

    Ad esempio, se il criterio è denominato **globale**, il seguente comando di PowerShell di esempio aggiorna il timeout della richiesta Web del file a 10 minuti.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{SharepointFileWebRequestTimeout="00:10:00"}
    ```

### <a name="avoid-scanner-timeouts-in-sharepoint"></a>Evitare i timeout dello scanner in SharePoint

Se si dispone di percorsi di file lunghi in SharePoint versione 2013 o successiva, verificare che il valore [httpRuntime. maxUrlLength](/dotnet/api/system.web.configuration.httpruntimesection.maxurllength) del server SharePoint sia maggiore di quello predefinito di 260 caratteri.

Questo valore è definito nella classe **HttpRuntimeSection** della `ASP.NET` configurazione. 

**Per aggiornare la classe HttpRuntimeSection**:

1. Eseguire il backup della configurazione del **web.config** . 

1. Aggiornare il valore di **maxUrlLength** in base alle esigenze. Esempio:

    ```c#
    <httpRuntime maxRequestLength="51200" requestValidationMode="2.0" maxUrlLength="5000"  />
    ```

1. Riavviare il server Web di SharePoint e verificare che venga caricato correttamente. 

    Ad esempio, in gestione Windows Internet Information Server (IIS) selezionare il sito e quindi in **Gestisci sito Web** selezionare **Riavvia**. 

## <a name="prevent-outlook-performance-issues-with-smime-emails"></a>Impedisci problemi di prestazioni di Outlook con messaggi di posta elettronica S/MIME

I problemi di prestazioni possono verificarsi in Outlook quando i messaggi di posta elettronica S/MIME sono aperti nel riquadro di lettura. Per evitare questi problemi, abilitare la proprietà avanzata **OutlookSkipSmimeOnReadingPaneEnabled** . 

L'abilitazione di questa proprietà impedisce che la barra di AIP e le classificazioni di posta elettronica vengano visualizzate nel riquadro di lettura.

Ad esempio, se il criterio è denominato **Global**, il comando di PowerShell di esempio seguente abilita la proprietà **OutlookSkipSmimeOnReadingPaneEnabled** :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookSkipSmimeOnReadingPaneEnabled="true"}
```

## <a name="turn-off-document-tracking-features-public-preview"></a>Disattiva le funzionalità di rilevamento dei documenti (anteprima pubblica)

Per impostazione predefinita, le funzionalità di rilevamento dei documenti sono attivate per il tenant. Per disabilitarle, ad esempio per i requisiti di privacy nella organizzazione o nell'area, impostare il valore di **EnableTrackAndRevoke** su **false**.

Una volta disattivato, i dati di rilevamento dei documenti non saranno più disponibili nell'organizzazione e gli utenti non visualizzeranno più l'opzione di menu [**Revoke**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) nelle app di Office.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **EnableTrackAndRevoke**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableTrackAndRevoke="False"}
```

Dopo aver impostato questo valore su **false**, Track and Revoke è disattivato come indicato di seguito: 

- L'apertura di documenti protetti con il client AIP Unified Labeling non registra più i documenti per Track and Revoke.
- Gli utenti finali non visualizzeranno più l'opzione di menu [**Revoke**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) nelle app di Office.

Tuttavia, i documenti protetti già registrati per il rilevamento continueranno a essere monitorati e gli amministratori potranno comunque revocare l'accesso da PowerShell. Per disattivare completamente le funzionalità di rilevamento e revoca, eseguire anche il cmdlet [Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) .

Questa configurazione usa un' [impostazione avanzata](#configuring-advanced-settings-for-the-client-via-powershell) dei criteri che è necessario configurare usando Office 365 Security & Compliance Center PowerShell.

> [!NOTE]
> Per attivare di nuovo Tracking e REVOKE, impostare **EnableTrackAndRevoke** su **true** ed eseguire anche il cmdlet [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature) .
>
## <a name="next-steps"></a>Passaggi successivi

Ora che è stato personalizzato il client di etichettatura Azure Information Protection Unified, vedere le risorse seguenti per altre informazioni che potrebbero essere necessarie per supportare questo client:

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)