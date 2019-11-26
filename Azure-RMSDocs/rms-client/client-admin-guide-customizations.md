---
title: Custom configurations - Azure Information Protection client
description: Informazioni sulla personalizzazione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v1client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 643715037716dcb30356b08c34e48047dd4f7074
ms.sourcegitcommit: 487e681c9683b8adb7ae6fcfb374830bf0e5ad72
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2019
ms.locfileid: "74479178"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client Azure Information Protection

>*Applies to: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions for: [Azure Information Protection client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client di Azure Information Protection.

Alcune di queste impostazioni richiedono la modifica del Registro di sistema e alcune usano impostazioni avanzate che è necessario configurare nel Portale di Azure e quindi pubblicare perché i client possano scaricarle.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Come configurare le impostazioni avanzate di configurazione del client nel portale

1. If you haven't already done so, in a new browser window, [sign in to the Azure portal](../configure-policy.md#signing-in-to-the-azure-portal), and then navigate to the **Azure Information Protection** pane.

2. Dall'opzione di menu **Classificazioni** > **Etichette**: selezionare **Criteri**.

3. On the **Azure Information Protection - Policies** pane, select the context menu ( **...** ) next to the policy to contain the advanced settings. Selezionare quindi **Impostazioni avanzate**.
    
    È possibile configurare le impostazioni avanzate per i criteri globali e per i criteri con ambito.

4. On the **Advanced settings** pane, type the advanced setting name and value, and then select **Save and close**.

5. Assicurarsi che gli utenti interessati da questi criteri riavviino le applicazioni di Office eventualmente aperte.

6. If you no longer need the setting and want to revert to the default behavior: On the **Advanced settings** pane, select the context menu ( **...** ) next to the setting you no longer need, and then select **Delete**. Fare clic su **Salva e chiudi**.

#### <a name="available-advanced-client-settings"></a>Impostazioni client avanzate disponibili

|Impostazioni|Scenario e istruzioni|
|----------------|---------------|
|DisableDNF|[Nascondere o visualizzare il pulsante Non inoltrare in Outlook](#hide-or-show-the-do-not-forward-button-in-outlook)|
|DisableMandatoryInOutlook|[Exempt Outlook messages from mandatory labeling](#exempt-outlook-messages-from-mandatory-labeling)|
|CompareSubLabelsInAttachmentAction|[Abilitare il supporto dell'ordinamento delle etichette secondarie](#enable-order-support-for-sublabels-on-attachments) 
|ContentExtractionTimeout|[Change the timeout settings for the scanner](#change-the-timeout-settings-for-the-scanner)
|EnableBarHiding|[Nascondere in modo permanente la barra di Azure Information Protection](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnableCustomPermissionsForCustomProtectedFiles|[Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnablePDFv2Protection|[Non proteggere i file PDF usando lo standard ISO per la crittografia dei file PDF](#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|FileProcessingTimeout|[Change the timeout settings for the scanner](#change-the-timeout-settings-for-the-scanner)
|LabelbyCustomProperty|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LabelToSMIME|[Configurare un'etichetta per applicare la protezione S/MIME in Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|LogLevel|[Modificare il livello di registrazione locale](#change-the-local-logging-level)
|LogMatchedContent|[Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti](#disable-sending-information-type-matches-for-a-subset-of-users)|
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
|PostponeMandatoryBeforeSave|[Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|ProcessUsingLowIntegrity|[Disabilitare il livello di integrità basso per lo scanner](#disable-the-low-integrity-level-for-the-scanner)|
|PullPolicy|[Supporto per i computer disconnessi](#support-for-disconnected-computers)
|RemoveExternalContentMarkingInApp|[Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Aggiungere "Segnala un problema" per gli utenti](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[Disable sending discovered sensitive information in documents to Azure Information Protection analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|RunPolicyInBackground|[Attivare l'esecuzione continua della classificazione in background](#turn-on-classification-to-run-continuously-in-the-background)|
|ScannerConcurrencyLevel|[Limitare il numero di thread usati dallo scanner](#limit-the-number-of-threads-used-by-the-scanner)|
|SyncPropertyName|[Etichettare un documento di Office usando una proprietà personalizzata esistente](#label-an-office-document-by-using-an-existing-custom-property)|
|SyncPropertyState|[Etichettare un documento di Office usando una proprietà personalizzata esistente](#label-an-office-document-by-using-an-existing-custom-property)|

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitare le richieste di accesso per i computer solo AD RMS

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection. Per i computer che comunicano solo con AD RMS questa configurazione può comportare una richiesta di accesso non necessaria per gli utenti. È possibile evitare questa richiesta di accesso modificando il Registro di sistema.

 - Individuare il nome di valore seguente e quindi impostare i dati del valore su **0**:
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indipendentemente da questa impostazione, il client Azure Information Protection segue comunque il [processo standard di individuazione del servizio RMS](client-deployment-notes.md#rms-service-discovery) per trovare il proprio cluster AD RMS.

## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, in genere gli utenti non hanno bisogno di accedere con un nome utente diverso quando usano il client Azure Information Protection. Per un amministratore, tuttavia, può essere necessario accedere con le credenziali di un altro utente durante una fase di testing. 

È possibile verificare con quale account è stato eseguito l'accesso usando la finestra di dialogo di **Microsoft Azure Information Protection**: nell'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'uso di un account non corretto è l'impossibilità di scaricare i criteri di Azure Information Protection, di visualizzare le etichette corrette o di ottenere il comportamento previsto.

Per accedere come utente diverso:

1. Passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzato un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e fare clic su **Accedi** dalla sezione **Stato del client** aggiornata.

Inoltre:

- Se l'accesso al client Azure Information Protection risulta ancora con l'account precedente dopo aver completato questi passaggi, eliminare tutti i cookie di Internet Explorer e quindi ripetere i passaggi 1 e 2.

- Se si usa la funzione Single Sign-On, è necessario uscire da Windows e accedere con un account utente diverso dopo aver eliminato il file del token. Il client di Azure Information Protection esegue quindi automaticamente l'autenticazione tramite l'account utente usato per l'accesso.

- Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. Per testare Azure Information Protection con più tenant, usare computer diversi.

- È possibile usare l'opzione **Ripristina le impostazioni** in **Guida e commenti** per disconnettersi ed eliminare i criteri di Azure Information Protection scaricati.


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>Applicare la modalità di sola protezione quando l'organizzazione dispone di licenze miste

Se l'organizzazione non ha alcuna licenza per Azure Information Protection, ma dispone di licenze per Office 365 che includono il servizio Azure Rights Management per la protezione dei dati, il client Azure Information Protection per Windows viene eseguito automaticamente in [modalità di sola protezione](client-protection-only-mode.md).

Tuttavia, se l'organizzazione ha una sottoscrizione per Azure Information Protection, tutti i computer Windows possono scaricare i criteri di Azure Information Protection per impostazione predefinita. Il client Azure Information Protection non gestisce il controllo e l'applicazione delle licenze. 

Se alcuni utenti non dispongono di una licenza di Azure Information Protection, ma hanno una licenza per Office 365 che include il servizio Azure Rights Management, modificare il Registro di sistema nei computer degli utenti per impedire loro di eseguire le funzionalità di classificazione ed etichettatura senza licenza da Azure Information Protection.

Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Controllare inoltre che in questi computer non esista un file denominato **Policy.msip** nella cartella **%LocalAppData%\Microsoft\MSIP**. Se il file esiste, eliminarlo. Questo file contiene i criteri di Azure Information Protection e potrebbe essere stato scaricato prima della modifica del Registro di sistema o se il client Azure Information Protection è stato installato con l'opzione demo.

## <a name="add-report-an-issue-for-users"></a>Aggiungere "Segnala un problema" per gli utenti

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si specifica la seguente impostazione client avanzata, gli utenti visualizzano l'opzione **Segnala un problema**, che può essere selezionata dalla finestra di dialogo **Guida e commenti** del client. Specificare una stringa HTTP per il collegamento. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **ReportAnIssueLink**

- Valore: **\<stringa HTTP>**

Valore di esempio per un sito Web: `https://support.contoso.com`

Valore di esempio per un indirizzo di posta elettronica: `mailto:helpdesk@contoso.com`

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. If you have computers that you know will not be able to connect to the internet for a period of time, you can prevent the client from attempting to connect to the service by editing the registry. 

Note that without an internet connection, the client cannot apply protection (or remove protection) by using your organization's cloud-based key. Il client può invece usare esclusivamente le etichette che applicano solo la classificazione o la protezione che usa [HYOK](../configure-adrms-restrictions.md).

È possibile evitare una richiesta di accesso al servizio Azure Information Protection tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che è necessario configurare nel portale di Azure, per poi scaricare i criteri per i computer. In alternativa, è possibile evitare questa richiesta di accesso modificando il Registro di sistema.

- Per configurare l'impostazione client avanzata:
    
    1. Immettere le stringhe seguenti:
    
        - Chiave: **PullPolicy**
        
        - Valore: **False**
    
    2. Scaricare i criteri con questa impostazione e installarli nei computer seguendo le istruzioni che seguono.

- In alternativa, modificare il Registro di sistema:
    
    - Individuare il nome di valore seguente e quindi impostare i dati del valore su **0**:
    
        **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 


Il client deve avere un file di criteri validi denominato **Policy.msip** nella cartella **%LocalAppData%\Microsoft\MSIP**.

È possibile esportare i criteri globali o i criteri con ambito dal portale di Azure e copiare il file esportato nel computer client. È anche possibile usare questo metodo per sostituire un file di criteri non aggiornato con i criteri più recenti. Esportare i criteri, tuttavia, non supporta lo scenario in cui un utente appartiene a più di un criterio con ambito. Tenere anche presente che se gli utenti selezionano l'opzione **Ripristina le impostazioni** in [Guida e commenti](client-admin-guide.md#help-and-feedback-section), questa azione elimina il file dei criteri e rende il client inutilizzabile fino a quando non si sostituisce manualmente il file dei criteri o il client si connette al servizio per scaricare i criteri.

Quando si esportano i criteri dal portale di Azure, viene scaricato un file ZIP che contiene più versioni dei criteri. Queste versioni dei criteri corrispondono a versioni diverse del client Azure Information Protection:

1. Decomprimere il file e usare la tabella seguente per identificare il file di criteri necessario. 
    
    |Nome file|Versione del client corrispondente|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |versione 1.2|
    |Policy1.2.msip |versione 1.3 - 1.7|
    |Policy1.3.msip |versione 1.8 - 1.29|
    |Policy1.4.msip |versione 1.32 e successive|
    
2. Rinominare il file identificato come **Policy.msip**, quindi copiarlo nella cartella **%LocalAppData%\Microsoft\MSIP** nei computer in cui è installato il client Azure Information Protection. 

If your disconnected computer is running the current GA version of the Azure Information Protection scanner, there are additional configuration steps you must take. For more information, see [Restriction: The scanner server cannot have internet connectivity](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity) from the scanner deployment instructions.

## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Nascondere o visualizzare il pulsante Non inoltrare in Outlook

Il metodo consigliato per configurare questa opzione è tramite l'[impostazione dei criteri](../configure-policy-settings.md) **Add the Do Not Forward button to the Outlook ribbon** (Aggiungi il pulsante Non inoltrare alla barra multifunzione di Outlook). Tuttavia, è possibile configurare questa opzione anche tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) configurata nel portale di Azure.

Quando è configurata, questa impostazione nasconde o visualizza il pulsante **Non inoltrare** sulla barra multifunzione in Outlook. Questa impostazione non influisce sull'opzione Non inoltrare nei menu di Office.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **DisableDNF**

- Valore: **True** per nascondere il pulsante o **False** per visualizzarlo

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate

Il metodo consigliato per configurare questa opzione è tramite l'[impostazione dei criteri](../configure-policy-settings.md) **Make the custom permissions option available for users** (Rendi disponibile l'opzione per le autorizzazioni personalizzate). Tuttavia, è possibile configurare questa opzione anche tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) configurata nel portale di Azure. 

Quando si configura questa impostazione e si pubblicano i criteri per gli utenti, le opzioni per le autorizzazioni personalizzate diventano visibili per gli utenti in modo che possano selezionare impostazioni di protezione personali oppure sono nascoste e quindi gli utenti non possono selezionare impostazioni di protezione personali, se non richiesto.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableCustomPermissions**

- Valore: **True** per rendere visibile l'opzione per le autorizzazioni personalizzate o **False** per nasconderla

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Quando si configura l'[impostazione di criteri](../configure-policy-settings.md) **Rendi disponibile agli utenti l'opzione per le autorizzazioni personalizzate** o l'impostazione client avanzata equivalente nella sezione precedente, gli utenti non possono visualizzare o modificare le autorizzazioni personalizzate già impostate in un documento protetto. 

Quando si crea e configura questa impostazione client avanzata, gli utenti possono visualizzare e modificare le autorizzazioni personalizzate per un documento protetto quando usano Esplora file e fare clic con il pulsante destro del mouse sul file. L'opzione **Autorizzazioni personalizzate** del pulsante **Proteggi** sulla barra multifunzione di Office rimane nascosta.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **EnableCustomPermissionsForCustomProtectedFiles**

- Valore: **True**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Nascondere in modo permanente la barra di Azure Information Protection

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Usarla solo quando l'[impostazione dei criteri](../configure-policy-settings.md) **Display the Information Protection bar in Office apps** (Visualizza la barra di Information Protection nelle app di Office) è impostata su **On** (Attiva).

Per impostazione predefinita, se un utente cancella l'opzione **Mostra barra** dalla scheda **Pagina iniziale**, il gruppo **Protezione**, il pulsante **Proteggi**, la barra di Information Protection non viene più visualizzata in quell'app Office. La barra viene tuttavia automaticamente visualizzata di nuovo alla successiva apertura di un'app Office.

Per impedire che la barra sia nuovamente visualizzata in automatico se è stato scelto di nasconderla, usare l'impostazione client. Questa impostazione non ha alcun effetto se l'utente chiude la barra tramite l'icona **Chiudi questa barra**.

Anche se la barra di Azure Information Protection rimane nascosta, gli utenti possono visualizzarla temporaneamente per selezionare un'etichetta, se è stata configurata la classificazione consigliata o se un documento o un messaggio di posta elettronica deve avere un'etichetta. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableBarHiding**

- Valore: **True**

## <a name="enable-order-support-for-sublabels-on-attachments"></a>Abilitare il supporto dell'ordinamento delle etichette secondarie per gli allegati

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Usare questa impostazione quando sono disponibili etichette secondarie ed è stata configurata l'[impostazione di criteri](../configure-policy-settings.md) seguente:

- **Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati**

Configurare le stringhe seguenti:

- Key: **CompareSubLabelsInAttachmentAction**

- Valore: **True**

Senza questa impostazione, al messaggio di posta elettronica viene applicata la prima etichetta con la classificazione più alta individuata dall'etichetta padre. 

Con questa impostazione, al messaggio di posta elettronica viene applicata l'etichetta secondaria con la classificazione più alta ordinata per ultima dall'etichetta padre. Se occorre riordinare le etichette per applicare quella desiderata per questo scenario, vedere [Come eliminare o riordinare un'etichetta per Azure Information Protection](../configure-policy-delete-reorder.md).

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Exempt Outlook messages from mandatory labeling

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

By default, when you enable the [policy setting](../configure-policy-settings.md) **All documents and emails must have a label**, all saved documents and sent emails must have a label applied. When you configure the following advanced setting, the policy setting applies only to Office documents and not to Outlook messages.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **DisableMandatoryInOutlook**

- Valore: **True**

## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **OutlookRecommendationEnabled**

- Valore: **True**


## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica

Questa configurazione usa più [impostazioni client avanzate](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che devono essere configurate nel portale di Azure.

Quando si creano e configurano le impostazioni client avanzate seguenti, gli utenti visualizzano messaggi popup di Outlook che possono avvertirli prima dell'invio di un messaggio di posta elettronica, chiedere di giustificare il motivo dell'invio o impedire l'invio di un messaggio di posta elettronica per uno degli scenari seguenti:

- **Il messaggio di posta elettronica o un suo allegato hanno un'etichetta specifica**:
    - L'allegato può essere qualsiasi tipo di file

- **Il messaggio di posta elettronica o l'allegato non hanno un'etichetta**:
    - L'allegato può essere un documento di Office o un documento PDF

When these conditions are met, the user sees a pop-up message with one of the following actions:

- **Warn**: The user can confirm and send, or cancel.

- **Justify**: The user is prompted for justification (predefined options or free-form).  L'utente può quindi inviare o annullare il messaggio di posta elettronica. Il testo della giustificazione è scritto nell'intestazione X- del messaggio di posta elettronica in modo da poter essere letto dagli altri sistemi. Ad esempio, servizi di prevenzione della perdita di dati.

- **Block**: The user is prevented from sending the email while the condition remains. Il messaggio include il motivo del blocco del messaggio di posta elettronica in modo che l'utente possa risolvere il problema, ad esempio rimuovendo destinatari specifici o assegnando un'etichetta al messaggio di posta elettronica. 

When the popup-messages are for a specific label, you can configure exceptions for recipients by domain name.

The resulting actions from the pop-up messages are logged to the local Windows event log **Applications and Services Logs** > **Azure Information Protection**:

- Warn messages: Information ID 301

- Justify messages: Information ID 302

- Block messages: Information ID 303

Voce dell'evento di esempio di un messaggio di giustificazione:

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Price list.msg
Item Name: Price list
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```
The following sections contain configuration instructions for each advanced client setting, and you can see them in action for yourself with [Tutorial: Configure Azure Information Protection to control oversharing of information using Outlook](../infoprotect-oversharing-tutorial.md).

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per etichette specifiche:

Per implementare i messaggi popup per etichette specifiche, è necessario conoscere l'ID etichetta per tali etichette. The label ID value is displayed on the **Label** pane, when you view or configure the Azure Information Protection policy in the Azure portal. Per i file a cui sono state applicate etichette, è anche possibile eseguire il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) per identificare l'ID etichetta (MainLabelId o SubLabelId). Quando un'etichetta ha etichette secondarie, specificare sempre l'ID della sola etichetta secondaria e non dell'etichetta padre.

Creare una o più delle impostazioni client avanzate seguenti con le chiavi seguenti. Per i valori, specificare una o più etichette in base ai rispettivi ID separandoli con una virgola.

Valore di esempio per più ID etichetta sotto forma di stringa delimitata da virgole: `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- Messaggi di avviso:
    
    - Key: **OutlookWarnUntrustedCollaborationLabel**
    
    - Valore: \<**ID etichetta, delimitato da virgole**>

- Messaggi di giustificazione:
    
    - Key: **OutlookJustifyUntrustedCollaborationLabel**
    
    - Valore: \<**ID etichetta, delimitato da virgole**>

- Messaggi di blocco:
    
    - Key: **OutlookBlockUntrustedCollaborationLabel**
    
    - Valore: \<**ID etichetta, delimitato da virgole**>

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>To exempt domain names for pop-up messages configured for specific labels

For the labels that you've specified with these pop-up messages, you can exempt specific domain names so that users do not see the messages for recipients who have that domain name included in their email address. In questo caso, i messaggi di posta elettronica vengono inviati senza interruzioni. Per specificare più domini, aggiungerli come stringa singola, delimitata da virgole.

Una configurazione tipica consiste nel rendere visualizzabili i messaggi popup solo dai destinatari che sono esterni all'organizzazione o che non sono partner autorizzati dell'organizzazione. In questo caso, specificare tutti i domini di posta elettronica usati dall'organizzazione e dai partner.

Create the following advanced client settings and for the value, specify one or more domains, each one separated by a comma.

Valore di esempio per più domini sotto forma di stringa delimitata da virgole: `contoso.com,fabrikam.com,litware.com`

- Messaggi di avviso:
    
    - Key: **OutlookWarnTrustedDomains**
    
    - Valore: **\<** nomi di dominio, delimitati da virgole **>**

- Messaggi di giustificazione:
    
    - Key: **OutlookJustifyTrustedDomains**
    
    - Valore: **\<** nomi di dominio, delimitati da virgole **>**

- Messaggi di blocco:
    
    - Key: **OutlookBlockTrustedDomains**
    
    - Valore: **\<** nomi di dominio, delimitati da virgole **>**

For example, you have specified the **OutlookBlockUntrustedCollaborationLabel** advanced client setting for the **Confidential \ All Employees** label. You now specify the additional advanced client setting of **OutlookBlockTrustedDomains** and **contoso.com**. As a result, a user can send an email to john@sales.contoso.com when it is labeled **Confidential \ All Employees** but will be blocked from sending an email with the same label to a Gmail account.

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per i messaggi di posta elettronica o gli allegati senza etichetta:

Creare l'impostazione client avanzata seguente con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Warn**

- Messaggi di giustificazione:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Justify**

- Messaggi di blocco:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Block**

- Disattivare questi messaggi:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Off**

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>To define specific file name extensions for the warn, justify, or block pop-up messages for email attachments that don't have a label

By default, the warn, justify, or block pop-up messages apply to all Office documents and PDF documents. You can refine this list by specifying which file name extensions should display the warn, justify, or block messages with an additional advanced client property and a comma-separated list of file name extensions.

Example value for multiple file name extensions to define as a comma-separated string: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

In this example, an unlabeled PDF document will not result in warn, justify, or block pop-up messages.


- Key: **OutlookOverrideUnlabeledCollaborationExtensions**

- Value: **\<** file name extensions to display messages, comma separated **>**

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>To specify a different action for email messages without attachments

By default, the value that you specify for OutlookUnlabeledCollaborationAction to warn, justify, or block pop-up messages applies to emails or attachments that don't have a label. You can refine this configuration by specifying another advanced client setting for email messages that don't have attachments.

Creare l'impostazione client avanzata seguente con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Warn**

- Messaggi di giustificazione:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Justify**

- Messaggi di blocco:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Block**

- Disattivare questi messaggi:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Off**

If you don't specify this client setting, the value that you specify for OutlookUnlabeledCollaborationAction is used for unlabeled email messages without attachments as well as unlabeled email messages with attachments.


## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata nei criteri di Azure Information Protection per l'impostazione **Selezionare l'etichetta predefinita**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per applicare un'etichetta diversa, è necessario specificare il relativo ID. The label ID value is displayed on the **Label** pane, when you view or configure the Azure Information Protection policy in the Azure portal. Per i file a cui sono state applicate etichette, è anche possibile eseguire il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) per identificare l'ID etichetta (MainLabelId o SubLabelId). Quando un'etichetta ha etichette secondarie, specificare sempre l'ID della sola etichetta secondaria e non dell'etichetta padre.

Per fare in modo che Outlook non applichi l'etichetta predefinita, specificare **Nessuna**.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **OutlookDefaultLabel**

- Valore: \<**ID etichetta**> o **Nessuna**

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurare un'etichetta per applicare la protezione S/MIME in Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Usare questa impostazione solo se è disponibile una [distribuzione di S/MIME](https://docs.microsoft.com/exchange/s-mime-for-message-signing-and-encryption) funzionante e si vuole che un'etichetta applichi automaticamente questo metodo di protezione per i messaggi di posta elettronica anziché la protezione di Rights Management da Azure Information Protection. La protezione risultante è identica a quella applicata quando un utente seleziona manualmente le opzioni di S/MIME da Outlook.

Per questa configurazione è necessario specificare un'impostazione client avanzata denominata **LabelToSMIME** per ogni etichetta di Azure Information Protection a cui si vuole applicare la protezione S/MIME. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[Azure Information Protection label ID];[S/MIME action]`

The label ID value is displayed on the **Label** pane, when you view or configure the Azure Information Protection policy in the Azure portal. Per usare S/MIME con un'etichetta secondaria, è necessario specificare sempre l'ID solo dell'etichetta secondaria e non dell'etichetta padre. Quando si specifica un'etichetta secondaria, l'etichetta padre deve essere nello stesso ambito o nei criteri globali.

L'azione S/MIME può essere:

- `Sign;Encrypt`: per applicare una firma digitale e la crittografia S/MIME

- `Encrypt`: per applicare solo la crittografia S/MIME

- `Sign`: per applicare solo una firma digitale

Valori di esempio per l'ID etichetta **dcf781ba-727f-4860-b3c1-73479e31912b**:

- Per applicare una firma digitale e la crittografia S/MIME:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign;Encrypt**

- Per applicare solo la crittografia S/MIME:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Encrypt**
    
- Per applicare solo una firma digitale:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign**

Come risultato di questa configurazione, quando viene applicata l'etichetta per un messaggio di posta elettronica, al messaggio di posta elettronica viene applicata la protezione S/MIME oltre alla classificazione dell'etichetta.

Se l'etichetta specificata è configurata per la protezione di Rights Management nel portale di Azure, la protezione S/MIME sostituisce la protezione di Rights Management solo in Outlook. Per tutti gli altri scenari che supportano l'etichettatura, verrà applicata la protezione di Rights Management.

Se si vuole che l'etichetta sia visibile solo in Outlook, configurare l'etichetta per applicare la singola azione definita dall'utente **Non inoltrare**, come descritto in [Guida introduttiva: Configurare un'etichetta che consente di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate](../quickstart-label-dnf-protectedemail.md).

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Se si usa l'[impostazione dei criteri](../configure-policy-settings.md) **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, agli utenti viene richiesto di selezionare un'etichetta quando salvano per la prima volta un documento di Office e quando inviano un messaggio di posta elettronica. Per i documenti, gli utenti possono selezionare **Non ora** per chiudere temporaneamente la richiesta di selezionare un'etichetta e tornare al documento. Non possono però chiudere il documento salvato senza etichettarlo. 

Quando si configura questa impostazione l'opzione **Non ora** viene rimossa. In questo modo, quando il documento viene salvato per la prima volta gli utenti sono obbligati a selezionare un'etichetta.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **PostponeMandatoryBeforeSave**

- Valore: **False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>Attivare l'esecuzione continua della classificazione in background

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Quando si configura questa impostazione, cambia il [comportamento predefinito](../configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) del client Azure Information Protection rispetto all'applicazione delle etichette automatiche e consigliate ai documenti: 

- Per Word, Excel e PowerPoint, la classificazione automatica viene eseguita in modo continuo in background.  

Il comportamento rimane invariato per Outlook.

Quando il client di Azure Information Protection verifica periodicamente nei documenti le regole di condizione specificate, questo comportamento abilita la classificazione automatica e consigliata e la protezione dei documenti archiviati in SharePoint Online. I file di grandi dimensioni vengono salvati più rapidamente perché le regole di condizione sono già state eseguite. 

Le regole di condizione non vengono eseguite in tempo reale durante la digitazione. Vengono eseguite periodicamente come attività in background se il documento viene modificato.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **RunPolicyInBackground**

- Valore: **True**

## <a name="dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>Non proteggere i file PDF usando lo standard ISO per la crittografia dei file PDF

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando un file PDF è protetto con l'ultima versione del client Azure Information Protection, l'estensione risultante rimane pdf ed è conforme allo standard ISO per la crittografia dei file PDF. Per altre informazioni su questo standard, vedere la sezione **7.6 Encryption** (Crittografia) del [documento derivato dalla specifica ISO 32000-1](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf) e pubblicato da Adobe Systems Incorporated.

Se è necessario che il client ripristini il comportamento delle versioni precedenti, ovvero protezione dei file PDF con un'estensione di file ppdf, usare l'impostazione avanzata seguente immettendo questa stringa:

- Chiave: **EnablePDFv2Protection**

- Valore: **False**

Questa impostazione, ad esempio, può essere necessaria per tutti gli utenti se si usa un lettore di file PDF che non supporta lo standard ISO per la crittografia dei file PDF. Oppure può essere necessario configurare questa impostazione per alcuni utenti durante l'introduzione graduale di un lettore di file PDF che supporta il nuovo formato. Un altro possibile motivo per l'uso di questa impostazione è la necessità di aggiungere protezione a documenti PDF firmati. È possibile aggiungere ulteriore protezione ai documenti PDF con il formato con estensione ppdf, poiché questa protezione viene implementata come wrapper per i file. 

Per fare in modo che lo scanner Azure Information Protection usi la nuova impostazione, è necessario riavviare il servizio scanner. Inoltre, lo scanner non proteggerà più i documenti PDF per impostazione predefinita. Se si vuole che i documenti PDF siano protetti dallo scanner quando EnablePDFv2Protection è impostata su False, è necessario [modificare il Registro di sistema](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected).

Per altre informazioni sulla nuova crittografia PDF, vedere il post del blog [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nuovo supporto della crittografia PDF con Microsoft Azure Information Protection).

Per un elenco dei lettori di file PDF che supportano lo standard ISO per la crittografia dei file PDF e i lettori che supportano formati precedenti, vedere [Lettori di file PDF supportati per Microsoft Information Protection](protected-pdf-readers.md).

### <a name="to-convert-existing-ppdf-files-to-protected-pdf-files"></a>Per convertire i file con estensione ppdf esistenti in file con estensione pdf protetti

Dopo che il client Azure Information Protection ha scaricato i criteri client con la nuova impostazione, è possibile usare i comandi di PowerShell per convertire i file con estensione ppdf esistenti in file con estensione pdf protetti, che usano lo standard ISO per la crittografia PDF. 

Per usare le istruzioni seguenti per i file ai quali la protezione non è stata applicata dall'utente, è necessario avere [diritti di utilizzo di Rights Management](../configure-usage-rights.md) per rimuovere la protezione dai file oppure essere un utente con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../configure-super-users.md).

Inoltre quando l'utente usa queste istruzioni per file protetti da altri utenti, diventa l'[autorità di certificazione RMS](../configure-usage-rights.md#rights-management-issuer-and-rights-management-owner). In questo scenario, l'utente che ha protetto il documento in origine non può più tenerne traccia né revocarlo. Se gli utenti hanno l'esigenza di tenere traccia e revocare i loro documenti PDF protetti, chiedere loro di rimuovere manualmente e quindi riapplicare l'etichetta usando Esplora file e facendo clic con il pulsante destro del mouse.

Per usare i comandi di PowerShell per convertire file con estensione ppdf esistenti in file con estensione pdf protetti che usano lo standard ISO per la crittografia PDF:

1. Usare [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) con il file con estensione ppdf. Ad esempio:
    
        Get-AIPFileStatus -Path \\Finance\Projectx\sales.ppdf

2. Nell'output, prendere nota dei valori dei parametri seguenti:
    
   - Il valore (GUID) di **SubLabelId**, se presente. Se questo valore è vuoto, non è stata usata un'etichetta secondaria. In questo caso prendere nota del valore di **MainLabelId**.
    
     Nota: se non è presente neanche un valore per **MainLabelId**, il file non è provvisto di etichetta. In questo caso è possibile usare i comandi [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) e [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) invece dei comandi nei passaggi 3 e 4.
    
   - Valore di **RMSTemplateId**. Se questo valore è **Accesso limitato**, un utente ha protetto il file usando autorizzazioni personalizzate anziché le impostazioni di protezione configurate per l'etichetta. Se si continua, tali autorizzazioni personalizzate verranno sovrascritte dalle impostazioni di protezione dell'etichetta. Decidere se continuare o chiedere all'utente (valore visualizzato per **RMSIssuer**) di rimuovere l'etichetta e riapplicarla, con le relative autorizzazioni personalizzate originali.

3. Rimuovere l'etichetta usando [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) con il parametro *RemoveLabel*. Se si usa l'[impostazione criteri](../configure-policy-settings.md) **Gli utenti devono offrire una giustificazione per la configurazione di un'etichetta di classificazione più bassa, la rimozione di un'etichetta o la rimozione della protezione**, è necessario specificare anche il parametro *Giustificazione* con il motivo. Ad esempio: 
    
        Set-AIPFileLabel \\Finance\Projectx\sales.ppdf -RemoveLabel -JustificationMessage 'Removing .ppdf protection to replace with .pdf ISO standard'

4. Riapplicare l'etichetta originale, specificando il valore dell'etichetta identificato nel passaggio 1. Ad esempio:
    
        Set-AIPFileLabel \\Finance\Projectx\sales.pdf -LabelId d9f23ae3-1234-1234-1234-f515f824c57b

Il file mantiene l'estensione pdf ma viene classificato come in precedenza ed è protetto tramite lo standard ISO per la crittografia PDF.

## <a name="support-for-files-protected-by-secure-islands"></a>Supporto di file protetti da Secure Islands

This configuration option is in preview and might change.

Se è stato usato Secure Islands è possibile che siano stati protetti file di testo, file immagine e file generici. Sono esempi i file con estensione ptxt, pjpeg o pfile. Quando si modifica il registro di sistema come indicato di seguito, Azure Information Protection può decrittografare questi file:


Aggiungere il seguente valore DWORD di **EnableIQPFormats** al percorso del registro seguente e impostare i dati del valore su **1**:

- Per una versione di Windows a 64 bit: HKEY_LOCAL_MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\MSIP

- Per una versione di Windows a 32 bit: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\MSIP

In seguito a questa modifica del registro sono supportati gli scenari seguenti:

- Il visualizzatore Azure Information Protection può aprire questi file protetti.

- Lo scanner Azure Information Protection può verificare la presenza di informazioni riservate in questi file.

- Esplora file, PowerShell e lo scanner Azure Information Protection possono assegnare etichette a questi file. È quindi possibile applicare un'etichetta di Azure Information Protection che applica la nuova protezione da Azure Information Protection o che rimuove la protezione esistente di Secure Islands.

- È possibile usare la [personalizzazione client per la migrazione delle etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions) per convertire automaticamente l'etichetta Secure Islands di questi file protetti in un'etichetta di Azure Information Protection.

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Questa configurazione non è attualmente compatibile con il nuovo comportamento predefinito che protegge i file PDF usando lo standard ISO per la crittografia PDF. In questo scenario non è possibile aprire i file PPDF usando Esplora file, PowerShell o lo scanner. Per risolvere questo problema, usare l'impostazione client avanzata per [non usare lo standard ISO per la crittografia PDF](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).

Per i documenti di Office e i documenti PDF con etichette assegnate da Secure Islands, è possibile riassegnare etichette di Azure Information Protection a questi documenti usando un mapping definito appositamente. È anche possibile usare questo metodo per riutilizzare le etichette da altre soluzioni quando sono applicate a documenti di Office. 

> [!NOTE]
> Se sono presenti file diversi dai documenti Office e PDF protetti da Secure Islands, questi possono essere rietichettati dopo la modifica del registro, come descritto nella [sezione precedente](#support-for-files-protected-by-secure-islands). 

Con questa opzione di configurazione, la nuova etichetta di Azure Information Protection viene applicata mediante il client di Azure Information Protection come indicato di seguito:

- Per i documenti di Office: quando il documento viene aperto nell'app desktop, la nuova etichetta di Azure Information Protection viene visualizzata come impostata e viene applicata quando il documento viene salvato.

- Per Esplora file: nella finestra di dialogo Azure Information Protection, la nuova etichetta di Azure Information Protection viene visualizzata come impostata e viene applicata quando l'utente seleziona **Applica**. Se l'utente seleziona **Annulla** la nuova etichetta non viene applicata.

- Per PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) applica la nuova etichetta di Azure Information Protection. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) non visualizza la nuova etichetta di Azure Information Protection finché non viene impostata da un altro metodo.

- Per lo scanner di Azure Information Protection: l'individuazione segnala quando la nuova etichetta di Azure Information Protection viene impostata e può essere applicata con la modalità di imposizione.

Per questa configurazione è necessario specificare un'impostazione client avanzata denominata **LabelbyCustomProperty** per ogni etichetta di Azure Information Protection che si vuole mappare all'etichetta precedente. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

The label ID value is displayed on the **Label** pane, when you view or configure the Azure Information Protection policy in the Azure portal. Per specificare un'etichetta secondaria, l'etichetta padre deve essere nello stesso ambito o nei criteri globali.

Specificare un nome di regola di migrazione a propria scelta. Usare un nome descrittivo che consente di identificare come deve essere eseguito il mapping di una o più etichette dalla soluzione precedente imprevisto a un'etichetta di Azure Information Protection. Il nome viene visualizzato nei report dello scanner e nel Visualizzatore eventi. Si noti che questa impostazione non comporta la rimozione dell'etichetta originale dal documento o di tutti i contrassegni visivi nel documento che l'etichetta originale potrebbe aver applicato. Per rimuovere le intestazioni e i piè di pagina, vedere la sezione successiva [Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions).

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta

Requirement: Documents that have a Secure Islands label of "Confidential" should be relabeled as "Confidential" by Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection da usare è **Riservato** e ha l'ID etichetta **1ace2cc3-14bc-4142-9125-bf946a70542c**. 

- L'etichetta di Secure Islands è **Riservato** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Value|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c, "L'etichetta Secure Islands è Riservato",Classificazione,Riservato|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Esempio 2: Mapping uno-a-uno per un altro nome di etichetta

Requirement: Documents labeled as "Sensitive" by Secure Islands should be relabeled as "Highly Confidential" by Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection da usare è **Riservatezza elevata** e ha l'ID etichetta **3e9df74d-3168-48af-8b11-037e3021813f**.

- L'etichetta di Secure Islands è **Sensibile** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Value|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f, "L'etichetta Secure Islands è Sensibile",Classificazione,Sensibile|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>Esempio 3: Mapping molti-a-uno di nomi di etichetta

Requirement: You have two Secure Islands labels that include the word "Internal" and you want documents that have either of these Secure Islands labels to be relabeled as "General" by Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection da usare è **Generale** e ha l'ID etichetta **2beb8fe7-8293-444c-9768-7fdc6f75014d**.

- Le etichette di Secure Islands includono la parola **Interno** e sono archiviate nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Value|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d,"L'etichetta Secure Islands contiene Interno",Classificazione,.\*Interno.\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette

Questa configurazione usa più [impostazioni client avanzate](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che devono essere configurate nel portale di Azure. Queste impostazioni sono di anteprima e potrebbero cambiare.

Le impostazioni consentono di rimuovere o sostituire le intestazioni o i piè di pagina basati su testo nei documenti, quando questi contrassegni visivi sono stati applicati da un'altra soluzione di etichettatura. Ad esempio, il piè di pagina precedente contiene il nome di un'etichetta precedente di cui è stata eseguita la migrazione ad Azure Information Protection con un nuovo nome di etichetta e un proprio piè di pagina.

Quando il client ottiene questa configurazione nei relativi criteri, le intestazioni e i piè di pagina precedenti vengono rimossi o sostituiti quando il documento viene aperto nell'app di Office e al documento vengono applicate le etichette di Azure Information Protection.

Questa configurazione non è supportata per Outlook e tenere presente che quando viene usata con Word, Excel e PowerPoint, può influire negativamente sulle prestazioni di queste app per gli utenti. La configurazione consente di definire le impostazioni per ogni applicazione, ad esempio la ricerca di testo nelle intestazioni e nei piè di pagina di documenti di Word, ma non nei fogli di calcolo di Excel o nelle presentazioni di PowerPoint.

Because the pattern matching affects the performance for users, we recommend that you limit the Office application types (**W**ord, E**X**cel, **P**owerPoint) to just those that need to be searched:

- Chiave: **RemoveExternalContentMarkingInApp**

- Valore: \<**tipi di applicazioni di Office WXP**> 

Di seguito sono riportati alcuni esempi.

- Per eseguire la ricerca solo in documenti di Word, specificare **W**.

- Per eseguire la ricerca in documenti di Word e presentazioni di PowerPoint, specificare **WP**.

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

- Chiave: **ExternalContentMarkingToRemove**

- Valore: \<**stringa da confrontare, definita come espressione regolare**> 

#### <a name="multiline-headers-or-footers"></a>Intestazioni o piè di pagina su più righe

Se il testo di un'intestazione o un piè di pagina è su più righe, creare una chiave e un valore per ogni riga. Si supponga, ad esempio, di avere il piè di pagina seguente con due righe:

**The file is classified as Confidential**

**Label applied manually**

Per rimuovere il piè di pagina su più righe, creare le due voci seguenti:

- Chiave 1: **ExternalContentMarkingToRemove**

- Valore chiave 1: **\*Confidential***

- Chiave 2: **ExternalContentMarkingToRemove**

- Valore chiave 2: **\*Label applied*** 

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

Quando si hanno più forme di PowerPoint da rimuovere, creare tante chiavi **PowerPointShapeNameToRemove** quante sono le forme da rimuovere. Per ogni voce specificare il nome della forma da rimuovere.

Per impostazione predefinita, il testo delle intestazioni e dei piè di pagina viene cercato solo negli schemi diapositiva. Per estendere la ricerca a tutte le diapositive, che è un processo con un utilizzo maggiore di risorse, usare un'impostazione client avanzata aggiuntiva denominata **RemoveExternalContentMarkingInAllSlides**:

- Chiave: **RemoveExternalContentMarkingInAllSlides**

- Valore: **True**

## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>Etichettare un documento di Office usando una proprietà personalizzata esistente

> [!NOTE]
> Se si usa questa configurazione e la configurazione per [eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions), l'impostazione di migrazione delle etichette ha la precedenza. 

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si configura questa impostazione, è possibile classificare e, facoltativamente, proteggere un documento di Office quando dispone di una proprietà personalizzata esistente con un valore corrispondente a uno dei nomi di etichetta. Questa proprietà personalizzata può essere impostata da un'altra soluzione di classificazione o può essere impostata come proprietà da SharePoint.

In seguito a questa configurazione, quando un documento senza un'etichetta di Azure Information Protection viene aperto e salvato da un utente in un'app di Office, il documento viene quindi etichettato in modo che corrisponda al valore della proprietà corrispondente. 

Per questa configurazione è necessario specificare due impostazioni avanzate che interagiscono tra di loro. La prima è denominata **SyncPropertyName**, ovvero il nome della proprietà personalizzata che è stata impostata dall'altra soluzione di classificazione o una proprietà impostata da SharePoint. La seconda è denominata **SyncPropertyState** e deve essere impostata su OneWay.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave 1: **SyncPropertyName**

- Valore chiave 1 : \<**nome proprietà**> 

- Chiave 2: **SyncPropertyState**

- Valore chiave 2: **OneWay**

Usare queste chiavi e i valori corrispondenti per una sola proprietà personalizzata.

Si supponga, ad esempio, di avere una colonna di SharePoint denominata **Classificazione** con i valori possibili **Pubblico**, **Generale** e **Riservatezza elevata\Tutti i dipendenti**. I documenti vengono archiviati in SharePoint, con i valori **Pubblico**, **Generale** o **Riservatezza elevata\Tutti i dipendenti** impostati per la proprietà Classificazione.

Per etichettare un documento di Office con uno di questi valori di classificazione, impostare **SyncPropertyName** su **Classificazione** e **SyncPropertyState** a **OneWay**. 

A questo punto, quando un utente apre e salva uno di questi documenti di Office, il documento viene etichettato come **Pubblico**, **Generale** o **Riservatezza elevata\Tutti i dipendenti** se sono presenti etichette con questi nomi nei criteri di Azure Information Protection. In assenza di etichette con questi nomi, il documento rimane senza etichetta.

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Disable sending discovered sensitive information in documents to Azure Information Protection analytics

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

When the Azure Information Protection client is used in Office apps, it looks for sensitive information in documents when they are first saved. Providing the client isn't configured to not sent audit information, any sensitive information types found (predefined or custom) are then sent to [Azure Information Protection analytics](../reports-aip.md). 

The configuration that controls whether the client sends audit information is the [policy setting](../configure-policy-settings.md) of **Send audit data to Azure Information Protection log analytics**. When this policy setting is **On** because you want to send audit information that includes labeling actions but you don't want to send sensitive information types found by the client, enter the following strings:

- Key: **RunAuditInformationTypesDiscovery**

- Valore: **False**

If you set this advanced client setting, auditing information can still be sent from the client but the information is limited to labeling activity.

Ad esempio:

- With this setting, you can see that a user accessed Financial.docx that is labeled **Confidential \ Sales**.

- Without this setting, you can see that Financial.docx contains 6 credit card numbers.
    
    - If you also enable [deeper analytics into your sensitive data](../reports-aip.md#content-matches-for-deeper-analysis), you will additionally be able to see what those credit card numbers are.

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

When you select the checkbox for [Azure Information Protection analytics](../reports-aip.md) that enables deeper analytics into your sensitive data collects the content matches for your sensitive information types or your custom conditions, by default, this information is sent by all users, which includes service accounts that run the Azure Information Protection scanner. In presenza di utenti che non devono inviare questi dati, creare l'impostazione client avanzata seguente in un [criterio con ambito](../configure-policy-scope.md) per questi utenti: 

- Key: **LogMatchedContent**

- Value: **Disable**


## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>Limitare il numero di thread usati dallo scanner

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Per impostazione predefinita, lo scanner usa tutte le risorse del processore disponibili nel computer che esegue il servizio scanner. Se è necessario limitare l'utilizzo della CPU mentre questo servizio esegue l'analisi, creare la seguente impostazione avanzata. 

Come valore specificare il numero di thread simultanei che lo scanner può eseguire in parallelo. Lo scanner usa un thread separato per ogni file analizzato, quindi questa configurazione della limitazione definisce anche il numero di file che possono essere analizzati in parallelo. 

Quando si configura il valore per il test per la prima volta, è consigliabile specificare 2 per ogni core e quindi monitorare i risultati. Se ad esempio si esegue lo scanner in un computer con 4 core, impostare prima il valore su 8. Se necessario, aumentare o diminuire questo numero, in base alle prestazioni risultanti richieste per il computer dello scanner e la velocità di analisi. 

- Key: **ScannerConcurrencyLevel**

- Valore: **\<numero massimo di utenti simultanei>**

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>Disabilitare il livello di integrità basso per lo scanner

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Per impostazione predefinita, lo scanner di Azure Information Protection viene eseguito con un livello di integrità basso. Questa impostazione offre un maggiore isolamento di sicurezza, ma influisce negativamente sulle prestazioni. Il livello di integrità basso è appropriato se si esegue lo scanner con un account con privilegi (ad esempio un account amministratore locale) in quanto questa impostazione aiuta a proteggere il computer che esegue lo scanner.

Quando, tuttavia, l'account del servizio che esegue lo scanner ha solo i diritti indicati nei [prerequisiti dello scanner](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), il livello di integrità basso non è necessario e non è consigliato perché influisce negativamente sulle prestazioni. 

Per altre informazioni sui livelli di integrità di Windows, vedere [What is the Windows Integrity Mechanism?](https://msdn.microsoft.com/library/bb625957.aspx) (Informazioni sul meccanismo di integrità di Windows)

Per configurare questa impostazione avanzata in modo che lo scanner venga eseguito con un livello di integrità assegnato automaticamente da Windows (un account utente standard viene eseguito con un livello di integrità medio), immettere le stringhe seguenti:

- Chiave: **ProcessUsingLowIntegrity**

- Valore: **False**

## <a name="change-the-timeout-settings-for-the-scanner"></a>Change the timeout settings for the scanner

This configuration uses [advanced client settings](#how-to-configure-advanced-client-configuration-settings-in-the-portal) that you must configure in the Azure portal.

By default, the Azure Information Protection scanner has a timeout period of 00:15:00 (15 minutes) to inspect each file for sensitive information types or the regex expressions that you've configured for custom conditions. When the timeout period is reached for this content extraction process, any results before the timeout are returned and further inspection for the file stops. In this scenario, the following error message is logged in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zipped if there are multiple logs): **GetContentParts failed** with **The operation was canceled** in the details.

If you experience this timeout problem because of large files, you can increase this timeout period for full content extraction:

- Key: **ContentExtractionTimeout**

- Value: **\<hh:min:sec>**

The file type can influence how long it takes to scan a file. Example scanning times:

- A typical 100 MB Word file: 0.5-5 minutes

- A typical 100 MB PDF file: 5-20 minutes

- A typical 100 MB Excel file: 12-30 minutes

For some file types that are very large, such as video files, consider excluding them from the scan by adding the file name extension to the **File types to scan** option in the scanner profile.

In addition, the Azure Information Protection scanner has a timeout period of 00:30:00 (30 minutes) for each file that it processes. This value takes into account the time it can take to retrieve a file from a repository and temporarily save it locally for actions that can include decryption, content extraction for inspection, labeling, and encryption.

Although the Azure Information Protection scanner can scan dozens to hundreds of files per minute, if you have a data repository that has a high number of very large files, the scanner can exceed this default timeout period and in the Azure portal, seem to stop after 30 minutes. In this scenario, the following error message is logged in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zipped if there are multiple logs) and the scanner .csv log file: **The operation was canceled**.

A scanner with 4 core processors by default has 16 threads for scanning and the probability of encountering 16 large files in a 30 minute time period depends on the ratio of the large files. For example, if the scanning rate is 200 files per minute, and 1% of files exceed the 30 minute timeout, there is a probability of more than 85% that the scanner will encounter the 30 minute timeout situation. These timeouts can result in longer scanning times and higher memory consumption.

In this situation, if you cannot add more core processors to the scanner computer, consider decreasing the timeout period for better scanning rates and lower memory consumption, but with the acknowledgment that some files will be excluded. Alternatively, consider increasing the timeout period for more accurate scanning results but with the acknowledgment that this configuration will likely result in lower scanning rates and higher memory consumption.

To change the timeout period for file processing, configure the following advanced client setting:

- Key: **FileProcessingTimeout**

- Value: **\<hh:min:sec>**

## <a name="change-the-local-logging-level"></a>Modificare il livello di registrazione locale

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Per impostazione predefinita, il client Azure Information Protection scrive i file di log del client nella cartella **%localappdata%\Microsoft\MSIP**. Questi file sono destinati al supporto tecnico Microsoft per la risoluzione dei problemi.
 
Per modificare il livello di registrazione per questi file, configurare l'impostazione client avanzata seguente:

- Key: **LogLevel**

- Valore: **\<livello di registrazione>**

Impostare il livello di registrazione su uno dei valori seguenti:

- **Off**: No local logging.

- **Error**: Errors only.

- **Info**: Minimum logging, which includes no event IDs (the default setting for the scanner).

- **Debug**: Full information.

- **Trace**: Detailed logging (the default setting for clients). Per lo scanner, questa impostazione ha un impatto significativo sulle prestazioni e deve essere abilitata solo se richiesto dal supporto tecnico Microsoft. Se viene richiesto di impostare questo livello di registrazione per lo scanner, ricordarsi di impostare un valore diverso dopo aver raccolto i log rilevanti.

Questa impostazione client avanzata non modifica le informazioni inviate ad Azure Information Protection per [reporting centralizzato](../reports-aip.md) o le informazioni scritte nel [registro eventi](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) locale.

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Integrazione con la classificazione dei messaggi di Exchange per una soluzione di etichettatura dei dispositivi mobili

Outlook on the web now supports built-in labeling for Exchange Online, which is the recommended method to label emails in Outlook on the web. However, if you're not yet using sensitivity labels that are published from the Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft compliance center, you can use Exchange message classification to extend Azure Information Protection labels to your mobile users when they use Outlook on the web. You can also use this method for Exchange Server. 

Outlook Mobile non supporta la classificazione dei messaggi di Exchange.

Per ottenere questa soluzione: 

1. Usare il cmdlet [New-MessageClassification](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/New-MessageClassification?view=exchange-ps) di Exchange PowerShell per creare le classificazioni dei messaggi con la proprietà Name che esegue il mapping ai nomi di etichetta nei criteri di Azure Information Protection. 

2. Creare una regola del flusso di posta di Exchange per ogni etichetta: applicare la regola quando le proprietà del messaggio includono la classificazione configurata e modificare le proprietà del messaggio per impostare un'intestazione del messaggio. 

     For the message header, you find the information to specify by inspecting the internet headers of an email that you sent and classified by using your Azure Information Protection label. Look for the header **msip_labels** and the string that immediately follows, up to and excluding the semicolon. Ad esempio:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True**
    
    Quindi, per l'intestazione del messaggio nella regola, specificare **msip_labels** per l'intestazione e la parte rimanente della stringa per il valore dell'intestazione. Ad esempio:
    
    ![Regola del flusso di posta di Exchange Online di esempio che imposta l'intestazione del messaggio per un'etichetta di Azure Information Protection specifica](../media/exchange-rule-for-message-header.png)
    
    Nota: quando l'etichetta è un'etichetta secondaria, è necessario specificare anche l'etichetta padre prima dell'etichetta secondaria nel valore di intestazione, usando lo stesso formato. Ad esempio, se il GUID dell'etichetta secondaria è 27efdf94-80a0-4d02-b88c-b615c12d69a9, il valore potrebbe essere simile al seguente: `MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True`

Prima di eseguire il test della configurazione, tenere presente che spesso si verifica un ritardo quando vengono create o modificate le regole del flusso di posta. Ad esempio, può essere necessario attendere un'ora. Se la regola è attiva, quando gli utenti usano Outlook sul Web, si verificano gli eventi seguenti: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Se i destinatari interni visualizzano il messaggio di posta elettronica in Outlook e hanno installato il client di Azure Information Protection, vedono l'etichetta di Azure Information Protection assegnata. 

If your Azure Information Protection labels apply protection, add this protection to the rule configuration: Selecting the option to modify the message security, apply rights protection, and then select the protection template or Do Not Forward option.

È anche possibile configurare regole del flusso di posta per eseguire il mapping inverso. Quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente:

- Per ogni etichetta di Azure Information Protection, creare una regola del flusso di posta da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **General**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver personalizzato il client di Azure Information Protection, vedere le risorse seguenti per altre informazioni eventualmente necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


