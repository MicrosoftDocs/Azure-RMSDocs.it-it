---
title: Configurazioni personalizzate - Azure Information Protection unified client l'assegnazione di etichette
description: Informazioni sulla personalizzazione del client di assegnazione di etichette unificato di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 560d954119c40ad3fd9dd99b4d9f1ef18fb88515
ms.sourcegitcommit: 9c9ee62632bbb5d7151131da8b720b7c9bf2a8f1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67571854"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client di assegnazione di etichette unificata di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni seguenti per le configurazioni avanzate che potrebbe essere necessario per scenari specifici o un sottoinsieme di utenti per gestire il client di assegnazione di etichette unificato di Azure Information Protection.

Queste impostazioni richiedono la modifica del Registro di sistema o la specifica di impostazioni avanzate. L'utilizzo di impostazioni avanzate [Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps).

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Come configurare le impostazioni avanzate per il client usando Office 365 Security & Compliance Center PowerShell

Quando si usa Office 365 Security & Compliance Center PowerShell, è possibile configurare le impostazioni avanzate che supportano le personalizzazioni per i criteri etichetta ed etichette. Ad esempio:

- L'impostazione per visualizzare la barra di Information Protection nelle app di Office è un ***etichettare i criteri di impostazione avanzato***.
- L'impostazione per specificare un colore dell'etichetta è un ***etichetta impostazione avanzata***.

In entrambi i casi, dopo aver [connettersi a Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps), specificare il *AdvancedSettings* parametro con l'identità (nome o GUID) del criterio o etichetta e specificare in coppie chiave/valore una [tabella hash](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables). Usare la sintassi seguente:

Per un'impostazione di criteri di etichetta, singolo valore di stringa:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

Per impostazioni dei criteri etichetta, più valori di stringa per la stessa chiave:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Per un'impostazione di etichetta, singolo valore di stringa:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

Per le impostazioni dell'etichetta, più valori di stringa per la stessa chiave:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Per rimuovere un'impostazione avanzata, usare la stessa sintassi ma specifica un valore di stringa null.


#### <a name="examples-for-setting-advanced-settings"></a>Esempi relativi all'impostazione le impostazioni avanzate

Esempio 1: Impostare un criterio di etichetta le impostazioni avanzato di un valore stringa singolo:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

Esempio 2: Impostare un'etichetta con le impostazioni avanzata di un valore stringa singolo:

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

Esempio 3: Impostare un'etichetta con le impostazioni avanzata di più valori stringa:

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

Esempio 4: Rimuovere un criterio di etichetta impostazione avanzato, specificando un valore di stringa null:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>Specifica dell'identità per il criterio di etichetta o etichetta

Specifica il nome del criterio di etichetta per il comando di PowerShell *identità* parametro è semplice perché viene visualizzato un solo nome di criterio nell'interfaccia di amministrazione in cui è gestire i criteri etichetta. Tuttavia, per le etichette, viene visualizzato sia un **Name** e **nome visualizzato** in admin Center. In alcuni casi, il valore per entrambi sarà lo stesso, ma possono essere diverse:

- **Nome** è il nome originale dell'etichetta ed è univoco tra tutte le etichette. Se si modifica il nome dell'etichetta dopo averlo creato, questo valore rimane invariato.

- **Nome visualizzato** è il nome dell'etichetta sulla quale gli utenti vedono e non deve necessariamente essere univoco in tutte le etichette. Ad esempio, gli utenti visualizzeranno uno **tutti i dipendenti** sublabel per il **Confidential** etichetta e un altro **tutti i dipendenti** sublabel per il **riservatezza elevata**  etichetta. Queste etichette secondarie sia visualizzato lo stesso nome ma non sono la stessa etichetta e abbiano impostazioni diverse.

Per configurare l'etichetta impostazioni avanzata, usare il **nome** valore. Ad esempio, per identificare l'etichetta nell'immagine seguente, si specificherà `-Identity "All Company"`:

