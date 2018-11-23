---
title: Configurazioni personalizzate per il client Azure Information Protection
description: Informazioni sulla personalizzazione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/06/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 4d3a44426de151ad9d1f1262cae967fdddf0da6f
ms.sourcegitcommit: 520c8758c46ab46427fe205234bb221688ec9ec4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2018
ms.locfileid: "52292593"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client di Azure Information Protection.

Alcune di queste impostazioni richiedono la modifica del Registro di sistema e alcune usano impostazioni avanzate che è necessario configurare nel Portale di Azure e quindi pubblicare perché i client possano scaricarle.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Come configurare le impostazioni avanzate di configurazione del client nel portale

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](../configure-policy.md#signing-in-to-the-azure-portal) e quindi passare al pannello **Azure Information Protection**.

2. Dall'opzione di menu **Classificazioni** > **Etichette**: selezionare **Criteri**.

3. Nel pannello **Azure Information Protection - Criteri** selezionare il menu di scelta rapida (**...**) accanto ai criteri, contenente le impostazioni avanzate. Selezionare quindi **Impostazioni avanzate**.
    
    È possibile configurare le impostazioni avanzate per i criteri globali e per i criteri con ambito.

4. Nel pannello **Impostazioni avanzate** digitare il nome e il valore dell'impostazione avanzata e quindi selezionare **Salva e chiudi**.

5. Assicurarsi che gli utenti interessati da questi criteri riavviino le applicazioni di Office eventualmente aperte.

6. Se l'impostazione non è più necessaria e si vuole ripristinare il comportamento predefinito, nel pannello **Impostazioni avanzate** selezionare il menu di scelta rapida (**...**) accanto all'impostazione non più necessaria e quindi selezionare **Elimina**. Fare clic su **Salva e chiudi**.

#### <a name="available-advanced-client-settings"></a>Impostazioni client avanzate disponibili

|Impostazione|Scenario e istruzioni|
|----------------|---------------|
|DisableDNF|[Nascondere o visualizzare il pulsante Non inoltrare in Outlook](#hide-or-show-the-do-not-forward-button-in-outlook)|
|EnableBarHiding|[Nascondere in modo permanente la barra di Azure Information Protection](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnablePDFv2Protection|[Proteggere i file PDF usando lo standard ISO per la crittografia PDF](#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|LabelbyCustomProperty|[Eseguire la migrazione di etichette da Secure Islands e altre soluzioni per l'assegnazione di etichette](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|OutlookDefaultLabel|[Impostare un'etichetta predefinita diversa per Outlook](#set-a-different-default-label-for-outlook)|
|OutlookRecommendationEnabled|[Abilitare la classificazione consigliata in Outlook](#enable-recommended-classification-in-outlook)|
|PostponeMandatoryBeforeSave|[Rimuovere "Non ora" per i documenti quando si usa l'etichettatura obbligatoria](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|ProcessUsingLowIntegrity|[Disabilitare il livello di integrità basso per lo scanner](#disable-the-low-integrity-level-for-the-scanner)|
|RemoveExternalContentMarkingInApp|[Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Modificare l'indirizzo di posta elettronica per il collegamento Segnala un problema](#modify-the-email-address-for-the-report-an-issue-link)|
|RunPolicyInBackground|[Attivare l'esecuzione continua della classificazione in background](#turn-on-classification-to-run-continuously-in-the-background)|
|SyncPropertyName|[Etichettare un documento di Office usando una proprietà personalizzata esistente](#label-an-office-document-by-using-an-existing-custom-property)|
|SyncPropertyState|[Etichettare un documento di Office usando una proprietà personalizzata esistente](#label-an-office-document-by-using-an-existing-custom-property)|

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitare le richieste di accesso per i computer solo AD RMS

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection. Per i computer che comunicano solo con AD RMS questa configurazione può comportare una richiesta di accesso non necessaria per gli utenti. È possibile evitare questa richiesta di accesso modificando il Registro di sistema:

Individuare il nome di valore seguente e quindi impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indipendentemente da questa impostazione, il client Azure Information Protection segue il normale [processo di individuazione del servizio RMS](client-deployment-notes.md#rms-service-discovery) per trovare il proprio cluster AD RMS.

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

## <a name="modify-the-email-address-for-the-report-an-issue-link"></a>Modificare l'indirizzo di posta elettronica per il collegamento Segnala un problema

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è applicabile solo alle versioni di anteprima del client Azure Information Protection, perché le versioni di disponibilità generale del client non visualizzano il collegamento **Segnala un problema**.

Quando gli utenti selezionano il collegamento **Segnala un problema** nella finestra di dialogo **Guida e commenti** delle versioni precedenti del client, per impostazione predefinita viene visualizzato un messaggio di posta elettronica con un indirizzo Microsoft. Per modificare questo indirizzo, usare l'impostazione del client avanzata seguente. Ad esempio, specificare `mailto:helpdesk@contoso.com` per l'indirizzo di posta elettronica dell'help desk. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **ReportAnIssueLink**

- Valore: **\<stringa HTTP>**

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. Se si è conoscenza che i computer in uso non potranno connettersi a Internet per un determinato periodo di tempo, è possibile impedire al client di provare a connettersi al servizio modificando il Registro di sistema. 

Si noti che senza una connessione a Internet, il client non può applicare la protezione (o rimuovere la protezione) usando la chiave basata sul cloud dell'organizzazione. Il client può invece usare esclusivamente le etichette che applicano solo la classificazione o la protezione che usa [HYOK](../configure-adrms-restrictions.md).

Per configurare questa impostazione, trovare il nome del valore seguente nel Registro di sistema e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Verificare che nel client sia presente un file di criteri validi denominato **Policy.msip**, nella cartella **%LocalAppData%\Microsoft\MSIP**. Se necessario, è possibile esportare i criteri globali o i criteri con ambito dal portale di Azure e copiare il file esportato nel computer client. È anche possibile usare questo metodo per sostituire un file di criteri non aggiornato con i criteri pubblicati più recenti. Esportare i criteri, tuttavia, non supporta lo scenario in cui un utente appartiene a più di un criterio con ambito. Tenere anche presente che se gli utenti selezionano l'opzione **Ripristina le impostazioni** in [Guida e commenti](client-admin-guide.md#help-and-feedback-section), questa azione elimina il file dei criteri e rende il client inutilizzabile fino a quando non si sostituisce manualmente il file dei criteri o il client si connette al servizio per scaricare i criteri.

Quando si esportano i criteri dal portale di Azure, viene scaricato un file ZIP che contiene più versioni dei criteri. Queste versioni dei criteri corrispondono a versioni diverse del client Azure Information Protection:

1. Decomprimere il file e usare la tabella seguente per identificare il file di criteri necessario. 
    
    |Nome file|Versione del client corrispondente|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |versione 1.2|
    |Policy1.2.msip |versione 1.3 - 1.7|
    |Policy1.3.msip |versione 1.8 - 1.29|
    |Policy1.4.msip |versione 1.32 e successive|
    
2. Rinominare il file identificato come **Policy.msip**, quindi copiarlo nella cartella **%LocalAppData%\Microsoft\MSIP** nei computer in cui è installato il client Azure Information Protection. 


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


## <a name="permanently-hide-the-azure-information-protection-bar"></a>Nascondere in modo permanente la barra di Azure Information Protection

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Usarla solo quando l'[impostazione dei criteri](../configure-policy-settings.md) **Display the Information Protection bar in Office apps** (Visualizza la barra di Information Protection nelle app di Office) è impostata su **On** (Attiva).

Quando si configura questa impostazione, si pubblicano i criteri per gli utenti e un utente sceglie di non visualizzare la barra di Azure Information Protection nelle applicazioni di Office, la barra rimane nascosta. Ciò si verifica se l'utente deseleziona l'opzione **Mostra barra**: nella scheda **Home**, nel gruppo **Protezione**, fare clic sul pulsante **Proteggi**. Questa impostazione non ha alcun effetto se l'utente chiude la barra tramite l'icona **Chiudi questa barra**.

Anche se la barra di Azure Information Protection rimane nascosta, gli utenti possono visualizzarla temporaneamente per selezionare un'etichetta, se è stata configurata la classificazione consigliata o se un documento o un messaggio di posta elettronica deve avere un'etichetta. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableBarHiding**

- Valore: **True**


## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **OutlookRecommendationEnabled**

- Valore: **True**


## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata nei criteri di Azure Information Protection per l'impostazione **Selezionare l'etichetta predefinita**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per applicare un'etichetta diversa, è necessario specificare il relativo ID. Il valore dell'ID etichetta è visualizzato nel pannello **Etichetta**, quando si visualizzano o si configurano i criteri di Azure Information Protection nel portale di Azure. Per i file a cui sono state applicate etichette, è anche possibile eseguire il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) per identificare l'ID etichetta (MainLabelId o SubLabelId). Quando un'etichetta ha etichette secondarie, specificare sempre l'ID della sola etichetta secondaria e non dell'etichetta padre.

Per fare in modo che Outlook non applichi l'etichetta predefinita, specificare **Nessuna**.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **OutlookDefaultLabel**

- Valore: \<**ID etichetta**> o **Nessuna**

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

## <a name="protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>Protect PDF files by using the ISO standard for PDF encryption (Proteggere i file PDF usando lo standard ISO per la crittografia PDF)

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Per impostazione predefinita, quando il client Azure Information Protection protegge un file PDF, il file risultante ha l'estensione ppdf. È possibile modificare questo comportamento in modo che l'estensione rimanga pdf e che l'operazione sia conforme allo standard ISO per la crittografia dei file PDF. Per altre informazioni su questo standard, vedere la sezione **7.6 Encryption** (Crittografia) del [documento derivato dalla specifica ISO 32000-1](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf) e pubblicato da Adobe Systems Incorporated.

Per configurare questa impostazione avanzata, immettere la stringa seguente:

- Chiave: **EnablePDFv2Protection**

- Valore: **True**

Come risultato di questa opzione di configurazione, quando il client Azure Information Protection protegge un file PDF, questa azione crea un documento PDF protetto che può essere aperto con la versione più recente del client Azure Information Protection per Windows e con altri lettori PDF che supportano lo standard ISO per la crittografia PDF. L'app Azure Information Protection per iOS e Android non supporta attualmente lo standard ISO per la crittografia dei file PDF. Per informazioni aggiornate su Adobe Acrobat Reader, vedere [Starting October, use Adobe Acrobat Reader for PDFs protected by Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738) (A partire da ottobre è possibile usare Adobe Acrobat Reader per i PDF protetti da Microsoft Information Protection).

Per fare in modo che lo scanner Azure Information Protection usi la nuova impostazione, è necessario riavviare il servizio scanner.

Per altre informazioni sulla crittografia PDF, vedere il post del blog [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nuovo supporto della crittografia PDF con Microsoft Azure Information Protection).

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

Questa opzione di configurazione è attualmente in anteprima ed è soggetta a modifiche.

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

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione è in anteprima e potrebbe cambiare.

Questa configurazione non è attualmente compatibile con l'impostazione [Protect PDF files by using the ISO standard for PDF encryption](client-admin-guide-customizations.md#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption) (Proteggere i file PDF usando lo standard ISO per la crittografia PDF). Quando si usano entrambe le impostazioni insieme, non è possibile aprire i file con estensione ppdf tramite Esplora file, PowerShell o lo scanner.

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

Specificare un nome di regola di migrazione a propria scelta. Usare un nome descrittivo che consente di identificare come deve essere eseguito il mapping di una o più etichette dalla soluzione precedente imprevisto a un'etichetta di Azure Information Protection. Il nome viene visualizzato nei report dello scanner e nel Visualizzatore eventi. 

Tenere presente che questa impostazione non rimuove tutti i contrassegni visivi che potrebbero essere stati applicati dall'etichetta precedente. Per rimuovere le intestazioni e i piè di pagina, vedere la sezione successiva [Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette](#remove-headers-and-footers-from-other-labeling-solutions).

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Esempio 1: Mapping uno-a-uno con lo stesso nome di etichetta

I documenti con l'etichetta di Secure Islands "Riservato" devono essere rietichettati come "Riservato" da Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection **Riservato** ha l'ID etichetta 1ace2cc3-14bc-4142-9125-bf946a70542c. 

- L'etichetta di Secure Islands è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Valore|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c, "L'etichetta Secure Islands è Riservato",Classificazione,Riservato|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Esempio 2: Mapping uno-a-uno per un altro nome di etichetta

I documenti con l'etichetta di Secure Islands "Sensibile" devono essere rietichettati come "Riservatezza elevata" da Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection **Riservatezza elevata** ha l'ID etichetta 3e9df74d-3168-48af-8b11-037e3021813f.

- L'etichetta di Secure Islands è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Valore|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f, "L'etichetta Secure Islands è Sensibile",Classificazione,Sensibile|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>Esempio 3: Mapping molti-a-uno di nomi di etichetta

Sono disponibili due etichette di Secure Islands che includono la parola "Interno" e si vuole che i documenti con queste etichette di Secure Islands vengano rietichettati come "Generale" da Azure Information Protection.

In questo esempio:

- L'etichetta di Azure Information Protection **Generale** ha l'ID etichetta 2beb8fe7-8293-444c-9768-7fdc6f75014d.

- L'etichetta di Secure Islands è archiviata nella proprietà personalizzata denominata **Classificazione**.

L'impostazione client avanzata è la seguente:

    
|Name|Valore|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d,"L'etichetta Secure Islands contiene Interno",Classificazione,.\*Interno.\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Rimuovere intestazioni e piè di pagina da altre soluzioni di assegnazione etichette

Questa configurazione usa più [impostazioni client avanzate](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che devono essere configurate nel portale di Azure. Queste impostazioni sono di anteprima e potrebbero cambiare.

Le impostazioni consentono di rimuovere o sostituire le intestazioni o i piè di pagina dai documenti quando questi contrassegni visivi sono stati applicati da un'altra soluzione di assegnazione etichette. Ad esempio, il piè di pagina precedente contiene il nome di un'etichetta precedente di cui è stata eseguita la migrazione ad Azure Information Protection con un nuovo nome di etichetta e un proprio piè di pagina.

Quando il client ottiene questa configurazione nei relativi criteri, le intestazioni e i piè di pagina precedenti vengono rimossi o sostituiti quando il documento viene aperto nell'app di Office e al documento vengono applicate le etichette di Azure Information Protection.

Questa configurazione non è supportata per Outlook e tenere presente che quando viene usata con Word, Excel e PowerPoint, può influire negativamente sulle prestazioni di queste app per gli utenti. La configurazione consente di definire le impostazioni per ogni applicazione, ad esempio la ricerca di testo nelle intestazioni e nei piè di pagina di documenti di Word, ma non nei fogli di calcolo di Excel o nelle presentazioni di PowerPoint.

Poiché i criteri di ricerca influiscono sulle prestazioni per gli utenti, è consigliabile limitare i tipi di applicazioni di Office (**W**ord, **E**xcel, **P**owerPoint) solo a quelli in cui deve essere eseguita la ricerca:

- Chiave: **RemoveExternalContentMarkingInApp**

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

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>Disabilitare il livello di integrità basso per lo scanner

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Per impostazione predefinita, lo scanner di Azure Information Protection viene eseguito con un livello di integrità basso. Questa impostazione offre un maggiore isolamento di sicurezza, ma influisce negativamente sulle prestazioni. Il livello di integrità basso è appropriato se si esegue lo scanner con un account con privilegi (ad esempio un account amministratore locale) in quanto questa impostazione aiuta a proteggere il computer che esegue lo scanner.

Quando, tuttavia, l'account del servizio che esegue lo scanner ha solo i diritti indicati nei [prerequisiti dello scanner](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), il livello di integrità basso non è necessario e non è consigliato perché influisce negativamente sulle prestazioni. 

Per altre informazioni sui livelli di integrità di Windows, vedere [What is the Windows Integrity Mechanism?](https://msdn.microsoft.com/library/bb625957.aspx) (Informazioni sul meccanismo di integrità di Windows)

Per configurare questa impostazione avanzata in modo che lo scanner venga eseguito con un livello di integrità assegnato automaticamente da Windows (un account utente standard viene eseguito con un livello di integrità medio), immettere le stringhe seguenti:

- Chiave: **ProcessUsingLowIntegrity**

- Valore: **False**


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

Prima di eseguire il test della configurazione, tenere presente che spesso si verifica un ritardo quando vengono create o modificate le regole del flusso di posta. Ad esempio, può essere necessario attendere un'ora. Se la regola è attiva, quando gli utenti usano Outlook sul Web o un client per dispositivi mobili che supportaExchange ActiveSync IRM, si verificano gli eventi seguenti: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Se i destinatari interni visualizzano il messaggio di posta elettronica in Outlook e hanno installato il client di Azure Information Protection, vedono l'etichetta di Azure Information Protection assegnata. 

Se le etichette di Azure Information Protection applicano la protezione, aggiungere quest'ultima alla configurazione della regola: selezionare l'opzione per modificare la sicurezza del messaggio, applicare la protezione dei diritti e quindi selezionare il modello RMS o l'opzione Non inoltrare.

È anche possibile configurare regole del flusso di posta per eseguire il mapping inverso. Quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente:

- Per ogni etichetta di Azure Information Protection, creare una regola del flusso di posta da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **General**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver personalizzato il client di Azure Information Protection, vedere le risorse seguenti per altre informazioni eventualmente necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


