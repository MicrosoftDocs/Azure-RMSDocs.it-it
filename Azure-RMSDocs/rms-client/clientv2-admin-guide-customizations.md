---
title: Configurazioni personalizzate-Azure Information Protection client per l'assegnazione di etichette unificata
description: Informazioni sulla personalizzazione del client di Azure Information Protection Unified Labeling per Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b18beab3c6a2dd3b01991fdb9755b943ec62fe5a
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117698"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guida dell'amministratore: configurazioni personalizzate per il client di Azure Information Protection Unified Labeling

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client di Azure Information Protection Unified labeling.

Per queste impostazioni è necessario modificare il registro di sistema o specificare impostazioni avanzate. Le impostazioni avanzate usano [Office 365 Centro sicurezza e conformità PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps).

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Come configurare le impostazioni avanzate per il client usando Office 365 Centro sicurezza e conformità PowerShell

Quando si usa Office 365 Centro sicurezza e conformità PowerShell, è possibile configurare le impostazioni avanzate che supportano le personalizzazioni per i criteri etichette e le etichette. Ad esempio:

- L'impostazione per visualizzare la barra di Information Protection nelle app di Office è un' ***impostazione avanzata dei criteri***per le etichette.
- L'impostazione per specificare un colore dell'etichetta è un' ***impostazione avanzata etichetta***.

In entrambi i casi, dopo la [connessione a Office 365 Centro sicurezza e conformità PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps), specificare il parametro *AdvancedSettings* con l'identità (nome o GUID) del criterio o dell'etichetta e specificare le coppie chiave/valore in una [tabella hash](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables). Usare la sintassi seguente:

Per un'impostazione dei criteri di etichetta, valore stringa singola:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

Per le impostazioni dei criteri di etichetta, più valori stringa per la stessa chiave:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Per un'impostazione di etichetta, valore stringa singola:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

Per le impostazioni delle etichette, più valori stringa per la stessa chiave:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Per rimuovere un'impostazione avanzata, utilizzare la stessa sintassi ma specificare un valore di stringa null.


#### <a name="examples-for-setting-advanced-settings"></a>Esempi per l'impostazione di impostazioni avanzate

Esempio 1: impostare un'impostazione avanzata dei criteri per le etichette per un singolo valore stringa:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

Esempio 2: impostare un'impostazione avanzata etichetta per un valore stringa singolo:

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

Esempio 3: impostare un'impostazione avanzata etichetta per più valori stringa:

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

Esempio 4: rimuovere un'impostazione avanzata dei criteri di etichetta specificando un valore stringa null:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>Specifica dell'identità per il criterio etichetta o l'etichetta

Specificare il nome dei criteri di etichetta per il parametro *Identity* di PowerShell è semplice perché nel centro di amministrazione è presente un solo nome di criteri in cui si gestiscono i criteri di etichetta. Per le etichette, tuttavia, nel centro di amministrazione vengono visualizzati sia un **nome** che un **nome visualizzato** . In alcuni casi, il valore di entrambi gli elementi sarà lo stesso, ma possono essere diversi:

- **Nome** è il nome originale dell'etichetta ed è univoco in tutte le etichette. Se si modifica il nome dell'etichetta dopo che è stata creata, questo valore rimane invariato. Per le etichette di cui è stata eseguita la migrazione da Azure Information Protection, è possibile che venga visualizzato l'ID etichetta dell'etichetta dall'portale di Azure.

- **Nome visualizzato** è il nome dell'etichetta visualizzata dagli utenti e non è necessario che sia univoco in tutte le etichette. Ad esempio, gli utenti visualizzano una sottoetichetta **tutti i dipendenti** per l'etichetta **riservata** e un'altra sottoetichetta **tutti i dipendenti** per l'etichetta **riservatezza elevata** . Queste etichette secondarie visualizzano entrambi lo stesso nome, ma non hanno la stessa etichetta e hanno impostazioni diverse.

Per configurare le impostazioni avanzate dell'etichetta, usare il valore **nome** . Ad esempio, per identificare l'etichetta nell'immagine seguente, è necessario specificare `-Identity "All Company"`:

