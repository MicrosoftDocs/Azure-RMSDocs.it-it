---
title: Configurazioni personalizzate-client Azure Information Protection
description: Informazioni sulla personalizzazione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/12/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v1client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a43bdbf2e4ec14b60ac37164273529c764cffa98
ms.sourcegitcommit: bef2862237ede61c497a54e6fe0179ae4fe5a63e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "68978792"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client di Azure Information Protection.

Alcune di queste impostazioni richiedono la modifica del Registro di sistema e alcune usano impostazioni avanzate che è necessario configurare nel Portale di Azure e quindi pubblicare perché i client possano scaricarle.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Come configurare le impostazioni avanzate di configurazione del client nel portale

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](../configure-policy.md#signing-in-to-the-azure-portal) e quindi passare al pannello **Azure Information Protection**.

2. Dall'opzione di menu **Classificazioni** > **Etichette**: Selezionare i **criteri**.

3. Nel pannello **Azure Information Protection - Criteri** selezionare il menu di scelta rapida ( **...** ) accanto ai criteri, contenente le impostazioni avanzate. Selezionare quindi **Impostazioni avanzate**.
    
    È possibile configurare le impostazioni avanzate per i criteri globali e per i criteri con ambito.

4. Nel pannello **Impostazioni avanzate** digitare il nome e il valore dell'impostazione avanzata e quindi selezionare **Salva e chiudi**.

5. Assicurarsi che gli utenti interessati da questi criteri riavviino le applicazioni di Office eventualmente aperte.

6. Se l'impostazione non è più necessaria e si vuole ripristinare il comportamento predefinito: nel pannello **Impostazioni avanzate** selezionare il menu di scelta rapida ( **...** ) accanto all'impostazione non più necessaria e quindi selezionare **Elimina**. Fare clic su **Salva e chiudi**.

#### <a name="available-advanced-client-settings"></a>Impostazioni client avanzate disponibili

|Impostazione|Scenario e istruzioni|
|----------------|---------------|
|DisableDNF|[Nascondere o visualizzare il pulsante Non inoltrare in Outlook](#hide-or-show-the-do-not-forward-button-in-outlook)|
|DisableMandatoryInOutlook|[Esentare i messaggi di Outlook da un'etichetta obbligatoria](#exempt-outlook-messages-from-mandatory-labeling)|
|CompareSubLabelsInAttachmentAction|[Abilitare il supporto dell'ordinamento delle etichette secondarie](#enable-order-support-for-sublabels-on-attachments) 
|ContentExtractionTimeout|[Modificare le impostazioni di timeout per lo scanner](#change-the-timeout-settings-for-the-scanner)
|EnableBarHiding|[Nascondere in modo permanente la barra di Azure Information Protection](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnableCustomPermissionsForCustomProtectedFiles|[Per i file protetti con autorizzazioni personalizzate, rendere sempre le autorizzazioni personalizzate visualizzabili dagli utenti in Esplora file](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnablePDFv2Protection|[Non proteggere i file PDF usando lo standard ISO per la crittografia dei file PDF](#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|FileProcessingTimeout|[Modificare le impostazioni di timeout per lo scanner](#change-the-timeout-settings-for-the-scanner)
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
|RunAuditInformationTypesDiscovery|[Disabilitare l'invio di informazioni riservate individuate nei documenti a Azure Information Protection Analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
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

È possibile verificare a quale account è stato eseguito l'accesso usando la finestra di dialogo **Microsoft Azure Information Protection**: Aprire un'applicazione di Office, quindi nel gruppo **Protection** (Protezione) della scheda **Home** fare clic su **Protect** (Proteggi) e quindi fare clic su **Help and feedback** (Guida e commenti e suggerimenti). Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

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

- Key: **ReportAnIssueLink**

- Valore: **\<stringa HTTP>**

Valore di esempio per un sito Web: `https://support.contoso.com`

Valore di esempio per un indirizzo di posta elettronica: `mailto:helpdesk@contoso.com`

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. Se si è conoscenza che i computer in uso non potranno connettersi a Internet per un determinato periodo di tempo, è possibile impedire al client di provare a connettersi al servizio modificando il Registro di sistema. 

Si noti che senza una connessione a Internet, il client non può applicare la protezione (o rimuovere la protezione) usando la chiave basata sul cloud dell'organizzazione. Il client può invece usare esclusivamente le etichette che applicano solo la classificazione o la protezione che usa [HYOK](../configure-adrms-restrictions.md).

È possibile evitare una richiesta di accesso al servizio Azure Information Protection tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che è necessario configurare nel portale di Azure, per poi scaricare i criteri per i computer. In alternativa, è possibile evitare questa richiesta di accesso modificando il Registro di sistema.

- Per configurare l'impostazione client avanzata:
    
    1. Immettere le stringhe seguenti:
    
        - Key: **PullPolicy**
        
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

Se il computer disconnesso esegue la versione corrente di GA dello scanner di Azure Information Protection, è necessario eseguire ulteriori operazioni di configurazione. Per altre informazioni, vedere [Restrizione: il server dello scanner non può avere la connettività Internet](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity) nelle istruzioni per la distribuzione dello scanner.

## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Nascondere o visualizzare il pulsante Non inoltrare in Outlook

Il metodo consigliato per configurare questa opzione è tramite l'[impostazione dei criteri](../configure-policy-settings.md) **Add the Do Not Forward button to the Outlook ribbon** (Aggiungi il pulsante Non inoltrare alla barra multifunzione di Outlook). Tuttavia, è possibile configurare questa opzione anche tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) configurata nel portale di Azure.

Quando è configurata, questa impostazione nasconde o visualizza il pulsante **Non inoltrare** sulla barra multifunzione in Outlook. Questa impostazione non influisce sull'opzione Non inoltrare nei menu di Office.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **DisableDNF**

- Valore: **True** per nascondere il pulsante o **False** per visualizzarlo

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate

Il metodo consigliato per configurare questa opzione è tramite l'[impostazione dei criteri](../configure-policy-settings.md) **Make the custom permissions option available for users** (Rendi disponibile l'opzione per le autorizzazioni personalizzate). Tuttavia, è possibile configurare questa opzione anche tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) configurata nel portale di Azure. 

Quando si configura questa impostazione e si pubblicano i criteri per gli utenti, le opzioni per le autorizzazioni personalizzate diventano visibili per gli utenti in modo che possano selezionare impostazioni di protezione personali oppure sono nascoste e quindi gli utenti non possono selezionare impostazioni di protezione personali, se non richiesto.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **EnableCustomPermissions**

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

- Key: **EnableBarHiding**

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

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Esentare i messaggi di Outlook da un'etichetta obbligatoria

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Per impostazione predefinita, quando si Abilita l' [impostazione dei criteri](../configure-policy-settings.md) **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, a tutti i documenti salvati e ai messaggi di posta elettronica inviati deve essere applicata un'etichetta. Quando si configura l'impostazione avanzata seguente, l'impostazione dei criteri si applica solo ai documenti di Office e non ai messaggi di Outlook.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **DisableMandatoryInOutlook**

- Valore: **True**

## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **OutlookRecommendationEnabled**

- Valore: **True**


## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica

Questa configurazione usa più [impostazioni client avanzate](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che devono essere configurate nel portale di Azure.

Quando si creano e configurano le impostazioni client avanzate seguenti, gli utenti visualizzano messaggi popup di Outlook che possono avvertirli prima dell'invio di un messaggio di posta elettronica, chiedere di giustificare il motivo dell'invio o impedire l'invio di un messaggio di posta elettronica per uno degli scenari seguenti:

- **Il messaggio di posta elettronica o un suo allegato hanno un'etichetta specifica**:
    - L'allegato può essere qualsiasi tipo di file

- **Il messaggio di posta elettronica o l'allegato non hanno un'etichetta**:
    - L'allegato può essere un documento di Office o un documento PDF

Quando vengono soddisfatte queste condizioni, l'utente visualizza un messaggio popup con una delle azioni seguenti:

- **Avvisa**: l'utente può confermare e inviare oppure annullare.

- **Giustifica**: all'utente viene richiesta una giustificazione (opzioni predefinite o formato libero).  L'utente può quindi inviare o annullare il messaggio di posta elettronica. Il testo della giustificazione è scritto nell'intestazione X- del messaggio di posta elettronica in modo da poter essere letto dagli altri sistemi. Ad esempio, servizi di prevenzione della perdita di dati.

- **Blocca**: all'utente viene impedito di inviare il messaggio di posta elettronica finché la condizione persiste. Il messaggio include il motivo del blocco del messaggio di posta elettronica in modo che l'utente possa risolvere il problema, ad esempio rimuovendo destinatari specifici o assegnando un'etichetta al messaggio di posta elettronica. 

Quando i messaggi popup sono per un'etichetta specifica, è possibile configurare le eccezioni per i destinatari in base al nome di dominio.

Le azioni risultanti dai messaggi popup vengono registrate nel registro eventi di Windows locale >  **registri applicazioni e servizi** **Azure Information Protection**:

- Messaggi di avviso: ID informazioni 301

- Messaggi di giustificazione: ID informazioni 302

- Messaggi di blocco: ID informazioni 303

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
Le sezioni seguenti contengono istruzioni di configurazione per ogni impostazione client avanzata, che possono essere visualizzate in azione per se stessi [con l'esercitazione: Configurare Azure Information Protection per controllare la sovracondivisione delle informazioni mediante](../infoprotect-oversharing-tutorial.md)Outlook.

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per etichette specifiche:

Per implementare i messaggi popup per etichette specifiche, è necessario conoscere l'ID etichetta per tali etichette. Il valore dell'ID etichetta è visualizzato nel pannello **Etichetta**, quando si visualizzano o si configurano i criteri di Azure Information Protection nel portale di Azure. Per i file a cui sono state applicate etichette, è anche possibile eseguire il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) per identificare l'ID etichetta (MainLabelId o SubLabelId). Quando un'etichetta ha etichette secondarie, specificare sempre l'ID della sola etichetta secondaria e non dell'etichetta padre.

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

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>Per esentare i nomi di dominio per i messaggi popup configurati per etichette specifiche

Per le etichette specificate con questi messaggi popup, è possibile esentare i nomi di dominio specifici in modo che gli utenti non visualizzino i messaggi per i destinatari che hanno il nome di dominio incluso nell'indirizzo di posta elettronica. In questo caso, i messaggi di posta elettronica vengono inviati senza interruzioni. Per specificare più domini, aggiungerli come stringa singola, delimitata da virgole.

Una configurazione tipica consiste nel rendere visualizzabili i messaggi popup solo dai destinatari che sono esterni all'organizzazione o che non sono partner autorizzati dell'organizzazione. In questo caso, specificare tutti i domini di posta elettronica usati dall'organizzazione e dai partner.

Creare le seguenti impostazioni client avanzate e, per il valore, specificare uno o più domini, ciascuno separato da una virgola.

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

Ad esempio, è stata specificata l'impostazione **OutlookBlockUntrustedCollaborationLabel** Advanced client per l'etichetta **Confidential \ All Employees** . È ora possibile specificare l'impostazione client avanzata aggiuntiva di **OutlookBlockTrustedDomains** e **contoso.com**. Di conseguenza, un utente può inviare un messaggio di posta john@sales.contoso.com elettronica a quando viene etichettato come **riservato \ tutti i dipendenti** , ma l'invio di un messaggio di posta elettronica con la stessa etichetta a un account Gmail verrà bloccato.

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Per implementare i messaggi popup di avviso, giustificazione o blocco per i messaggi di posta elettronica o gli allegati senza etichetta:

Creare l'impostazione client avanzata seguente con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Avvisa**

- Messaggi di giustificazione:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Giustifica**

- Messaggi di blocco:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Bloccato**

- Disattivare questi messaggi:
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Valore: **Off**

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Per definire estensioni di file specifiche per i messaggi popup di avviso, giustificazione o blocco per gli allegati di posta elettronica che non hanno un'etichetta

Per impostazione predefinita, i messaggi popup avvisa, giustifica o blocca si applicano a tutti i documenti di Office e PDF. È possibile affinare questo elenco specificando quali estensioni di file devono visualizzare i messaggi di avviso, di giustificazione o di blocco con una proprietà client avanzata aggiuntiva e un elenco delimitato da virgole di estensioni di file.

Valore di esempio per più estensioni di file da definire come stringa delimitata da virgole:`.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

In questo esempio un documento PDF senza etichetta non comporterà l'avviso, la giustificazione o il blocco dei messaggi popup.


- Key: **OutlookOverrideUnlabeledCollaborationExtensions**

- Valore: **\<** estensioni di file per la visualizzazione dei messaggi, delimitati da virgole **>**

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>Per specificare un'azione diversa per i messaggi di posta elettronica senza allegati

Per impostazione predefinita, il valore specificato per OutlookUnlabeledCollaborationAction per avvisare, giustificare o bloccare i messaggi popup si applica ai messaggi di posta elettronica o agli allegati che non hanno un'etichetta. È possibile perfezionare questa configurazione specificando un'altra impostazione client avanzata per i messaggi di posta elettronica che non dispongono di allegati.

Creare l'impostazione client avanzata seguente con uno dei valori seguenti:

- Messaggi di avviso:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **Avvisa**

- Messaggi di giustificazione:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **Giustifica**

- Messaggi di blocco:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **Bloccato**

- Disattivare questi messaggi:
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valore: **Off**

Se non si specifica questa impostazione client, il valore specificato per OutlookUnlabeledCollaborationAction viene usato per i messaggi di posta elettronica senza etichetta senza allegati, nonché per i messaggi di posta elettronica senza etichetta con allegati.


## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata nei criteri di Azure Information Protection per l'impostazione **Selezionare l'etichetta predefinita**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per applicare un'etichetta diversa, è necessario specificare il relativo ID. Il valore dell'ID etichetta è visualizzato nel pannello **Etichetta**, quando si visualizzano o si configurano i criteri di Azure Information Protection nel portale di Azure. Per i file a cui sono state applicate etichette, è anche possibile eseguire il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) per identificare l'ID etichetta (MainLabelId o SubLabelId). Quando un'etichetta ha etichette secondarie, specificare sempre l'ID della sola etichetta secondaria e non dell'etichetta padre.

Per fare in modo che Outlook non applichi l'etichetta predefinita, specificare **Nessuna**.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **OutlookDefaultLabel**

- Valore: \<**ID etichetta**> o **Nessuna**

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurare un'etichetta per applicare la protezione S/MIME in Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Usare questa impostazione solo se è disponibile una [distribuzione di S/MIME](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption) funzionante e si vuole che un'etichetta applichi automaticamente questo metodo di protezione per i messaggi di posta elettronica anziché la protezione di Rights Management da Azure Information Protection. La protezione risultante è identica a quella applicata quando un utente seleziona manualmente le opzioni di S/MIME da Outlook.

Per questa configurazione è necessario specificare un'impostazione client avanzata denominata **LabelToSMIME** per ogni etichetta di Azure Information Protection a cui si vuole applicare la protezione S/MIME. Per ogni voce impostare quindi il valore usando la sintassi seguente:

`[Azure Information Protection label ID];[S/MIME action]`

Il valore dell'ID etichetta è visualizzato nel pannello **Etichetta**, quando si visualizzano o si configurano i criteri di Azure Information Protection nel portale di Azure. Per usare S/MIME con un'etichetta secondaria, è necessario specificare sempre l'ID solo dell'etichetta secondaria e non dell'etichetta padre. Quando si specifica un'etichetta secondaria, l'etichetta padre deve essere nello stesso ambito o nei criteri globali.

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

Se si vuole che l'etichetta sia visibile solo in Outlook, configurare l'etichetta per applicare la singola azione definita dall'utente **Non inoltrare**, come descritto in [Avvio rapido: Configurare un'etichetta che consente di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate](../quickstart-label-dnf-protectedemail.md).

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Se si usa l'[impostazione dei criteri](../configure-policy-settings.md) **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**, agli utenti viene richiesto di selezionare un'etichetta quando salvano per la prima volta un documento di Office e quando inviano un messaggio di posta elettronica. Per i documenti, gli utenti possono selezionare **Non ora** per chiudere temporaneamente la richiesta di selezionare un'etichetta e tornare al documento. Non possono però chiudere il documento salvato senza etichettarlo. 

Quando si configura questa impostazione l'opzione **Non ora** viene rimossa. In questo modo, quando il documento viene salvato per la prima volta gli utenti sono obbligati a selezionare un'etichetta.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **PostponeMandatoryBeforeSave**

- Valore: **False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>Attivare l'esecuzione continua della classificazione in background

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Quando si configura questa impostazione, cambia il [comportamento predefinito](../configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) del client Azure Information Protection rispetto all'applicazione delle etichette automatiche e consigliate ai documenti: 

- Per Word, Excel e PowerPoint, la classificazione automatica viene eseguita in modo continuo in background.  

Il comportamento rimane invariato per Outlook.

Quando il client di Azure Information Protection verifica periodicamente nei documenti le regole di condizione specificate, questo comportamento abilita la classificazione automatica e consigliata e la protezione dei documenti archiviati in SharePoint Online. I file di grandi dimensioni vengono salvati più rapidamente perché le regole di condizione sono già state eseguite. 

Le regole di condizione non vengono eseguite in tempo reale durante la digitazione. Vengono eseguite periodicamente come attività in background se il documento viene modificato.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Key: **RunPolicyInBackground**

- Valore: **True**

## <a name="dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>Non proteggere i file PDF usando lo standard ISO per la crittografia dei file PDF

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando un file PDF è protetto con l'ultima versione del client Azure Information Protection, l'estensione risultante rimane pdf ed è conforme allo standard ISO per la crittografia dei file PDF. Per altre informazioni su questo standard, vedere la sezione **7.6 Encryption** (Crittografia) del [documento derivato dalla specifica ISO 32000-1](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf) e pubblicato da Adobe Systems Incorporated.

Se è necessario che il client ripristini il comportamento delle versioni precedenti, ovvero protezione dei file PDF con un'estensione di file ppdf, usare l'impostazione avanzata seguente immettendo questa stringa:

- Key: **EnablePDFv2Protection**

- Valore: **False**

Questa impostazione, ad esempio, può essere necessaria per tutti gli utenti se si usa un lettore di file PDF che non supporta lo standard ISO per la crittografia dei file PDF. Oppure può essere necessario configurare questa impostazione per alcuni utenti durante l'introduzione graduale di un lettore di file PDF che supporta il nuovo formato. Un altro possibile motivo per l'uso di questa impostazione è la necessità di aggiungere protezione a documenti PDF firmati. È possibile aggiungere ulteriore protezione ai documenti PDF con il formato con estensione ppdf, poiché questa protezione viene implementata come wrapper per i file. 

Per fare in modo che lo scanner Azure Information Protection usi la nuova impostazione, è necessario riavviare il servizio scanner. Inoltre, lo scanner non proteggerà più i documenti PDF per impostazione predefinita. Se si vuole che i documenti PDF siano protetti dallo scanner quando EnablePDFv2Protection è impostata su False, è necessario [modificare il Registro di sistema](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner).

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
    
     Nota: se non è presente neanche un valore per **MainLabelId**, il file non ha etichetta. In questo caso è possibile usare i comandi [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) e [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) invece dei comandi nei passaggi 3 e 4.
    
   - Valore di **RMSTemplateId**. Se questo valore è **Accesso limitato**, un utente ha protetto il file usando autorizzazioni personalizzate anziché le impostazioni di protezione configurate per l'etichetta. Se si continua, tali autorizzazioni personalizzate verranno sovrascritte dalle impostazioni di protezione dell'etichetta. Decidere se continuare o chiedere all'utente (valore visualizzato per **RMSIssuer**) di rimuovere l'etichetta e riapplicarla, con le relative autorizzazioni personalizzate originali.

3. Rimuovere l'etichetta usando [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) con il parametro *RemoveLabel*. Se si usa l'[impostazione criteri](../configure-policy-settings.md) **Gli utenti devono offrire una giustificazione per la configurazione di un'etichetta di classificazione più bassa, la rimozione di un'etichetta o la rimozione della protezione**, è necessario specificare anche il parametro *Giustificazione* con il motivo. Ad esempio: 
    
        Set-AIPFileLabel \\Finance\Projectx\sales.ppdf -RemoveLabel -JustificationMessage 'Removing .ppdf protection to replace with .pdf ISO standard'

4. Riapplicare l'etichetta originale, specificando il valore dell'etichetta identificato nel passaggio 1. Ad esempio:
    
        Set-AIPFileLabel \\Finance\Projectx\sales.pdf -LabelId d9f23ae3-1234-1234-1234-f515f824c57b

Il file mantiene l'estensione pdf ma viene classificato come in precedenza ed è protetto tramite lo standard ISO per la crittografia PDF.

## <a name="support-for-files-protected-by-secure-islands"></a>Supporto di file protetti da Secure Islands

Questa opzione di configurazione è in anteprima e potrebbe cambiare.

Se è stato usato Secure Islands è possibile che siano stati protetti file di testo, file immagine e file generici. Sono esempi i file con estensione ptxt, pjpeg o pfile. Quando si modifica il registro di sistema come indicato di seguito, Azure Information Protection può decrittografare questi file:


Aggiungere il seguente valore DWORD di **EnableIQPFormats** al percorso del registro seguente e impostare i dati del valore su **1**:

- Per una versione a 64 bit di Windows: HKEY_LOCAL_MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\MSIP

- Per una versione a 32 bit di Windows: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\MSIP

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

Il valore dell'ID etichetta è visualizzato nel pannello **Etichetta**, quando si visualizzano o si configurano i criteri di Azure Information Protection nel portale di Azure. Per specificare un'etichetta secondaria, l'etichetta padre deve essere nello stesso ambito o nei criteri globali.

Specificare un nome di regola di migrazione a propria scelta. Usare un nome descrittivo che consente di identificare come deve essere eseguito il mapping di una o più etichette dalla soluzione precedente imprevisto a un'etichetta di Azure Information Protection. Il nome viene visualizzato nei report dello scanner e nel Visualizzatore eventi. Si noti che questa impostazione non comporta la rimozione dell'etichetta originale dal documento o di tutti i contrassegni visivi nel documento che l'etichetta originale potrebbe aver applicato. Per rimuovere le intestazioni e i piè di pagina, vedere la sezione successiva [Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions).

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta

Requisito: I documenti con l'etichetta di Secure Islands "Riservato" devono essere rietichettati come "Riservato" da Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection da usare è **Riservato** e ha l'ID etichetta **1ace2cc3-14bc-4142-9125-bf946a70542c**. 

- L'etichetta di Secure Islands è **Riservato** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Valore|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c, "L'etichetta Secure Islands è Riservato",Classificazione,Riservato|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Esempio 2: Mapping uno-a-uno per un altro nome di etichetta

Requisito: I documenti con l'etichetta di Secure Islands "Sensibile" devono essere rietichettati come "Riservatezza elevata" da Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection da usare è **Riservatezza elevata** e ha l'ID etichetta **3e9df74d-3168-48af-8b11-037e3021813f**.

- L'etichetta di Secure Islands è **Sensibile** ed è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Valore|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f, "L'etichetta Secure Islands è Sensibile",Classificazione,Sensibile|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>Esempio 3: Mapping molti-a-uno di nomi di etichetta

Requisito: Sono disponibili due etichette di Secure Islands che includono la parola "Interno" e si vuole che i documenti con queste etichette di Secure Islands vengano rietichettati come "Generale" da Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection da usare è **Generale** e ha l'ID etichetta **2beb8fe7-8293-444c-9768-7fdc6f75014d**.

- Le etichette di Secure Islands includono la parola **Interno** e sono archiviate nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Valore|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d,"L'etichetta Secure Islands contiene Interno",Classificazione,.\*Interno.\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette

Questa configurazione usa più [impostazioni client avanzate](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che devono essere configurate nel portale di Azure. Queste impostazioni sono di anteprima e potrebbero cambiare.

Le impostazioni consentono di rimuovere o sostituire le intestazioni o i piè di pagina basati su testo nei documenti, quando questi contrassegni visivi sono stati applicati da un'altra soluzione di etichettatura. Ad esempio, il piè di pagina precedente contiene il nome di un'etichetta precedente di cui è stata eseguita la migrazione ad Azure Information Protection con un nuovo nome di etichetta e un proprio piè di pagina.

Quando il client ottiene questa configurazione nei relativi criteri, le intestazioni e i piè di pagina precedenti vengono rimossi o sostituiti quando il documento viene aperto nell'app di Office e al documento vengono applicate le etichette di Azure Information Protection.

Questa configurazione non è supportata per Outlook e tenere presente che quando viene usata con Word, Excel e PowerPoint, può influire negativamente sulle prestazioni di queste app per gli utenti. La configurazione consente di definire le impostazioni per ogni applicazione, ad esempio la ricerca di testo nelle intestazioni e nei piè di pagina di documenti di Word, ma non nei fogli di calcolo di Excel o nelle presentazioni di PowerPoint.

Poiché i criteri di ricerca influiscono sulle prestazioni per gli utenti, è consigliabile limitare i tipi di applicazioni di Office (**W**ord, **E**xcel, **P**owerPoint) solo a quelli in cui deve essere eseguita la ricerca:

- Key: **RemoveExternalContentMarkingInApp**

- Valore: \<**tipi di applicazioni di Office WXP**> 

Esempi:

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

- Key: **ExternalContentMarkingToRemove**

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

- Key: **PowerPointShapeNameToRemove**

- Valore: \<**nome delle forma di PowerPoint**> 

Quando si hanno più forme di PowerPoint da rimuovere, creare tante chiavi **PowerPointShapeNameToRemove** quante sono le forme da rimuovere. Per ogni voce specificare il nome della forma da rimuovere.

Per impostazione predefinita, il testo delle intestazioni e dei piè di pagina viene cercato solo negli schemi diapositiva. Per estendere la ricerca a tutte le diapositive, che è un processo con un utilizzo maggiore di risorse, usare un'impostazione client avanzata aggiuntiva denominata **RemoveExternalContentMarkingInAllSlides**:

- Key: **RemoveExternalContentMarkingInAllSlides**

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

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Disabilitare l'invio di informazioni riservate individuate nei documenti a Azure Information Protection Analytics

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Quando il client Azure Information Protection viene usato nelle app di Office, Cerca informazioni riservate nei documenti quando vengono salvate per la prima volta. Se si specifica che il client non è configurato per l'invio di informazioni di controllo, i tipi di informazioni riservate trovate (predefinite o personalizzate) vengono quindi inviati a [Azure Information Protection Analytics](../reports-aip.md).

Per modificare questo comportamento in modo che i tipi di informazioni riservate rilevati dal client classico non vengano inviati a Azure Information Protection Analytics, immettere le stringhe seguenti:

- Key: **RunAuditInformationTypesDiscovery**

- Valore: **False**

Se si imposta questa impostazione client avanzata, i risultati di controllo possono comunque essere inviati dal client, ma le informazioni sono limitate alla segnalazione quando un utente ha eseguito l'accesso al contenuto con etichetta.

Ad esempio:

- Con questa impostazione è possibile vedere che un utente ha eseguito l'accesso a Financial. docx con etichetta **Confidential \ Sales**.

- Senza questa impostazione, è possibile notare che Financial. docx contiene 6 numeri di carta di credito.
    
    - Se si abilita [l'analisi più approfondita nei dati sensibili](../reports-aip.md#content-matches-for-deeper-analysis), sarà possibile vedere anche quali sono i numeri di carta di credito.

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>Disabilitare l'invio delle corrispondenze per i tipi di informazioni per un subset di utenti

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Quando si seleziona la casella di controllo [Azure Information Protection Analytics](../reports-aip.md) che Abilita l'analisi più approfondita nei dati sensibili raccoglie le corrispondenze di contenuto per i tipi di informazioni riservate o le condizioni personalizzate, per impostazione predefinita, queste informazioni sono Inviato da tutti gli utenti, inclusi gli account del servizio che eseguono lo scanner Azure Information Protection. In presenza di utenti che non devono inviare questi dati, creare l'impostazione client avanzata seguente in un [criterio con ambito](../configure-policy-scope.md) per questi utenti: 

- Key: **LogMatchedContent**

- Valore: **Disabilitare**


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

- Key: **ProcessUsingLowIntegrity**

- Valore: **False**

## <a name="change-the-timeout-settings-for-the-scanner"></a>Modificare le impostazioni di timeout per lo scanner

Questa configurazione USA [Impostazioni client avanzate](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che è necessario configurare nel portale di Azure.

Per impostazione predefinita, lo scanner Azure Information Protection ha un periodo di timeout di 00:15:00 (15 minuti) per esaminare ogni file per i tipi di informazioni riservate o per le espressioni Regex configurate per le condizioni personalizzate. Quando viene raggiunto il periodo di timeout per questo processo di estrazione del contenuto, vengono restituiti tutti i risultati prima del timeout e l'ulteriore ispezione del file viene arrestata. In questo scenario, il messaggio di errore seguente viene registrato in%*LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog (compresso se sono presenti più log): **GetContentParts non riuscito** con **l'operazione** annullata nei dettagli.

Se si verifica questo problema di timeout a causa di file di grandi dimensioni, è possibile aumentare questo periodo di timeout per l'estrazione del contenuto completo:

- Key: **ContentExtractionTimeout**

- Valore:  **\<HH: min: sec >**

Il tipo di file può influire sul tempo necessario per eseguire la scansione di un file. Tempi di analisi di esempio:

- Un file di Word 100 MB tipico: 0,5-5 minuti

- Un file PDF tipico di 100 MB: 5-20 minuti

- Un file di Excel di 100 MB tipico: 12-30 minuti

Per alcuni tipi di file di dimensioni molto elevate, ad esempio file video, è consigliabile escluderli dall'analisi aggiungendo l'estensione del nome di file all'opzione **tipi di file da analizzare** nel profilo dello scanner.

Inoltre, lo scanner Azure Information Protection ha un periodo di timeout di 00:30:00 (30 minuti) per ogni file elaborato. Questo valore prende in considerazione il tempo richiesto per recuperare un file da un repository e salvarlo temporaneamente localmente per le azioni che possono includere la decrittografia, l'estrazione del contenuto per l'ispezione, l'assegnazione di etichette e la crittografia.

Sebbene lo scanner di Azure Information Protection possa analizzare dozzine di centinaia di file al minuto, se si dispone di un repository di dati con un numero elevato di file di grandi dimensioni, lo scanner può superare questo periodo di timeout predefinito e, nel portale di Azure, sembra arrestarsi dopo 30 minuti. In questo scenario, il seguente messaggio di errore viene registrato in%*LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog (compresso se sono presenti più log) e il file di log scanner. csv: **L'operazione è stata**annullata.

Uno scanner con 4 processori core per impostazione predefinita dispone di 16 thread per l'analisi e la probabilità che si verifichino 16 file di grandi dimensioni in un periodo di tempo di 30 minuti dipende dal rapporto dei file di grandi dimensioni. Se, ad esempio, la frequenza di analisi è di 200 file al minuto e l'1% dei file supera il timeout di 30 minuti, esiste una probabilità superiore al 85% che lo scanner rileverà la situazione di timeout di 30 minuti. Questi timeout possono causare tempi di analisi più lunghi e un maggiore consumo di memoria.

In questa situazione, se non è possibile aggiungere più processori di base al computer dello scanner, provare a ridurre il periodo di timeout per ottenere una migliore frequenza di analisi e ridurre il consumo di memoria, ma con il riconoscimento che alcuni file verranno esclusi. In alternativa, provare ad aumentare il periodo di timeout per ottenere risultati di analisi più accurati, ma con il riconoscimento che questa configurazione comporterà probabilmente una riduzione delle frequenze di analisi e un maggiore consumo di memoria.

Per modificare il periodo di timeout per l'elaborazione dei file, configurare l'impostazione client avanzata seguente:

- Key: **FileProcessingTimeout**

- Valore:  **\<HH: min: sec >**

## <a name="change-the-local-logging-level"></a>Modificare il livello di registrazione locale

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Per impostazione predefinita, il client Azure Information Protection scrive i file di log del client nella cartella **%localappdata%\Microsoft\MSIP**. Questi file sono destinati al supporto tecnico Microsoft per la risoluzione dei problemi.
 
Per modificare il livello di registrazione per questi file, configurare l'impostazione client avanzata seguente:

- Key: **LogLevel**

- Valore: **\<livello di registrazione>**

Impostare il livello di registrazione su uno dei valori seguenti:

- **Off**: nessuna registrazione locale.

- **Errore**: solo errori.

- **Info**: Registrazione minima, che non include gli ID evento (impostazione predefinita per lo scanner).

- **Debug**: Informazioni complete.

- **Traccia**: Registrazione dettagliata (impostazione predefinita per i client). Per lo scanner, questa impostazione ha un impatto significativo sulle prestazioni e deve essere abilitata solo se richiesto dal supporto tecnico Microsoft. Se viene richiesto di impostare questo livello di registrazione per lo scanner, ricordarsi di impostare un valore diverso dopo aver raccolto i log rilevanti.

Questa impostazione client avanzata non modifica le informazioni inviate ad Azure Information Protection per [reporting centralizzato](../reports-aip.md) o le informazioni scritte nel [registro eventi](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) locale.

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Integrazione con la classificazione dei messaggi di Exchange per una soluzione di etichettatura dei dispositivi mobili

Benché Outlook sul Web non supporti ancora in modo nativo la protezione e la classificazione di Azure Information Protection, è possibile usare la classificazione dei messaggi di Exchange per estendere le etichette di Azure Information Protection agli utenti dei dispositivi mobili quando usano Outlook sul Web. Outlook Mobile non supporta la classificazione dei messaggi di Exchange.

Per ottenere questa soluzione: 

1. Usare il cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) di Exchange PowerShell per creare le classificazioni dei messaggi con la proprietà Name che esegue il mapping ai nomi di etichetta nei criteri di Azure Information Protection. 

2. Creare una regola del flusso di posta di Exchange per ogni etichetta: applicare la regola quando le proprietà del messaggio includono la classificazione configurata e modificare le proprietà del messaggio per impostare un'intestazione del messaggio. 

     Per l'intestazione del messaggio, è possibile trovare le informazioni da specificare nelle intestazioni Internet di un messaggio di posta elettronica inviato e classificato tramite l'etichetta di Azure Information Protection. Cercare l'intestazione **msip_labels** e la stringa immediatamente successiva fino al punto e virgola incluso. Ad esempio:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Quindi, per l'intestazione del messaggio nella regola, specificare **msip_labels** per l'intestazione e la parte rimanente della stringa per il valore dell'intestazione. Ad esempio:
    
    ![Regola del flusso di posta di Exchange Online di esempio che imposta l'intestazione del messaggio per un'etichetta di Azure Information Protection specifica](../media/exchange-rule-for-message-header.png)
    
    Nota: quando l'etichetta è un'etichetta secondaria, è necessario specificare anche l'etichetta padre prima dell'etichetta secondaria nel valore di intestazione, usando lo stesso formato. Ad esempio, se il GUID dell'etichetta secondaria è 27efdf94-80a0-4d02-b88c-b615c12d69a9, il valore potrebbe essere simile al seguente: `MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True;`

Prima di eseguire il test della configurazione, tenere presente che spesso si verifica un ritardo quando vengono create o modificate le regole del flusso di posta. Ad esempio, può essere necessario attendere un'ora. Se la regola è attiva, quando gli utenti usano Outlook sul Web, si verificano gli eventi seguenti: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Se i destinatari interni visualizzano il messaggio di posta elettronica in Outlook e hanno installato il client di Azure Information Protection, vedono l'etichetta di Azure Information Protection assegnata. 

Se le etichette di Azure Information Protection applicano la protezione, aggiungerla alla configurazione della regola: Selezionando l'opzione per la modifica della protezione dei messaggi, applicare la protezione dei diritti e quindi selezionare il modello di protezione o l'opzione Non inoltrare.

È anche possibile configurare regole del flusso di posta per eseguire il mapping inverso. Quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente:

- Per ogni etichetta di Azure Information Protection: creare una regola del flusso di posta da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **General**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver personalizzato il client di Azure Information Protection, vedere le risorse seguenti per altre informazioni eventualmente necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