![Usare 'Name' anziché 'Nome visualizzato' per identificare un'etichetta di riservatezza](../media/labelname_scc.png)

Se si preferisce per specificare l'etichetta GUID, questo valore non viene visualizzato nell'interfaccia di amministrazione in cui è gestire le etichette. Tuttavia, è possibile usare il comando seguente di Office 365 Security & Compliance Center PowerShell per trovare questo valore:

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Ordine di precedenza - modalità in conflitto vengono risolte le impostazioni

Scegliendo tra le interfacce di amministrazione in cui è gestire le etichette di riservatezza, è possibile configurare le impostazioni dei criteri etichetta seguente:

- **Applicare questa etichetta per impostazione predefinita a documenti e messaggi di posta elettronica**

- **Gli utenti devono fornire una giustificazione per rimuovere un'etichetta o etichetta di classificazione più bassa**

- **Richiedere agli utenti di applicare un'etichetta per il messaggio di posta elettronica o documento**

- **Fornire agli utenti un collegamento a una pagina della Guida personalizzata**

Quando più di un criterio di etichetta è configurato per un utente, ognuno con le impostazioni di criteri potenzialmente diversi, l'ultima impostazione dei criteri viene applicato in base all'ordine dei criteri del centro di amministrazione. Per altre informazioni, vedere [etichettare priorità dei criteri (ordine è rilevante)](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels#label-policy-priority-order-matters)

Etichetta impostazioni avanzata seguono la stessa logica per la precedenza: Quando un'etichetta è in più criteri di etichetta e quell'etichetta ha impostazioni avanzate, l'ultima impostazione avanzata viene applicato in base all'ordine dei criteri del centro di amministrazione.

Impostazioni avanzati dei criteri di etichetta vengono applicati in ordine inverso: Con un'eccezione, vengono applicate le impostazioni avanzate dal primo criterio, in base all'ordine dei criteri del centro di amministrazione. L'eccezione è l'impostazione avanzata *OutlookDefaultLabel*, che imposta un'etichetta predefinita diversa per Outlook. Per questo criterio di etichetta impostazione avanzata, solo l'ultima impostazione viene applicata in base all'ordine dei criteri del centro di amministrazione.

#### <a name="available-advanced-settings-for-label-policies"></a>Le impostazioni avanzate per i criteri etichetta disponibile

|Impostazione|Scenario e istruzioni|
|----------------|---------------|
|AttachmentAction|[Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|EnableCustomPermissions|[Disabilitare le autorizzazioni personalizzate in Esplora File](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|HideBarByDefault|[Visualizza la barra di Information Protection nelle app Office](##display-the-information-protection-bar-in-office-apps)|
|labelByCustomProperties|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LogMatchedContent|[Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti](#disable-sending-information-type-matches-for-a-subset-of-users)|
|OutlookBlockTrustedDomains|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Impostare un'etichetta predefinita diversa per Outlook](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Abilitare la classificazione consigliata in Outlook](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PostponeMandatoryBeforeSave|[Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Aggiungere "Segnala un problema" per gli utenti](#add-report-an-issue-for-users)|
|RunAuditInformationTypeDiscovery|[Disabilitare l'invio di informazioni sensibili rilevate nei documenti a analitica di Azure Information Protection](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|

Esempio di comando di PowerShell per controllare le impostazioni dei criteri etichetta attiva per un criterio di etichetta denominata "Global":

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>Impostazioni avanzate disponibili per le etichette

|Impostazione|Scenario e istruzioni|
|----------------|---------------|
|Colore|[Specificare un colore per l'etichetta](#specify-a-color-for-the-label)|
|customPropertyByLabel|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|DefaultSubLabelId|[Specificare un'etichetta secondaria predefinito per un'etichetta padre](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[Applicare una proprietà personalizzata quando viene applicata un'etichetta](#apply-a-custom-property-when-a-label-is-applied)|
|SMimeEncrypt|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|

Esempio di comando di PowerShell per controllare le impostazioni di etichetta in vigore per un'etichetta denominata "Public":

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>Visualizza la barra di Information Protection nelle app Office

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Per impostazione predefinita, gli utenti devono selezionare i **Mostra barra** opzione il **sensibilità** pulsante per visualizzare la barra di Information Protection nelle app di Office. Usare la **HideBarByDefault** chiave e il valore impostato su **False** per visualizzare automaticamente questa barra per gli utenti in modo che è possibile selezionare le etichette dalla barra o il pulsante. 

Per i criteri etichetta selezionata, specificare le stringhe seguenti:

- Chiave: **HideBarByDefault**

- Valore: **False**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per i criteri etichetta selezionata, specificare le stringhe seguenti:

- Chiave: **OutlookRecommendationEnabled**

- Valore: **True**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata come un'impostazione di criteri per l'opzione **applicare questa etichetta per impostazione predefinita a documenti e messaggi di posta elettronica**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per i criteri etichetta selezionata, specificare le stringhe seguenti:

- Chiave: **OutlookDefaultLabel**

- Valore: \< **etichetta GUID**> o **None**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}


## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si usa l'impostazione del criterio di etichetta **tutti i documenti e messaggi di posta elettronica devono avere un'etichetta**, agli utenti viene chiesto di selezionare un'etichetta quando salvano prima di tutto un documento di Office e quando inviano un messaggio di posta elettronica. Per i documenti, gli utenti possono selezionare **Non ora** per chiudere temporaneamente la richiesta di selezionare un'etichetta e tornare al documento. Non possono però chiudere il documento salvato senza etichettarlo. 

Quando si configura questa impostazione l'opzione **Non ora** viene rimossa. In questo modo, quando il documento viene salvato per la prima volta gli utenti sono obbligati a selezionare un'etichetta.

Per i criteri etichetta selezionata, specificare le stringhe seguenti:

- Chiave: **PostponeMandatoryBeforeSave**

- Valore: **False**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette

Questa configurazione usa criteri [impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Le impostazioni consentono di rimuovere o sostituire le intestazioni o i piè di pagina basati su testo nei documenti, quando questi contrassegni visivi sono stati applicati da un'altra soluzione di etichettatura. Ad esempio, il piè di pagina precedente contiene il nome di un'etichetta precedente ora migrato per etichette di riservatezza per usare un nuovo nome di etichetta e un proprio piè di pagina.

Quando il client di assegnazione di etichette unificato riceve questa configurazione nei suoi criteri, le precedenti intestazioni e piè di pagina vengono rimosse o sostituite quando il documento viene aperto nell'app di Office e qualsiasi etichetta di riservatezza viene applicata al documento.

Questa configurazione non è supportata per Outlook e tenere presente che quando viene usata con Word, Excel e PowerPoint, può influire negativamente sulle prestazioni di queste app per gli utenti. La configurazione consente di definire le impostazioni per ogni applicazione, ad esempio la ricerca di testo nelle intestazioni e nei piè di pagina di documenti di Word, ma non nei fogli di calcolo di Excel o nelle presentazioni di PowerPoint.

Poiché i criteri di ricerca influisce sulle prestazioni per gli utenti, è consigliabile limitare i tipi di applicazioni di Office (**W**ord, **elettronica**xcel, **P**PowerPoint) a quelle che dovrà essere eseguita la ricerca.

Per i criteri etichetta selezionata, specificare le stringhe seguenti:

- Chiave: **RemoveExternalContentMarkingInApp**

- Valore: \<**tipi di applicazioni di Office WXP**> 

Esempi:

- Per eseguire la ricerca solo in documenti di Word, specificare **W**.

- Per eseguire la ricerca in documenti di Word e presentazioni di PowerPoint, specificare **WP**.

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

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

Per lo stesso criterio di etichetta, specificare le stringhe seguenti:

- Chiave: **ExternalContentMarkingToRemove**

- Valore: \<**stringa da confrontare, definita come espressione regolare**> 

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>Intestazioni o piè di pagina su più righe

Se il testo di un'intestazione o un piè di pagina è su più righe, creare una chiave e un valore per ogni riga. Si supponga, ad esempio, di avere il piè di pagina seguente con due righe:

**The file is classified as Confidential**

**Label applied manually**

Per rimuovere il piè di pagina su più righe, si crea le seguenti due voci per lo stesso criterio di etichetta:

- Chiave: **ExternalContentMarkingToRemove**

- Valore chiave 1: **\*Confidential***

- Valore chiave 2: **\*Label applied*** 

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

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

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

Quando si dispone di più di una forma di PowerPoint da rimuovere, specificare tanti valori quanti si hanno le forme da rimuovere.

Per impostazione predefinita, il testo delle intestazioni e dei piè di pagina viene cercato solo negli schemi diapositiva. Per estendere la ricerca a tutte le diapositive, che è un processo con un utilizzo maggiore di risorse, usare un'impostazione client avanzata aggiuntiva denominata **RemoveExternalContentMarkingInAllSlides**:

- Chiave: **RemoveExternalContentMarkingInAllSlides**

- Valore: **True**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>Disabilitare le autorizzazioni personalizzate in Esplora File

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Per impostazione predefinita, gli utenti visualizzano un'opzione denominata **Proteggi con autorizzazioni personalizzate** quando pulsante destro del mouse in Esplora File e scegliere **classifica e Proteggi**. Questa opzione permetta di impostare le proprie impostazioni di protezione che è possono eseguire l'override di eventuali impostazioni di protezione che sia stata inclusa con una configurazione di etichetta. Gli utenti possono visualizzare anche un'opzione per rimuovere la protezione. Quando si configura questa impostazione, queste opzioni non vengono visualizzate agli utenti.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per il criterio di etichetta selezionata:

- Chiave: **EnableCustomPermissions**

- Valore: **False**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si configura l'impostazione client avanzata per [disabilitare le autorizzazioni personalizzate in Esplora File](#disable-custom-permissions-in-file-explorer), per impostazione predefinita, gli utenti non sono in grado di visualizzare o modificare le autorizzazioni personalizzate che sono già impostate in un documento protetto.

Tuttavia, vi è un'altra impostazione avanzata del client che è possibile specificare in modo che in questo scenario, gli utenti possono visualizzare e modificare le autorizzazioni personalizzate per un documento protetto, quando si usa Esplora File e fare doppio clic su file.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per il criterio di etichetta selezionata:

- Chiave: **EnableCustomPermissionsForCustomProtectedFiles**

- Valore: **True**

Comando di PowerShell di esempio:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)

Questa configurazione usa criteri [impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Questa impostazione è destinata quando gli utenti di collegare i documenti con etichettati a un messaggio di posta elettronica e di non assegnata un'etichetta di messaggio di posta elettronica. In questo scenario, un'etichetta viene selezionata automaticamente in base alle etichette di classificazione che vengono applicate agli allegati. L'etichetta di classificazione più alta è selezionata.

L'allegato deve essere un file fisico e non un collegamento a un file, ad esempio in SharePoint o OneDrive for Business.

È possibile configurare questa impostazione per **Recommended**, in modo che gli utenti vengono richiesto di applicare l'etichetta selezionata per il messaggio di posta elettronica, con una descrizione comando personalizzabile. Gli utenti possono accettare il suggerimento o ignorarlo. Oppure, è possibile configurare questa impostazione per **automatica**, in cui viene applicata automaticamente l'etichetta selezionata, ma gli utenti possono rimuovere l'etichetta o selezionare un'etichetta diversa prima di inviare il messaggio di posta elettronica.

Nota: Quando l'allegato con l'etichetta di classificazione più alta è configurato per la protezione con l'impostazione di autorizzazioni definite dall'utente:

- Quando l'etichetta definita dall'utente autorizzazioni includono Outlook (non inoltrare), che seleziona l'etichetta e protezione non inoltrare viene applicata al messaggio di posta elettronica. 
- Quando le autorizzazioni definite dall'utente dell'etichetta sono semplicemente per Word, Excel, PowerPoint e File Explorer, quell'etichetta non viene applicato al messaggio di posta elettronica e nessuno è la protezione.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per il criterio di etichetta selezionata:

- Chiave 1: **AttachmentAction**

- Valore chiave 1: **Consigliato** o **automatica**

- Chiave 2: **AttachmentActionTip**

- Valore della chiave 2: "\<personalizzata della descrizione comando >"


Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>Aggiungere "Segnala un problema" per gli utenti

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si specifica la seguente impostazione client avanzata, gli utenti visualizzano l'opzione **Segnala un problema**, che può essere selezionata dalla finestra di dialogo **Guida e commenti** del client. Specificare una stringa HTTP per il collegamento. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per il criterio di etichetta selezionata:

- Chiave: **ReportAnIssueLink**

- Valore: **\<stringa HTTP>**

Valore di esempio per un sito Web: `https://support.contoso.com`

Valore di esempio per un indirizzo di posta elettronica: `mailto:helpdesk@contoso.com`

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica

Questa configurazione usa criteri [impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si creano e configurano le impostazioni client avanzate seguenti, gli utenti visualizzano messaggi popup di Outlook che possono avvertirli prima dell'invio di un messaggio di posta elettronica, chiedere di giustificare il motivo dell'invio o impedire l'invio di un messaggio di posta elettronica per uno degli scenari seguenti:

- **Il messaggio di posta elettronica o un suo allegato hanno un'etichetta specifica**:
    - L'allegato può essere qualsiasi tipo di file

- **Il messaggio di posta elettronica o l'allegato non hanno un'etichetta**:
    - L'allegato può essere un documento di Office o un documento PDF

Quando vengono soddisfatte queste condizioni e indirizzo di posta elettronica del destinatario non è incluso in un elenco di nomi di dominio consentiti che è stato specificato, l'utente visualizza un messaggio popup con una delle azioni seguenti:

- **Avvisa**: l'utente può confermare e inviare oppure annullare.

- **Giustifica**: all'utente viene richiesta una giustificazione (opzioni predefinite o formato libero).  L'utente può quindi inviare o annullare il messaggio di posta elettronica. Il testo della giustificazione è scritto nell'intestazione X- del messaggio di posta elettronica in modo da poter essere letto dagli altri sistemi. Ad esempio, servizi di prevenzione della perdita di dati.

- **Blocca**: all'utente viene impedito di inviare il messaggio di posta elettronica finché la condizione persiste. Il messaggio include il motivo del blocco del messaggio di posta elettronica in modo che l'utente possa risolvere il problema, ad esempio rimuovendo destinatari specifici o assegnando un'etichetta al messaggio di posta elettronica. 


> [!TIP]
> Sebbene nell'esercitazione per il client Azure Information Protection anziché il client di assegnazione di etichette unificato, è possibile visualizzare queste impostazioni in azione autonomamente con avanzate [esercitazione: Configurare Azure Information Protection per controllare oversharing di informazioni tramite Outlook](../infoprotect-oversharing-tutorial.md).

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per etichette specifiche:

Il criterio selezionato, per creare uno o più delle seguenti impostazioni avanzate con le chiavi seguenti. Per i valori, specificare una o più etichette in base al GUID, ciascuno separato da una virgola.

Valore di esempio per più etichetta GUID sotto forma di stringa separato da virgole: `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- Messaggi di avviso:
    
    - Chiave: **OutlookWarnUntrustedCollaborationLabel**
    
    - Valore: \< **etichettare i GUID, delimitati da virgole**>

- Messaggi di giustificazione:
    
    - Chiave: **OutlookJustifyUntrustedCollaborationLabel**
    
    - Valore: \< **etichettare i GUID, delimitati da virgole**>

- Messaggi di blocco:
    
    - Chiave: **OutlookBlockUntrustedCollaborationLabel**
    
    - Valore: \< **etichettare i GUID, delimitati da virgole**>


Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}


### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per i messaggi di posta elettronica o gli allegati senza etichetta:

Per lo stesso criterio di etichetta, creare la seguente advanced client con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Avvisa**

- Messaggi di giustificazione:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Giustifica**

- Messaggi di blocco:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Bloccato**

- Disattivare questi messaggi:
    
    - Chiave: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Off**


Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Per definire estensioni di file specifico per l'avviso, giustificare o bloccare i messaggi popup per gli allegati di posta elettronica che non hanno un'etichetta

Per impostazione predefinita, l'avviso, giustificare o bloccare i messaggi popup si applicano a tutti i documenti di Office e i documenti PDF. È possibile perfezionare questo elenco specificando quali estensioni di nome file deve visualizzare l'avviso, giustificare oppure bloccare i messaggi con un'ulteriore avanzate impostazione e un elenco delimitato da virgole di file di estensioni del nome.

Valore di esempio per più estensioni file definire come una stringa delimitata da virgole: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

In questo esempio, un documento PDF senza etichetta non genererà un avviso, giustificare o bloccare i messaggi popup.

Per lo stesso criterio di etichetta, immettere le stringhe seguenti: 


- Chiave: **OutlookOverrideUnlabeledCollaborationExtensions**

- Valore: **\<** estensioni per visualizzare i messaggi, separati da virgole di file **>**


Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

### <a name="to-specify-the-allowed-domain-names-for-recipients-exempt-from-the-pop-up-messages"></a>Per specificare i nomi di dominio consentiti per i destinatari esenti dai messaggi popup

Quando si specificano nomi di dominio in un'impostazione client avanzata aggiuntiva, gli utenti non in grado di visualizzare i messaggi popup per i destinatari che hanno tale nome di dominio incluso nell'indirizzo di posta elettronica. In questo caso, i messaggi di posta elettronica vengono inviati senza interruzioni. Per specificare più domini, aggiungerli come stringa singola, delimitata da virgole.

Una configurazione tipica consiste nel rendere visualizzabili i messaggi popup solo dai destinatari che sono esterni all'organizzazione o che non sono partner autorizzati dell'organizzazione. In questo caso, specificare tutti i domini di posta elettronica usati dall'organizzazione e dai partner.

Per lo stesso criterio di etichetta, creare le seguenti impostazioni client avanzate e per il valore, specificare uno o più domini, ognuno dei quali separati da una virgola.

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

Ad esempio, specificare il client avanzato per non bloccare mai i messaggi di posta elettronica inviati agli utenti che dispongono di un indirizzo di posta elettronica di contoso.com, l'impostazione della **OutlookBlockTrustedDomains** e **contoso.com**. Di conseguenza, evitare la visualizzazione di messaggi di avviso popup in Outlook quando inviano un messaggio di posta elettronica john@sales.contoso.com.

Comandi PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Disabilitare l'invio di informazioni sensibili rilevate nei documenti a analitica di Azure Information Protection

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

[Analitica di Azure Information Protection](../reports-aip.md) può individuare e segnalare i documenti salvati dal client Azure Information Protection quando tale contenuto contiene informazioni riservate. Per impostazione predefinita, queste informazioni vengono inviate dal client Azure Information Protection unified imprevisto delle etichette di analitica di Azure Information Protection.

Per modificare questo comportamento in modo che queste informazioni non vengono inviate dal client di assegnazione di etichette unificato, immettere le stringhe seguenti per il criterio di etichetta selezionata:

- Chiave: **RunAuditInformationTypeDiscovery**

- Valore: **False**

Se si imposta questa impostazione client avanzata, i risultati dei controlli sono ancora inviate dal client l'assegnazione di etichette unificato ma le informazioni sono limitate alla creazione di report quando un utente ha eseguito con l'etichetta di contenuto.

Ad esempio:

- Con questa impostazione, è possibile vedere che un utente accede Financial.docx etichettato **Confidential \ Sales**.

- Senza questa impostazione, è possibile notare che Financial.docx contiene 6 numeri di carta di credito.
    
    - Se si abilita anche [Corrispondenze di contenuto per un'analisi più approfondita](../reports-aip.md#content-matches-for-deeper-analysis), si potranno vedere anche i numeri di carta di credito stessi.

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypeDiscovery="False"}

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti

Questa configurazione usa un criterio [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si seleziona la casella di controllo [Analisi di Azure Information Protection](../reports-aip.md) che raccoglie le corrispondenze di contenuto per i tipi di informazioni riservate o le condizioni personalizzate, per impostazione predefinita, queste informazioni vengono inviate da tutti gli utenti. Se si dispongono di alcuni utenti non devono inviare i dati, creare le seguenti impostazioni in un criterio di etichetta per tali utenti client avanzate: 

- Chiave: **LogMatchedContent**

- Valore: **False**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="Disable"}

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette

Questa configurazione usa un'etichetta [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Questa configurazione non è compatibile con i file PDF protetti che hanno un'estensione di file con estensione ppdf. Questi file non possono essere aperto da Esplora File, PowerShell o lo scanner.

Per i documenti di Office con l'etichetta Secure islands, è possibile modificare le etichette un'etichetta di riservatezza a questi documenti tramite un mapping definito. È anche possibile usare questo metodo per riutilizzare le etichette da altre soluzioni quando sono applicate a documenti di Office. 

In seguito a questa opzione di configurazione, la nuova etichetta di riservatezza viene applicata dal client Azure Information Protection unified imprevisto delle etichette come indicato di seguito:

- Per i documenti di Office: Quando il documento viene aperto nell'app desktop, la nuova etichetta di riservatezza viene visualizzata come impostata e viene applicata quando il documento viene salvato.

- Per PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) possibile applicare la nuova etichetta di riservatezza.

- Per Esplora file: Nella finestra di dialogo Azure Information Protection, la nuova etichetta di riservatezza è visualizzata ma non è impostata.

Questa configurazione richiede di specificare un'impostazione avanzata denominata **labelByCustomProperties** per ogni etichetta di riservatezza che si vuole mappare all'etichetta precedente. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

Specificare un nome di regola di migrazione a propria scelta. Usare un nome descrittivo che consente di identificare come uno o più etichette dalla soluzione precedente imprevisto delle etichette deve essere mappato a etichetta di riservatezza. Il nome viene visualizzato nei report dello scanner e nel Visualizzatore eventi.

Si noti che questa impostazione non comporta la rimozione dell'etichetta originale dal documento o di tutti i contrassegni visivi nel documento che l'etichetta originale potrebbe aver applicato. Per rimuovere le intestazioni e piè di pagina, vedere la sezione precedente [rimuovere le intestazioni e piè di pagina da altre soluzioni di assegnazione di etichette](#remove-headers-and-footers-from-other-labeling-solutions).

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta

Requisito: I documenti con l'etichetta di Secure Islands "Riservato" devono essere rietichettati come "Riservato" da Azure Information Protection.

In questo esempio:

- L'etichetta di Secure Islands è **Riservato** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione avanzata:

- Key: **labelByCustomProperties**

- Valore: **L'etichetta protetta Islands è riservato, classificazione, riservato**

Comando PowerShell di esempio, in cui l'etichetta è denominata "Riservato":

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Esempio 2: Mapping uno-a-uno per un altro nome di etichetta

Requisito: I documenti con l'etichetta di Secure Islands "Sensibile" devono essere rietichettati come "Riservatezza elevata" da Azure Information Protection.

In questo esempio:

- L'etichetta di Secure Islands è **Sensibile** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione avanzata:

- Key: **labelByCustomProperties**

- Valore: **L'etichetta sicuro Islands è sensibile, classificazione, sensibile**

Comando PowerShell di esempio, in cui l'etichetta è denominata "Riservatezza elevata":

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>Esempio 3: Mapping molti-a-uno di nomi di etichetta

Requisito: Si dispongono di due etichette di Secure Islands che includono la parola "Interno" e si vuole documenti che contengono una di queste etichette di Secure Islands vengano rietichettati come "Generale" dal client Azure Information Protection unified imprevisto delle etichette.

In questo esempio:

- Le etichette di Secure Islands includono la parola **Interno** e sono archiviate nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

- Key: **labelByCustomProperties**

- Valore: **Sicuro Islands contiene interno, classificazione. \*Interna.\***

Comando PowerShell di esempio, in cui l'etichetta è denominata "Generale":

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Esempio 4: Più regole per la stessa etichetta

Quando sono necessarie più regole per la stessa etichetta, definire più valori di stringa per la stessa chiave. 

In questo esempio:

- Etichette di Secure Islands denominata "riservato" e "Segreto" viene archiviato nella proprietà personalizzata denominata * * classificazione e si desidera che il client di assegnazione di etichette unificato di Azure Information Protection per applicare l'etichetta di riservatezza denominato "Riservato":

    Set-Label: Confidential identità AdvancedSettings-@{labelByCustomProperties = ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>Estendere l'etichetta delle regole di migrazione per messaggi di posta elettronica

È possibile usare il labelByCustomProperties avanzata delle impostazioni con i messaggi di Outlook oltre a documenti di Office, specificando un'impostazione di criteri avanzati aggiuntivo dell'etichetta. Tuttavia, questa impostazione non ha un noto negativi impatto sulle prestazioni di Outlook, quindi, configurare questa impostazione altri solo quando si dispone di un requisito di business complessa per risolverlo e ricordare di impostare un valore stringa null dopo aver completato la migrazione dal altra soluzione di assegnazione di etichette.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti per il criterio di etichetta selezionata:

- Chiave: **EnableLabelByMailHeader**

- Valore: **Mar**

Comando PowerShell di esempio, in cui il criterio di etichetta denominato "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Applicare una proprietà personalizzata quando viene applicata un'etichetta

Questa configurazione usa un'etichetta [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Potrebbero esserci alcuni scenari quando si desidera applicare uno o più proprietà personalizzate a un messaggio di posta elettronica o documento oltre ai metadati che viene applicato da un'etichetta di riservatezza.

Ad esempio:

- Sei nel durante del [eseguendo la migrazione da un'altra soluzione di assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions), ad esempio Secure Islands. Per garantire l'interoperabilità durante la migrazione, è opportuno etichette di riservatezza da applicare anche una proprietà personalizzata che viene usata per l'altra soluzione di assegnazione di etichette.

- Per il sistema di gestione dei contenuti, quali SharePoint o una soluzione di gestione di documenti da un altro fornitore, si desidera utilizzare un nome di proprietà personalizzato coerente con valori diversi per le etichette e con nomi descrittivi anziché il GUID di etichetta.

Per i documenti di Office e i messaggi di Outlook di quell'etichetta agli utenti tramite Azure Information Protection unified imprevisto delle etichette client, è possibile aggiungere uno o più proprietà personalizzate definite. È anche possibile usare questo metodo per il client di assegnazione di etichette unificato per visualizzare una proprietà personalizzata come un'etichetta da altre soluzioni per il contenuto non è ancora etichettato dal client di assegnazione di etichette unificato.

In seguito a questa opzione di configurazione, tutte le altre proprietà personalizzate vengono applicate dal client Azure Information Protection unified imprevisto delle etichette come indicato di seguito:

- Per i documenti di Office: Quando il documento viene etichettato nell'app desktop, le proprietà aggiuntive personalizzate vengono applicate quando il documento viene salvato.

- Per messaggi di posta elettronica di Outlook: Quando viene applicata un'etichetta di messaggio di posta elettronica in Outlook, vengono applicate le proprietà aggiuntive per l'intestazione x-quando viene inviato il messaggio di posta elettronica.

- Per PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) applica le proprietà personalizzate aggiuntive quando il documento viene etichettato e salvato. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) consente di visualizzare le proprietà personalizzate dell'etichetta con mapping se non viene applicata un'etichetta di riservatezza.

- Per Esplora file: Quando l'utente fa clic il file e applica l'etichetta, vengono applicate le proprietà personalizzate.

Questa configurazione richiede di specificare un'impostazione avanzata denominata **customPropertyByLabel** per ogni etichetta di riservatezza da applicare le proprietà personalizzate aggiuntive. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Esempio 1: Aggiungere una singola proprietà personalizzate per un'etichetta

Requisito: I documenti identificati come "Riservato" dal client Azure Information Protection unified imprevisto delle etichette devono avere la proprietà personalizzata aggiuntiva denominata "Classificazione" con il valore di "Segreto".

In questo esempio:

- L'etichetta di riservatezza è denominato **Confidential** e crea una proprietà personalizzata denominata **classificazione** con il valore di **segreto**.

L'impostazione avanzata:

- Key: **customPropertyByLabel**

- Valore: **Classificazione, segreto**

Comando PowerShell di esempio, in cui l'etichetta è denominata "Riservato":

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertyByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Esempio 2: Aggiungere più proprietà personalizzate per un'etichetta

Per aggiungere più di una proprietà personalizzata per la stessa etichetta, è necessario definire più valori di stringa per la stessa chiave.

Comando di PowerShell di esempio, in cui l'etichetta è denominata "Generale" e si desidera aggiungere una proprietà personalizzata denominata **classificazione** con il valore di **generali** e una seconda proprietà personalizzata denominata **Sensibilità** con il valore della **interno**:

    Set-Label -Identity General -AdvancedSettings @{customPropertyByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurare un'etichetta per applicare la protezione S/MIME in Outlook

Questa configurazione usa l'etichetta [impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Usare queste impostazioni solo se si dispone di un working [distribuzione di S/MIME](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption) e si desidera un'etichetta per applicare automaticamente questo metodo di protezione per messaggi di posta elettronica anziché la protezione di Rights Management di Azure Information Protection. La protezione risultante è identica a quella applicata quando un utente seleziona manualmente le opzioni di S/MIME da Outlook.

Per configurare un'impostazione avanzata per le firme digitali una S/MIME, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **SMimeSign**

- Valore: **True**

Per configurare un'impostazione avanzata per la crittografia S/MIME, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **SMimeEncrypt**

- Valore: **True**

Se l'etichetta specificata è configurata per la crittografia, per la versione di anteprima del client l'assegnazione di etichette di Azure Information Protection unified, protezione dati di S/MIME sostituisce la protezione di Rights Management solo in Outlook. La versione con disponibilità generale del client di assegnazione di etichette unificata continua a usare le impostazioni di crittografia specificate per l'etichetta nell'interfaccia di amministrazione. Per le app di Office con l'assegnazione di etichette predefinite, queste non si applicano la protezione di S/MIME ma al contrario, applicare la protezione non inoltrare.

Se si desidera venga visualizzato in Outlook solo l'etichetta, configurare l'etichetta per applicare la crittografia **solo messaggi di Outlook di posta elettronica**.

Comandi PowerShell di esempio, in cui l'etichetta è denominata "Solo destinatari":

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Specificare un'etichetta secondaria predefinito per un'etichetta padre

Questa configurazione usa un'etichetta [impostazione avanzata](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell. È supportata dalla versione di anteprima di solo i client unificato imprevisto delle etichette.

Quando si aggiunge un'etichetta secondaria a un'etichetta, gli utenti non è più possano applicare l'etichetta padre a un documento o messaggio di posta elettronica. Per impostazione predefinita, gli utenti selezionano l'etichetta padre per visualizzare le etichette secondarie che si possono applicare e quindi selezionare una di queste etichette secondarie. Se si configura questa impostazione, avanzata quando gli utenti selezionano l'etichetta padre, un'etichetta secondaria viene automaticamente selezionata e applicata per essi: 

- Chiave: **DefaultSubLabelId**

- Valore: \<sublabel GUID >

Comando di PowerShell di esempio, in cui l'etichetta padre è denominata "Riservato" e l'etichetta secondaria "Tutti i dipendenti" ha un GUID di 8faca7b8 - 8d 20-48a3-8ea2-0f96310a848e:

    Set-Label -Identity "Confidential" -AdvancedSettings @{defaultsublabels="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}

## <a name="specify-a-color-for-the-label"></a>Specificare un colore per l'etichetta

Questa configurazione usa l'etichetta [impostazioni avanzate](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) che è necessario configurare tramite Office 365 Security & Compliance Center PowerShell.

Usare questa impostazione avanzata per impostare un colore per un'etichetta. Per specificare il colore, immettere un codice tripletta esadecimale per i componenti (RGB) rossi, verdi e blu del colore. Ad esempio, & 40e0d0 è il valore esadecimale RGB per turchese.

Se è necessario un riferimento per questi codici, sarà disponibile un'utile tabella dal [ \<colore >](https://developer.mozilla.org/docs/Web/CSS/color_value) pagina dalla documentazione web MSDN. È anche possibile trovare i codici in molte applicazioni per la modifica di immagini. Ad esempio quando in Microsoft Paint si sceglie un colore personalizzato in una tavolozza vengono visualizzati automaticamente i valori RGB corrispondenti ed è possibile copiarli.

Per configurare le impostazioni avanzate per il colore dell'etichetta, immettere le stringhe seguenti per l'etichetta selezionata:

- Chiave: **colore**

- Valore: \<Valore esadecimale RGB >

Comando PowerShell di esempio, in cui l'etichetta è denominata "Public":

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, gli utenti non sarebbero in genere necessario eseguire l'accesso come utente diverso quando usano Azure Information Protection unified client imprevisto delle etichette. Per un amministratore, tuttavia, può essere necessario accedere con le credenziali di un altro utente durante una fase di testing. 

È possibile verificare a quale account è stato eseguito l'accesso usando la finestra di dialogo **Microsoft Azure Information Protection**: Aprire un'applicazione di Office e, nella **Home** scheda, seleziona il **sensibilità** e quindi selezionare **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'uso di un account non corretto impossibilità di scaricare le etichette, o non possono visualizzare le etichette o un comportamento previsto.

Per accedere come utente diverso:

1. Passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non è possibile visualizzare un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare al **Microsoft Azure Information Protection** finestra di dialogo e selezionare **Accedi** dal aggiornata **lo stato del Client** sezione.

Inoltre:

- Se il client di assegnazione di etichette unificato di Azure Information Protection viene ancora eseguito l'accesso con l'account precedente dopo aver completato questi passaggi, eliminare tutti i cookie di Internet Explorer e quindi ripetere i passaggi 1 e 2.

- Se si usa la funzione Single Sign-On, è necessario uscire da Windows e accedere con un account utente diverso dopo aver eliminato il file del token. Il client di assegnazione di etichette unificato di Azure Information Protection quindi esegue automaticamente l'autenticazione usando l'accesso dell'account utente.

- Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. Per testare Azure Information Protection con più tenant, usare computer diversi.

- È possibile usare la **Reimposta le impostazioni** opzione **Guida e commenti** per disconnettersi ed eliminare le impostazioni e le etichette scaricate di Office 365 Centro sicurezza e conformità, il Il Centro sicurezza di Microsoft 365 o il centro di conformità di Microsoft 365.


## <a name="change-the-local-logging-level"></a>Modificare il livello di registrazione locale

Per impostazione predefinita, Azure Information Protection unified imprevisto delle etichette client scrive file di log client per il **%localappdata%\Microsoft\MSIP** cartella. Questi file sono destinati al supporto tecnico Microsoft per la risoluzione dei problemi.
 
Per modificare il livello di registrazione per questi file, individuare il nome di valore seguente del Registro di sistema e impostare il valore per il livello di registrazione necessario:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

Impostare il livello di registrazione su uno dei valori seguenti:

- **Off**: nessuna registrazione locale.

- **Errore**: solo errori.

- **Info**: registrazione minima che non include ID evento.

- **Debug**: Informazioni complete.

- **Traccia**: Registrazione dettagliata (impostazione predefinita per i client).

Questa impostazione del Registro di sistema non modifica le informazioni che viene inviate ad Azure Information Protection per [reporting centralizzato](../reports-aip.md).


## <a name="next-steps"></a>Passaggi successivi
Ora che è stato personalizzato il client di assegnazione di etichette unificato di Azure Information Protection, vedere le risorse seguenti per informazioni aggiuntive che potrebbe essere necessario supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)