![Usare "Name" invece di "nome visualizzato" per identificare un'etichetta di riservatezza](../media/labelname_scc.png)

Se si preferisce specificare il GUID dell'etichetta, questo valore non viene visualizzato nell'interfaccia di amministrazione in cui si gestiscono le etichette. Tuttavia, è possibile usare il comando seguente di Office 365 Centro sicurezza e conformità PowerShell per trovare questo valore:

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Ordine di precedenza-come vengono risolte le impostazioni in conflitto

Usando uno dei centri di amministrazione in cui si gestiscono le etichette di riservatezza, è possibile configurare le impostazioni dei criteri di etichetta seguenti:

- **Per impostazione predefinita, applicare questa etichetta ai documenti e ai messaggi di posta elettronica**

- **Gli utenti devono fornire la giustificazione per rimuovere un'etichetta o un'etichetta di classificazione inferiore**

- **Richiedi agli utenti di applicare un'etichetta al messaggio di posta elettronica o al documento**

- **Fornire agli utenti un collegamento a una pagina della Guida personalizzata**

Quando per un utente sono configurati più criteri di etichetta, ognuno con impostazioni di criteri potenzialmente diverse, l'ultima impostazione dei criteri viene applicata in base all'ordine dei criteri nell'interfaccia di amministrazione. Per ulteriori informazioni, vedere [priorità dei criteri delle etichette (ordine degli ordini)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters)

Le impostazioni avanzate dell'etichetta seguono la stessa logica per la precedenza: quando un'etichetta si trova in più criteri etichetta e l'etichetta ha impostazioni avanzate, l'ultima impostazione avanzata viene applicata in base all'ordine dei criteri nell'interfaccia di amministrazione.

Le impostazioni avanzate dei criteri di etichetta vengono applicate in ordine inverso: con un'eccezione, vengono applicate le impostazioni avanzate del primo criterio, in base all'ordine dei criteri nell'interfaccia di amministrazione. L'eccezione è l'impostazione avanzata *OutlookDefaultLabel*, che imposta un'etichetta predefinita diversa per Outlook. Solo per questa impostazione avanzata dei criteri di etichetta, l'ultima impostazione viene applicata in base all'ordine dei criteri nell'interfaccia di amministrazione.

#### <a name="available-advanced-settings-for-label-policies"></a>Impostazioni avanzate disponibili per i criteri delle etichette

Usare il parametro *AdvancedSettings* con [New-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-labelpolicy?view=exchange-ps) e [set-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps).

|Impostazioni|Scenario e istruzioni|
|----------------|---------------|
|AttachmentAction|[Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|DisableMandatoryInOutlook|[Esentare i messaggi di Outlook da un'etichetta obbligatoria](#exempt-outlook-messages-from-mandatory-labeling)
|EnableAudit|[Disabilitare l'invio di dati di controllo a Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|EnableCustomPermissions|[Disabilitare le autorizzazioni personalizzate in Esplora file](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|EnableLabelBySharePointProperties|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
|HideBarByDefault|[Visualizza la barra di Information Protection nelle app Office](#display-the-information-protection-bar-in-office-apps)|
|LogMatchedContent|[Invia corrispondenze del tipo di informazioni a Azure Information Protection Analytics](#send-information-type-matches-to-azure-information-protection-analytics)|
|OutlookBlockTrustedDomains|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Impostare un'etichetta predefinita diversa per Outlook](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Abilitare la classificazione consigliata in Outlook](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PFileSupportedExtensions|[Modificare i tipi di file da proteggere](#change-which-file-types-to-protect)|
|PostponeMandatoryBeforeSave|[Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Aggiungere "Segnala un problema" per gli utenti](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[Disabilitare l'invio di informazioni riservate individuate nei documenti a Azure Information Protection Analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|ScannerConcurrencyLevel|[Limitare il numero di thread usati dallo scanner](#limit-the-number-of-threads-used-by-the-scanner)|

Esempio di comando di PowerShell per verificare le impostazioni dei criteri di etichetta attive per un criterio etichetta denominato "globale":

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>Impostazioni avanzate disponibili per le etichette

Usare il parametro *AdvancedSettings* con [New-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) e [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

|Impostazioni|Scenario e istruzioni|
|----------------|---------------|
|colore|[Specificare un colore per l'etichetta](#specify-a-color-for-the-label)|
|customPropertiesByLabel|[Applicare una proprietà personalizzata quando viene applicata un'etichetta](#apply-a-custom-property-when-a-label-is-applied)|
|DefaultSubLabelId|[Specificare un'etichetta secondaria predefinita per un'etichetta padre](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|SMimeEncrypt|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|

Esempio di comando di PowerShell per verificare le impostazioni dell'etichetta attive per un'etichetta denominata "public":

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>Visualizza la barra di Information Protection nelle app Office

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Per impostazione predefinita, gli utenti devono selezionare l'opzione **Mostra barra** dal pulsante **sensibilità** per visualizzare la barra di Information Protection nelle app di Office. Usare la chiave **HideBarByDefault** e impostare il valore su **false** per visualizzare automaticamente questa barra per gli utenti in modo che sia possibile selezionare le etichette dalla barra o dal pulsante. 

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **HideBarByDefault**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Esentare i messaggi di Outlook da un'etichetta obbligatoria

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Per impostazione predefinita, quando si Abilita l'impostazione dei criteri di etichetta di **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, tutti i documenti salvati e i messaggi di posta elettronica inviati devono avere un'etichetta applicata. Quando si configura l'impostazione avanzata seguente, l'impostazione dei criteri si applica solo ai documenti di Office e non ai messaggi di Outlook.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **DisableMandatoryInOutlook**

- Valore: **True**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}

## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **OutlookRecommendationEnabled**

- Valore: **True**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata come impostazione dei criteri per l'opzione **applica questa etichetta per impostazione predefinita a documenti e messaggi di posta elettronica**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **OutlookDefaultLabel**

- Valore: \<**GUID etichetta**> o **None**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}

## <a name="change-which-file-types-to-protect"></a>Modificare i tipi di file da proteggere

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Per impostazione predefinita, il client Azure Information Protection Unified Labeling protegge tutti i tipi di file e lo scanner dal client protegge solo i tipi di file di Office e i file PDF.

È possibile modificare questo comportamento predefinito per i criteri di etichetta selezionati, specificando quanto segue:

- Chiave: **PFileSupportedExtensions**

- Valore: **<string value>** 

Usare la tabella seguente per identificare il valore stringa da specificare:

| Valore stringa| Client| Scanner|
|-------------|-------|--------|
|\*|Valore predefinito: applicare la protezione a tutti i tipi di file|Applicare la protezione a tutti i tipi di file|
|\<valore null >| Applicare la protezione ai tipi di file di Office e ai file PDF| Valore predefinito: applicare la protezione ai tipi di file di Office e ai file PDF|
|ConvertTo-JSON (". jpg", ". png")|Oltre ai tipi di file di Office e ai file PDF, applicare la protezione alle estensioni di file specificate | Oltre ai tipi di file di Office e ai file PDF, applicare la protezione alle estensioni di file specificate

Esempio 1: comando di PowerShell per il client unificato per proteggere solo i tipi di file di Office e i file PDF, in cui il criterio dell'etichetta è denominato "client":

    Set-LabelPolicy -Identity Client -AdvancedSettings @{PFileSupportedExtensions=""}

Esempio 2: comando di PowerShell per lo scanner per proteggere tutti i tipi di file, in cui il criterio dell'etichetta è denominato "scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Esempio 3: comando di PowerShell per lo scanner per proteggere i file con estensione txt e CSV, oltre ai file di Office e PDF, in cui il criterio dell'etichetta è denominato "scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}

Con questa impostazione è possibile modificare i tipi di file protetti, ma non è possibile modificare il livello di protezione predefinito da nativo a generico. Ad esempio, per gli utenti che eseguono il client di etichettatura unificata, è possibile modificare l'impostazione predefinita in modo che siano protetti solo i file di Office e i file PDF anziché tutti i tipi di file. Tuttavia, non è possibile modificare questi tipi di file in modo da essere protetti in modo generico con un'estensione di file. Pfile.

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si usa l'impostazione dei criteri di etichetta di **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, agli utenti viene richiesto di selezionare un'etichetta quando salvano per la prima volta un documento di Office e inviano un messaggio di posta elettronica. Per i documenti, gli utenti possono selezionare **Non ora** per chiudere temporaneamente la richiesta di selezionare un'etichetta e tornare al documento. Non possono però chiudere il documento salvato senza etichettarlo. 

Quando si configura questa impostazione l'opzione **Non ora** viene rimossa. In questo modo, quando il documento viene salvato per la prima volta gli utenti sono obbligati a selezionare un'etichetta.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **PostponeMandatoryBeforeSave**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette

Questa configurazione USA [le impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Esistono due metodi che possono essere usati per rimuovere le classificazioni da altre soluzioni di assegnazione di etichette. Il primo metodo rimuove qualsiasi forma da documenti di Word in cui il nome della forma corrisponde al nome definito nella proprietà avanzata **WordShapeNameToRemove**, il secondo metodo consente di rimuovere o sostituire intestazioni o piè di pagina basati su testo da documenti di Word, Excel e PowerPoint come definito nella proprietà avanzata **RemoveExternalContentMarkingInApp** . 

### <a name="use-the-wordshapenametoremove-advanced-property-preview"></a>Usare la proprietà avanzata WordShapeNameToRemove (anteprima)

*La proprietà avanzata **WordShapeNameToRemove** è supportata dalla versione 2.6.101.0 e successive*

Questa impostazione consente di rimuovere o sostituire etichette basate su forme da documenti di Word quando tali contrassegni visivi sono stati applicati da un'altra soluzione di assegnazione di etichette. Ad esempio, la forma contiene il nome di un'etichetta precedente a cui è stata eseguita la migrazione in etichette di riservatezza per usare un nuovo nome di etichetta e la relativa forma.

Per usare questa proprietà avanzata, è necessario trovare il nome della forma nel documento di Word e quindi definirli nell'elenco delle proprietà avanzate **WordShapeNameToRemove** di forme. Il servizio rimuoverà qualsiasi forma in Word che inizia con un nome definito nell'elenco di forme in questa proprietà avanzata.

Evitare di rimuovere le forme che contengono il testo che si desidera ignorare, definendo il nome di tutte le forme da rimuovere ed evitando di controllare il testo in tutte le forme, ovvero un processo che richiede un utilizzo intensivo delle risorse.

Se non si specificano le forme parola in questa impostazione aggiuntiva di proprietà avanzata e Word viene incluso nel valore della chiave **RemoveExternalContentMarkingInApp** , verranno controllate tutte le forme per il testo specificato nel valore **ExternalContentMarkingToRemove** . 

Per trovare il nome della forma che si sta utilizzando e si desidera escludere:

1. In Word visualizzare il riquadro di **selezione** : **scheda Home** > gruppo di **modifica** > **selezionare** l'opzione > riquadro di **selezione**.

2. Selezionare la forma nella pagina che si desidera contrassegnare per la rimozione. Il nome della forma contrassegnata è ora evidenziato nel riquadro di **selezione** .

Usare il nome della forma per specificare un valore stringa per la chiave * * * * WordShapeNameToRemove * * * *. 

Esempio: il nome della forma è **DC**. Per rimuovere la forma con questo nome, specificare il valore: `dc`.

- Chiave: **WordShapeNameToRemove**

- Valore: \<**nome della forma Word**> 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}

Quando si dispone di più di una forma di parola da rimuovere, specificare tutti i valori disponibili per la rimozione delle forme.


### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>Usare la proprietà avanzata RemoveExternalContentMarkingInApp
Questa impostazione consente di rimuovere o sostituire intestazioni o piè di pagina basati su testo da documenti quando tali contrassegni visivi sono stati applicati da un'altra soluzione di assegnazione di etichette. Il piè di pagina precedente, ad esempio, contiene il nome di una vecchia etichetta a cui è stata eseguita la migrazione in etichette di riservatezza per usare un nuovo nome di etichetta e il relativo piè di pagina.

Quando il client di etichettatura unificata ottiene questa configurazione nel criterio, le intestazioni e i piè di pagina precedenti vengono rimossi o sostituiti quando il documento viene aperto nell'app di Office ed è applicata qualsiasi etichetta di riservatezza al documento.

Questa configurazione non è supportata per Outlook e tenere presente che quando viene usata con Word, Excel e PowerPoint, può influire negativamente sulle prestazioni di queste app per gli utenti. La configurazione consente di definire le impostazioni per ogni applicazione, ad esempio la ricerca di testo nelle intestazioni e nei piè di pagina di documenti di Word, ma non nei fogli di calcolo di Excel o nelle presentazioni di PowerPoint.

Poiché la corrispondenza dei criteri influiscono sulle prestazioni degli utenti, è consigliabile limitare i tipi di applicazioni di Office (**W**Ord, E**X**cel, **P**owerPoint) solo a quelli che devono essere cercati.

Per i criteri etichetta selezionati specificare le stringhe seguenti:

- Chiave: **RemoveExternalContentMarkingInApp**

- Valore: \<**tipi di applicazioni di Office WXP**> 

Di seguito sono riportati alcuni esempi.

- Per eseguire la ricerca solo in documenti di Word, specificare **W**.

- Per eseguire la ricerca in documenti di Word e presentazioni di PowerPoint, specificare **WP**.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

Sarà necessaria almeno un'altra impostazione client avanzata, **ExternalContentMarkingToRemove**, per specificare il contenuto dell'intestazione o del piè di pagina e il modo in cui rimuoverlo o sostituirlo.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Come configurare ExternalContentMarkingToRemove

Quando si specifica il valore stringa per la chiave **ExternalContentMarkingToRemove**, sono disponibili tre opzioni che usano le espressioni regolari:

- Corrispondenza parziale per rimuovere tutto il contenuto dell'intestazione o del piè di pagina.
    
    Esempio: le intestazioni o i piè di pagina contengono la stringa **TEXT TO REMOVE**. Per rimuovere completamente le intestazioni o i piè di pagina, specificare il valore: `*TEXT*`.

- Corrispondenza completa per rimuovere solo determinate parole nell'intestazione o nel piè di pagina.
    
    Esempio: le intestazioni o i piè di pagina contengono la stringa **TEXT TO REMOVE**. Per rimuovere solo la parola **TEXT**, lasciando la stringa **TO REMOVE** nell'intestazione o nel piè di pagina, specificare il valore: `TEXT `.

- Corrispondenza completa per rimuovere tutto il contenuto dell'intestazione o del piè di pagina.
    
    Esempio: le intestazioni o i piè di pagina contengono la stringa **TEXT TO REMOVE**. Per rimuovere le intestazioni o i piè di pagina che contengono esattamente questa stringa, specificare il valore: `^TEXT TO REMOVE$`.
    

I criteri di ricerca per la stringa specificata non fanno distinzione tra maiuscole e minuscole. La lunghezza massima della stringa è 255 caratteri.

Poiché alcuni documenti potrebbero includere caratteri invisibili o tipi diversi di spazi o tabulazioni, la stringa specificata per una frase potrebbe non essere rilevata. Quando possibile, specificare una singola parola distintiva per il valore e assicurarsi di testare i risultati prima della distribuzione nell'ambiente di produzione.

Per gli stessi criteri di etichetta specificare le stringhe seguenti:

- Chiave: **ExternalContentMarkingToRemove**

- Valore: \<**stringa da confrontare, definita come espressione regolare**> 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>Intestazioni o piè di pagina su più righe

Se il testo di un'intestazione o un piè di pagina è su più righe, creare una chiave e un valore per ogni riga. Si supponga, ad esempio, di avere il piè di pagina seguente con due righe:

**The file is classified as Confidential**

**Label applied manually**

Per rimuovere il piè di pagina su più righe, creare le due voci seguenti per gli stessi criteri di etichetta:

- Chiave: **ExternalContentMarkingToRemove**

- Valore chiave 1: **\*Confidential***

- Valore chiave 2: **\*Label applied*** 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>Ottimizzazione per PowerPoint

I piè di pagina in PowerPoint vengono implementati come forme. Per evitare la rimozione di forme che contengono il testo specificato ma non sono intestazioni o piè di pagina, usare un'impostazione client avanzata aggiuntiva denominata **PowerPointShapeNameToRemove**. È consigliabile usare questa impostazione anche per evitare di controllare il testo in tutte le forme, essendo un processo a elevato utilizzo di risorse.

Se non si specifica questa impostazione client avanzata aggiuntiva e PowerPoint è incluso nel valore della chiave **RemoveExternalContentMarkingInApp**, il testo specificato nel valore **ExternalContentMarkingToRemove** verrà ricercato in tutte le forme. 

Per trovare il nome della forma usata come intestazione o piè di pagina:

1. In PowerPoint visualizzare il riquadro **Selezione**: scheda **Formato** > gruppo **Disponi** > **Riquadro di selezione**.

2. Selezionare la forma sulla diapositiva contenente l'intestazione o il piè di pagina. Il nome della forma selezionata viene evidenziato nel riquadro **Selezione**.

Usare il nome della forma per specificare un valore stringa per la chiave **PowerPointShapeNameToRemove**. 

Esempio: il nome della forma è **fc**. Per rimuovere la forma con questo nome, specificare il valore: `fc`.

- Chiave: **PowerPointShapeNameToRemove**

- Valore: \<**nome delle forma di PowerPoint**> 

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

Quando si dispone di più di una forma di PowerPoint da rimuovere, specificare tutti i valori disponibili per le forme da rimuovere.

Per impostazione predefinita, il testo delle intestazioni e dei piè di pagina viene cercato solo negli schemi diapositiva. Per estendere la ricerca a tutte le diapositive, che è un processo con un utilizzo maggiore di risorse, usare un'impostazione client avanzata aggiuntiva denominata **RemoveExternalContentMarkingInAllSlides**:

- Chiave: **RemoveExternalContentMarkingInAllSlides**

- Valore: **True**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>Disabilitare le autorizzazioni personalizzate in Esplora file

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Per impostazione predefinita, gli utenti visualizzano un'opzione denominata **Proteggi con autorizzazioni personalizzate** quando fanno clic con il pulsante destro del mouse in Esplora file e scelgono **classifica e proteggi**. Questa opzione consente di impostare impostazioni di protezione personalizzate che possono sostituire le impostazioni di protezione che potrebbero essere state incluse con una configurazione di etichetta. Gli utenti possono visualizzare anche un'opzione per rimuovere la protezione. Quando si configura questa impostazione, gli utenti non visualizzano queste opzioni.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableCustomPermissions**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si configura l'impostazione client avanzata per [disabilitare le autorizzazioni personalizzate in Esplora file](#disable-custom-permissions-in-file-explorer), per impostazione predefinita gli utenti non sono in grado di visualizzare o modificare le autorizzazioni personalizzate già impostate in un documento protetto.

Tuttavia, esiste un'altra impostazione client avanzata che è possibile specificare in modo che in questo scenario gli utenti possano visualizzare e modificare le autorizzazioni personalizzate per un documento protetto quando usano Esplora file e fare clic con il pulsante destro del mouse sul file.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableCustomPermissionsForCustomProtectedFiles**

- Valore: **True**

Esempio di comando di PowerShell:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)

Questa configurazione USA [le impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Questa impostazione è destinata al momento in cui gli utenti alleghino i documenti con etichetta a un messaggio di posta elettronica e non etichettano il messaggio. In questo scenario viene selezionata automaticamente un'etichetta, in base alle etichette di classificazione applicate agli allegati. Viene selezionata l'etichetta di classificazione più alta.

L'allegato deve essere un file fisico e non un collegamento a un file, ad esempio in SharePoint o OneDrive for Business.

È possibile configurare questa impostazione su **consigliato**, in modo che agli utenti venga richiesto di applicare l'etichetta selezionata al messaggio di posta elettronica con una descrizione comando personalizzabile. Gli utenti possono accettare il suggerimento o ignorarlo. In alternativa, è possibile configurare questa impostazione su **automatica**, in cui l'etichetta selezionata viene applicata automaticamente, ma gli utenti possono rimuovere l'etichetta o selezionare un'etichetta diversa prima di inviare il messaggio di posta elettronica.

Nota: quando l'allegato con l'etichetta di classificazione più alta è configurato per la protezione con l'impostazione delle autorizzazioni definite dall'utente:

- Quando le autorizzazioni definite dall'utente dell'etichetta includono Outlook (non inviare), tale etichetta è selezionata e non viene applicata la protezione in diretta al messaggio di posta elettronica.
- Quando le autorizzazioni definite dall'utente dell'etichetta sono destinate solo a Word, Excel, PowerPoint ed Esplora file, tale etichetta non viene applicata al messaggio di posta elettronica e nessuna delle due è la protezione.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave 1: **AttachmentAction**

- Valore chiave 1: **consigliato** o **automatico**

- Chiave 2: **AttachmentActionTip**

- Valore chiave 2: "\<descrizione comando personalizzata >"

La descrizione comando personalizzata supporta solo un solo linguaggio.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>Aggiungere "Segnala un problema" per gli utenti

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si specifica la seguente impostazione client avanzata, gli utenti visualizzano l'opzione **Segnala un problema**, che può essere selezionata dalla finestra di dialogo **Guida e commenti** del client. Specificare una stringa HTTP per il collegamento. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **ReportAnIssueLink**

- Valore: **\<stringa HTTP>**

Valore di esempio per un sito Web: `https://support.contoso.com`

Valore di esempio per un indirizzo di posta elettronica: `mailto:helpdesk@contoso.com`

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica

Questa configurazione USA [le impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si creano e configurano le impostazioni client avanzate seguenti, gli utenti visualizzano messaggi popup di Outlook che possono avvertirli prima dell'invio di un messaggio di posta elettronica, chiedere di giustificare il motivo dell'invio o impedire l'invio di un messaggio di posta elettronica per uno degli scenari seguenti:

- **Il messaggio di posta elettronica o un suo allegato hanno un'etichetta specifica**:
    - L'allegato può essere qualsiasi tipo di file

- **Il messaggio di posta elettronica o l'allegato non hanno un'etichetta**:
    - L'allegato può essere un documento di Office o un documento PDF

Quando vengono soddisfatte queste condizioni, l'utente visualizza un messaggio popup con una delle azioni seguenti:

- **Avviso**: l'utente può confermare e inviare o annullare.

- **Giustifica**: all'utente viene richiesta la giustificazione (opzioni predefinite o formato libero).  L'utente può quindi inviare o annullare il messaggio di posta elettronica. Il testo della giustificazione è scritto nell'intestazione X- del messaggio di posta elettronica in modo da poter essere letto dagli altri sistemi. Ad esempio, servizi di prevenzione della perdita di dati.

- **Block**: l'utente non è in grado di inviare il messaggio di posta elettronica mentre la condizione rimane. Il messaggio include il motivo del blocco del messaggio di posta elettronica in modo che l'utente possa risolvere il problema, ad esempio rimuovendo destinatari specifici o assegnando un'etichetta al messaggio di posta elettronica. 

Quando i messaggi popup sono per un'etichetta specifica, è possibile configurare le eccezioni per i destinatari in base al nome di dominio.

> [!TIP]
> Per un esempio di procedura dettagliata su come configurare queste impostazioni, vedere il video [Azure Information Protection configurazione popup di Outlook](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/) .

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per etichette specifiche:

Per i criteri selezionati, creare una o più delle seguenti impostazioni avanzate con le chiavi seguenti. Per i valori, specificare una o più etichette in base ai relativi GUID, separate da una virgola.

Valore di esempio per più GUID etichetta come stringa con valori delimitati da virgole: `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- Messaggi di avviso:
    
    - Chiave: **OutlookWarnUntrustedCollaborationLabel**
    
    - Valore: \<**GUID dell'etichetta,** delimitati da virgole>

- Messaggi di giustificazione:
    
    - Chiave: **OutlookJustifyUntrustedCollaborationLabel**
    
    - Valore: \<**GUID dell'etichetta,** delimitati da virgole>

- Messaggi di blocco:
    
    - Chiave: **OutlookBlockUntrustedCollaborationLabel**
    
    - Valore: \<**GUID dell'etichetta,** delimitati da virgole>


Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>Per esentare i nomi di dominio per i messaggi popup configurati per etichette specifiche

Per le etichette specificate con questi messaggi popup, è possibile esentare i nomi di dominio specifici in modo che gli utenti non visualizzino i messaggi per i destinatari che hanno il nome di dominio incluso nell'indirizzo di posta elettronica. In questo caso, i messaggi di posta elettronica vengono inviati senza interruzioni. Per specificare più domini, aggiungerli come stringa singola, delimitata da virgole.

Una configurazione tipica consiste nel rendere visualizzabili i messaggi popup solo dai destinatari che sono esterni all'organizzazione o che non sono partner autorizzati dell'organizzazione. In questo caso, specificare tutti i domini di posta elettronica usati dall'organizzazione e dai partner.

Per gli stessi criteri di etichetta, creare le seguenti impostazioni client avanzate e, per il valore, specificare uno o più domini, ciascuno separato da una virgola.

Valore di esempio per più domini sotto forma di stringa delimitata da virgole: `contoso.com,fabrikam.com,litware.com`

- Messaggi di avviso:
    
    - Chiave: **OutlookWarnTrustedDomains**
    
    - Valore: **\<** nomi di dominio, delimitati da virgole **>**

- Messaggi di giustificazione:
    
    - Chiave: **OutlookJustifyTrustedDomains**
    
    - Valore: **\<** nomi di dominio, delimitati da virgole **>**

- Messaggi di blocco:
    
    - Chiave: **OutlookBlockTrustedDomains**
    
    - Valore: **\<** nomi di dominio, delimitati da virgole **>**

Ad esempio, è stata specificata l'impostazione **OutlookBlockUntrustedCollaborationLabel** Advanced client per l'etichetta **Confidential \ All Employees** . È ora possibile specificare l'impostazione client avanzata aggiuntiva di **OutlookJustifyTrustedDomains** e **contoso.com**. Di conseguenza, un utente può inviare un messaggio di posta elettronica a john@sales.contoso.com quando viene etichettato come **riservato \ tutti i dipendenti** , ma l'invio di un messaggio di posta elettronica con la stessa etichetta a un account Gmail verrà bloccato.

Comandi di PowerShell di esempio, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per i messaggi di posta elettronica o gli allegati senza etichetta:

Per gli stessi criteri di etichetta, creare l'impostazione client avanzata seguente con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **avviso**

- Messaggi di giustificazione:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **giustifica**

- Messaggi di blocco:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **blocco**

- Disattivare questi messaggi:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **disattivato**


Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Per definire estensioni di file specifiche per i messaggi popup di avviso, giustificazione o blocco per gli allegati di posta elettronica che non hanno un'etichetta

Per impostazione predefinita, i messaggi popup avvisa, giustifica o blocca si applicano a tutti i documenti di Office e PDF. È possibile affinare questo elenco specificando quali estensioni di file devono visualizzare i messaggi di avviso, di giustificazione o di blocco con un'impostazione avanzata aggiuntiva e un elenco delimitato da virgole di estensioni di file.

Valore di esempio per più estensioni di file da definire come stringa delimitata da virgole: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

In questo esempio un documento PDF senza etichetta non comporterà l'avviso, la giustificazione o il blocco dei messaggi popup.

Per gli stessi criteri di etichetta, immettere le stringhe seguenti: 


- Chiave: **OutlookOverrideUnlabeledCollaborationExtensions**

- Valore: **\<** estensioni di file per visualizzare i messaggi, delimitati da virgole **>**


Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>Per specificare un'azione diversa per i messaggi di posta elettronica senza allegati

Per impostazione predefinita, il valore specificato per OutlookUnlabeledCollaborationAction per avvisare, giustificare o bloccare i messaggi popup si applica ai messaggi di posta elettronica o agli allegati che non hanno un'etichetta. È possibile perfezionare questa configurazione specificando un'altra impostazione avanzata per i messaggi di posta elettronica che non dispongono di allegati.

Creare l'impostazione client avanzata seguente con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **avviso**

- Messaggi di giustificazione:
    
    - Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **giustifica**

- Messaggi di blocco:
    
    - Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **blocco**

- Disattivare questi messaggi:
    
    - Chiave: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **disattivato**

Se non si specifica questa impostazione client, il valore specificato per OutlookUnlabeledCollaborationAction viene usato per i messaggi di posta elettronica senza etichetta senza allegati, nonché per i messaggi di posta elettronica senza etichetta con allegati.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Disabilitare l'invio di dati di controllo a Azure Information Protection Analytics

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Il client per l'assegnazione di etichette unificata di Azure Information Protection supporta il reporting centrale e, per impostazione predefinita, invia i dati di controllo a [Azure Information Protection Analytics](../reports-aip.md). Per ulteriori informazioni sulle informazioni inviate e archiviate, vedere la sezione [informazioni raccolte e inviate a Microsoft](../reports-aip.md#information-collected-and-sent-to-microsoft) dalla documentazione centrale per la creazione di report.

Per modificare questo comportamento in modo che queste informazioni non vengano inviate dal client Unified Labeling, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableAudit**

- Valore: **False**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}


## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Disabilitare l'invio di informazioni riservate individuate nei documenti a Azure Information Protection Analytics

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si usa il client di assegnazione di etichette unificato Azure Information Protection nelle app di Office, Cerca informazioni riservate nei documenti quando vengono salvate per la prima volta. Se si specifica l'impostazione avanzata [EnableAudit](#disable-sending-audit-data-to-azure-information-protection-analytics) non è impostato su **false**, vengono inviati a [Azure Information Protection Analytics](../reports-aip.md)tutti i tipi di informazioni sensibili predefiniti e personalizzati trovati.

Per modificare questo comportamento in modo che i tipi di informazioni riservate individuate dal client Unified Labeling non vengano inviati, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **RunAuditInformationTypesDiscovery**

- Valore: **False**

Se si imposta questa impostazione client avanzata, le informazioni di controllo possono comunque essere inviate dal client, ma le informazioni sono limitate alla segnalazione quando un utente ha eseguito l'accesso al contenuto con etichetta.

Ad esempio:

- Con questa impostazione è possibile vedere che un utente ha eseguito l'accesso a Financial. docx con etichetta **Confidential \ Sales**.

- Senza questa impostazione, è possibile notare che Financial. docx contiene 6 numeri di carta di credito.
    
    - Se si abilita anche [Corrispondenze di contenuto per un'analisi più approfondita](../reports-aip.md#content-matches-for-deeper-analysis), si potranno vedere anche i numeri di carta di credito stessi.

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypesDiscovery="False"}

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>Invia corrispondenze del tipo di informazioni a Azure Information Protection Analytics
 
Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Per impostazione predefinita, il client di etichettatura unificata non invia corrispondenze di contenuto per i tipi di informazioni riservate a [Azure Information Protection Analytics](../reports-aip.md). Per ulteriori informazioni su queste informazioni aggiuntive che possono essere inviate, vedere la sezione relativa alle [corrispondenze per un'analisi più approfondita](../reports-aip.md#content-matches-for-deeper-analysis) dalla documentazione centrale per la creazione di report.

Per inviare le corrispondenze di contenuto quando si inviano tipi di informazioni riservate, creare l'impostazione client avanzata seguente in un criterio etichetta: 

- Chiave: **LogMatchedContent**

- Valore: **True**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}

## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>Limitare il numero di thread usati dallo scanner

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dei criteri che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Per impostazione predefinita, lo scanner usa tutte le risorse del processore disponibili nel computer che esegue il servizio scanner. Se è necessario limitare l'utilizzo della CPU durante l'analisi di questo servizio, creare l'impostazione avanzata seguente in un criterio di etichetta. 

Come valore specificare il numero di thread simultanei che lo scanner può eseguire in parallelo. Lo scanner usa un thread separato per ogni file analizzato, quindi questa configurazione della limitazione definisce anche il numero di file che possono essere analizzati in parallelo. 

Quando si configura il valore per il test per la prima volta, è consigliabile specificare 2 per ogni core e quindi monitorare i risultati. Se ad esempio si esegue lo scanner in un computer con 4 core, impostare prima il valore su 8. Se necessario, aumentare o diminuire questo numero, in base alle prestazioni risultanti richieste per il computer dello scanner e la velocità di analisi. 

- Chiave: **ScannerConcurrencyLevel**

- Valore: **\<numero massimo di utenti simultanei>**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}


## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) delle etichette che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Questa configurazione non è compatibile con i file PDF protetti con estensione Ppdf. Questi file non possono essere aperti dal client usando Esplora file o PowerShell.

Per i documenti di Office etichettati con le isole sicure, è possibile rietichettare questi documenti con un'etichetta di riservatezza usando un mapping definito dall'utente. È anche possibile usare questo metodo per riutilizzare le etichette da altre soluzioni quando sono applicate a documenti di Office. 

In seguito a questa opzione di configurazione, la nuova etichetta di riservatezza viene applicata dal client Azure Information Protection Unified Labeling come indicato di seguito:

- Per i documenti di Office: quando il documento viene aperto nell'app desktop, la nuova etichetta di riservatezza viene visualizzata come impostata e viene applicata quando il documento viene salvato.

- Per PowerShell: [set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) possono applicare la nuova etichetta di riservatezza.

- Per Esplora file: nella finestra di dialogo Azure Information Protection, la nuova etichetta di riservatezza viene visualizzata ma non è impostata.

Per questa configurazione è necessario specificare un'impostazione avanzata denominata **labelByCustomProperties** per ogni etichetta di riservatezza di cui si vuole eseguire il mapping all'etichetta precedente. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

Specificare un nome di regola di migrazione a propria scelta. Usare un nome descrittivo che consenta di identificare la modalità di mapping di una o più etichette della soluzione di assegnazione di etichette precedente all'etichetta di riservatezza.

Si noti che questa impostazione non comporta la rimozione dell'etichetta originale dal documento o di tutti i contrassegni visivi nel documento che l'etichetta originale potrebbe aver applicato. Per rimuovere intestazioni e piè di pagina, vedere la sezione precedente [rimuovere intestazioni e piè di pagina dalle altre soluzioni per l'assegnazione di etichette](#remove-headers-and-footers-from-other-labeling-solutions).

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta

Requisito: i documenti con un'etichetta di isole sicure "riservato" devono essere rietichettati come "riservati" da Azure Information Protection.

In questo esempio:

- L'etichetta di Secure Islands è **Riservato** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

Impostazione avanzata:

- Chiave: **labelByCustomProperties**

- Valore: l' **etichetta Secure Islands è riservata, classificazione, riservata**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "Confidential":

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Esempio 2: Mapping uno-a-uno per un altro nome di etichetta

Requisito: i documenti contrassegnati come "sensibili" dalle isole sicure devono essere rietichettati come "riservatezza elevata" da Azure Information Protection.

In questo esempio:

- L'etichetta di Secure Islands è **Sensibile** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

Impostazione avanzata:

- Chiave: **labelByCustomProperties**

- Valore: l' **etichetta Secure Islands è sensibile, classificazione, sensibile**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "highly Confidential":

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>Esempio 3: Mapping molti-a-uno di nomi di etichetta

Requisito: sono presenti due etichette di isole sicure che includono la parola "Internal" e si vuole che i documenti che contengono una di queste etichette di isole sicure vengano rietichettati come "General" dal client Azure Information Protection Unified labeling.

In questo esempio:

- Le etichette di Secure Islands includono la parola **Interno** e sono archiviate nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

- Chiave: **labelByCustomProperties**

- Valore: l' **etichetta Secure Islands contiene Internal, Classification,.\*Internal.\***

Esempio di comando di PowerShell, in cui l'etichetta è denominata "generale":

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Esempio 4: più regole per la stessa etichetta

Quando sono necessarie più regole per la stessa etichetta, definire più valori stringa per la stessa chiave. 

In questo esempio, le etichette delle isole sicure denominate "Confidential" e "Secret" vengono archiviate nella proprietà personalizzata denominata **Classification**e si vuole che il client Azure Information Protection Unified Labeling applichi l'etichetta di riservatezza denominata "Confidential":

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>Estendi le regole di migrazione delle etichette ai messaggi di posta elettronica

È possibile usare le impostazioni avanzate di labelByCustomProperties con i messaggi di posta elettronica di Outlook oltre ai documenti di Office specificando un'impostazione aggiuntiva avanzata dei criteri di etichetta. Tuttavia, questa impostazione ha un impatto negativo noto sulle prestazioni di Outlook. Configurare quindi questa impostazione aggiuntiva solo quando si dispone di un requisito aziendale sicuro e ricordarsi di impostarla su un valore di stringa null dopo aver completato la migrazione dalla altra soluzione per l'assegnazione di etichette.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableLabelByMailHeader**

- Valore: **True**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>Estendere le regole di migrazione delle etichette alle proprietà di SharePoint

È possibile usare le impostazioni avanzate di labelByCustomProperties con proprietà di SharePoint che è possibile esporre come colonne agli utenti.

Questa impostazione è supportata quando si usano Word, Excel e PowerPoint.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per i criteri di etichetta selezionati:

- Chiave: **EnableLabelBySharePointProperties**

- Valore: **True**

Esempio di comando di PowerShell, in cui il criterio etichetta è denominato "globale":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Applicare una proprietà personalizzata quando viene applicata un'etichetta

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) delle etichette che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Potrebbero essere presenti alcuni scenari in cui si desidera applicare una o più proprietà personalizzate a un documento o a un messaggio di posta elettronica oltre ai metadati applicati da un'etichetta di riservatezza.

Ad esempio:

- È in corso la [migrazione da un'altra soluzione di assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions), ad esempio le isole sicure. Per l'interoperabilità durante la migrazione, si desidera che le etichette di riservatezza applichino anche una proprietà personalizzata utilizzata dall'altra soluzione di assegnazione di etichette.

- Per il sistema di gestione dei contenuti (ad esempio SharePoint o una soluzione di gestione dei documenti di un altro fornitore) si vuole usare un nome di proprietà personalizzato coerente con valori diversi per le etichette e con nomi descrittivi anziché il GUID dell'etichetta.

Per i documenti di Office e i messaggi di posta elettronica di Outlook che gli utenti etichettano usando il Azure Information Protection client Unified Labeling, è possibile aggiungere una o più proprietà personalizzate definite dall'utente. È anche possibile usare questo metodo per il client di etichettatura unificata per visualizzare una proprietà personalizzata come etichetta di altre soluzioni per il contenuto che non è ancora etichettato dal client di etichettatura unificata.

In seguito a questa opzione di configurazione, tutte le proprietà personalizzate aggiuntive vengono applicate dal client Azure Information Protection Unified Labeling come indicato di seguito:

- Per i documenti di Office: quando il documento viene etichettato nell'app desktop, le proprietà personalizzate aggiuntive vengono applicate quando il documento viene salvato.

- Per i messaggi di posta elettronica di Outlook: quando il messaggio di posta elettronica è contrassegnato in Outlook, le proprietà aggiuntive vengono applicate all'intestazione x quando viene inviato il messaggio di posta elettronica.

- Per PowerShell: [set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) applica le proprietà personalizzate aggiuntive quando il documento viene etichettato e salvato. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) Visualizza le proprietà personalizzate come etichetta mappata se non viene applicata un'etichetta di riservatezza.

- Per Esplora file: quando l'utente fa clic con il pulsante destro del mouse sul file e applica l'etichetta, vengono applicate le proprietà personalizzate.

Per questa configurazione è necessario specificare un'impostazione avanzata denominata **customPropertiesByLabel** per ogni etichetta di riservatezza a cui si desidera applicare le proprietà personalizzate aggiuntive. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Esempio 1: aggiungere un'unica proprietà personalizzata per un'etichetta

Requisito: i documenti etichettati come "riservati" dal client Azure Information Protection Unified Labeling devono avere la proprietà personalizzata aggiuntiva denominata "classificazione" con il valore "Secret".

In questo esempio:

- L'etichetta di riservatezza è denominata **Confidential** e crea una proprietà personalizzata denominata **classificazione** con il valore **Secret**.

Impostazione avanzata:

- Chiave: **customPropertiesByLabel**

- Valore: **classificazione, segreto**

Esempio di comando di PowerShell, in cui l'etichetta è denominata "Confidential":

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Esempio 2: aggiungere più proprietà personalizzate per un'etichetta

Per aggiungere più di una proprietà personalizzata per la stessa etichetta, è necessario definire più valori stringa per la stessa chiave.

Esempio di comando di PowerShell, in cui l'etichetta è denominata "generale" e si vuole aggiungere una proprietà personalizzata denominata **classificazione** con il valore **generale** e una seconda proprietà personalizzata denominata **Sensitivity** con il valore **Internal**:

    Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurare un'etichetta per applicare la protezione S/MIME in Outlook

Questa configurazione USA [le impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dell'etichetta che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Usare queste impostazioni solo quando si dispone di una [distribuzione S/MIME](https://docs.microsoft.com/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption) funzionante e si vuole che un'etichetta applichi automaticamente questo metodo di protezione per i messaggi di posta elettronica anziché Rights Management la protezione da Azure Information Protection. La protezione risultante è identica a quella applicata quando un utente seleziona manualmente le opzioni di S/MIME da Outlook.

Per configurare un'impostazione avanzata per una firma digitale S/MIME, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **SMimeSign**

- Valore: **True**

Per configurare un'impostazione avanzata per la crittografia S/MIME, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **SMimeEncrypt**

- Valore: **True**

Se l'etichetta specificata è configurata per la crittografia, per il client Azure Information Protection Unified Labeling, S/MIME Protection sostituisce la protezione Rights Management solo in Outlook. La versione di disponibilità generale del client Unified Labeling continua a usare le impostazioni di crittografia specificate per l'etichetta nell'interfaccia di amministrazione. Per le app di Office con etichette predefinite, non applicano la protezione S/MIME, bensì applicano la protezione non inoltrare.

Se si vuole che l'etichetta sia visibile solo in Outlook, configurare l'etichetta in modo da applicare la crittografia **solo ai messaggi di posta elettronica in Outlook**.

Comandi di PowerShell di esempio, in cui l'etichetta è denominata "solo destinatari":

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Specificare un'etichetta secondaria predefinita per un'etichetta padre

Questa configurazione usa un' [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) delle etichette che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Quando si aggiunge un'etichetta secondaria a un'etichetta, gli utenti non possono più applicare l'etichetta padre a un documento o a un messaggio di posta elettronica. Per impostazione predefinita, gli utenti selezionano l'etichetta padre per visualizzare le etichette secondarie che possono essere applicate, quindi selezionare una delle etichette secondarie. Se si configura questa impostazione avanzata, quando gli utenti selezionano l'etichetta padre, viene automaticamente selezionata e applicata un'etichetta secondaria: 

- Chiave: **DefaultSubLabelId**

- Valore: \<GUID dell'etichetta secondaria >

Esempio di comando di PowerShell, in cui l'etichetta padre è denominata "Confidential" e l'etichetta secondaria "All Employees" ha un GUID di 8faca7b8-8d20-48A3-8ea2-0f96310a848e:

    Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}


## <a name="specify-a-color-for-the-label"></a>Specificare un colore per l'etichetta

Questa configurazione USA [le impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) dell'etichetta che è necessario configurare usando Office 365 Centro sicurezza e conformità PowerShell.

Usare questa impostazione avanzata per impostare un colore per un'etichetta. Per specificare il colore, immettere un codice di tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, #40e0d0 è il valore esadecimale RGB per il turchese.

Se è necessario un riferimento per questi codici, è possibile trovare una tabella utile dalla pagina di [> dei colori\<](https://developer.mozilla.org/docs/Web/CSS/color_value) da MSDN Web docs. Questi codici sono disponibili anche in molte applicazioni che consentono di modificare le immagini. Ad esempio quando in Microsoft Paint si sceglie un colore personalizzato in una tavolozza vengono visualizzati automaticamente i valori RGB corrispondenti ed è possibile copiarli.

Per configurare l'impostazione avanzata per il colore di un'etichetta, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **colore**

- Valore: \<valore esadecimale RGB >

Esempio di comando di PowerShell, in cui l'etichetta è denominata "public":

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, gli utenti in genere non devono eseguire l'accesso come utente diverso quando usano il client di Azure Information Protection Unified labeling. Per un amministratore, tuttavia, può essere necessario accedere con le credenziali di un altro utente durante una fase di testing. 

È possibile verificare l'account a cui si è attualmente connessi usando la finestra di dialogo **Microsoft Azure Information Protection** : aprire un'applicazione di Office e nella scheda **Home** , selezionare il pulsante **sensibilità** , quindi selezionare **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'utilizzo dell'account errato include il mancato download delle etichette o la mancata visualizzazione delle etichette o del comportamento previsto.

Per accedere come utente diverso:

1. Passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzata una richiesta nell'applicazione di Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e selezionare **Accedi** dalla sezione **stato client** aggiornato.

Inoltre:

- Se il client Azure Information Protection Unified Labeling è ancora connesso con l'account precedente dopo aver completato questi passaggi, eliminare tutti i cookie da Internet Explorer, quindi ripetere i passaggi 1 e 2.

- Se si usa la funzione Single Sign-On, è necessario uscire da Windows e accedere con un account utente diverso dopo aver eliminato il file del token. Il Azure Information Protection client per l'assegnazione di etichette unificata viene quindi autenticato automaticamente utilizzando l'account utente attualmente connesso.

- Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. Per testare Azure Information Protection con più tenant, usare computer diversi.

- È possibile usare l'opzione **Reimposta impostazioni** da **Guida e commenti e suggerimenti** per disconnettersi ed eliminare le etichette e le impostazioni dei criteri attualmente scaricate dall'Centro sicurezza e conformità di Office 365, dal centro sicurezza Microsoft 365 o dal centro di conformità Microsoft 365.


## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

> [!IMPORTANT]
> I computer disconnessi sono supportati per gli scenari di assegnazione di etichette seguenti: Esplora file, PowerShell, le app di Office e lo scanner.

Per impostazione predefinita, il client di Azure Information Protection Unified Labeling tenta automaticamente di connettersi a Internet per scaricare le etichette e le impostazioni dei criteri di etichetta dal centro di gestione delle etichette: il Centro sicurezza e conformità di Office 365, il Microsoft 365 Centro sicurezza o il centro di conformità Microsoft 365. Se si dispone di computer che non possono connettersi a Internet per un certo periodo di tempo, è possibile esportare e copiare i file che gestiscono manualmente i criteri per il client di etichettatura unificata.

Istruzioni:

1. Scegliere o creare un account utente in Azure AD che si utilizzerà per scaricare le etichette e le impostazioni dei criteri che si desidera utilizzare nel computer disconnesso.

2. Come impostazione dei criteri di etichetta aggiuntiva per questo account, [disabilitare l'invio dei dati di controllo a Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) usando l'impostazione avanzata **EnableAudit** .
    
    Si consiglia di eseguire questo passaggio perché se il computer disconnesso presenta una connettività Internet periodica, invierà le informazioni di registrazione a Azure Information Protection Analytics che include il nome utente del passaggio 1. Tale account utente potrebbe essere diverso dall'account locale in uso nel computer disconnesso.

3. Da un computer con connettività Internet con il client Unified Labeling installato e connesso con l'account utente del passaggio 1, scaricare le etichette e le impostazioni dei criteri.

4. Da questo computer esportare i file di log.
    
    Ad esempio, eseguire il cmdlet [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs) oppure usare l'opzione **Esporta log** dalla finestra di dialogo [Guida e commenti](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client) del client. 
    
    I file di log vengono esportati come un singolo file compresso.

5.  Aprire il file compresso, quindi copiare i file con estensione XML dalla cartella MSIP.

6. Incollare questi file nella cartella **%LocalAppData%\Microsoft\MSIP** del computer disconnesso.

7. Se l'account utente scelto è uno che in genere si connette a Internet, abilitare di nuovo l'invio dei dati di controllo, impostando il valore di **EnableAudit** su **true**.

8. Affinché il computer disconnesso protegga i file, riproteggi i file, Rimuovi la protezione dai file o controlla i file protetti: nel computer disconnesso, eseguire il cmdlet [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con il parametro *DelegatedUser* e specificare l'account utente del passaggio 1 per impostare il contesto utente. Ad esempio:
    
        Set-AIPAuthentication -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser offlineuser@contoso.com

Tenere presente che se un utente del computer seleziona l'opzione **Reimposta impostazioni** da [Guida e commenti e suggerimenti](clientv2-admin-guide.md#help-and-feedback-section), questa azione Elimina i file di criteri e rende il client inutilizzabile fino a quando non si sostituiscono manualmente i file o il client si connette a Internet e Scarica i file.

Se il computer disconnesso esegue lo scanner Azure Information Protection, è necessario eseguire passaggi di configurazione aggiuntivi. Per altre informazioni, vedere [restrizione: il server dello scanner non può avere connettività Internet](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity) dalle istruzioni per la distribuzione dello scanner.

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

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato personalizzato il client di etichettatura Azure Information Protection Unified, vedere le risorse seguenti per altre informazioni che potrebbero essere necessarie per supportare questo client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)
