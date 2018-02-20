---
title: Configurazioni personalizzate per il client Azure Information Protection
description: Informazioni sulla personalizzazione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 662ed627fc6138e1ff16efb731b209964784432f
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client di Azure Information Protection.

Alcune di queste impostazioni richiedono la modifica del Registro di sistema e alcune usano impostazioni avanzate che è necessario configurare nel Portale di Azure e quindi pubblicare perché i client possano scaricarle.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Come configurare le impostazioni avanzate di configurazione del client nel portale

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](../deploy-use/configure-policy.md#signing-in-to-the-azure-portal) e quindi passare al pannello **Azure Information Protection**.

2. Nel pannello iniziale di Azure Information Protection selezionare **Criteri con ambito**.

3. Nel pannello **Azure Information Protection - Criteri con ambito** selezionare il menu di scelta rapida (**...**) accanto ai criteri, contenente le impostazioni avanzate. Selezionare quindi **Impostazioni avanzate**.
    
    È possibile configurare le impostazioni avanzate per i criteri globali e per i criteri con ambito.

4. Nel pannello **Impostazioni avanzate** digitare il nome e il valore dell'impostazione avanzata e quindi selezionare **Salva e chiudi**.

5. Fare clic su **Pubblica** e assicurarsi che gli utenti interessati da questi criteri riavviino le applicazioni di Office eventualmente aperte.

6. Se l'impostazione non è più necessaria e si vuole ripristinare il comportamento predefinito, nel pannello **Impostazioni avanzate** selezionare il menu di scelta rapida (**...**) accanto all'impostazione non più necessaria e quindi selezionare **Elimina**. Quindi fare clic su **Salva e chiudi** e ripubblicare i criteri modificati.

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitare le richieste di accesso per i computer solo AD RMS

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection. Per i computer che comunicano solo con AD RMS questa configurazione può comportare una richiesta di accesso non necessaria per gli utenti. È possibile evitare questa richiesta di accesso modificando il Registro di sistema:

Individuare il nome di valore seguente e quindi impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indipendentemente da questa impostazione, il client Azure Information Protection segue il normale [processo di individuazione del servizio RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) per trovare il proprio cluster AD RMS.

## <a name="suppress-the-initial-congratulations-welcome-page"></a>Eliminare la pagina introduttiva "Congratulazioni!"

Quando il client di Azure Information Protection viene installato per la prima volta in un computer e un utente apre Word, Excel, PowerPoint o Outlook, una pagina **Complimenti!** mostra, attraverso brevi istruzioni, come usare la nuova barra Information Protection per selezionare le etichette. È possibile eliminare questa pagina, modificando il registro.

Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnableWelcomeExperience** 


## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, in genere gli utenti non hanno bisogno di accedere con un nome utente diverso quando usano il client Azure Information Protection. Per un amministratore, tuttavia, può essere necessario accedere con le credenziali di un altro utente durante una fase di testing. 

È possibile verificare con quale account è stato eseguito l'accesso usando la finestra di dialogo di **Microsoft Azure Information Protection**: nell'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'uso di un account non corretto è l'impossibilità di scaricare i criteri di Azure Information Protection, di visualizzare le etichette corrette o di ottenere il comportamento previsto.

Per accedere come utente diverso:

1. Passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzato un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e fare clic su **Accedi** dalla sezione **Stato del client** aggiornata.

Inoltre:

- Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. Per testare Azure Information Protection con più tenant, usare computer diversi.

- Se si usa la funzione Single Sign-On, è necessario uscire da Windows, modificare il Registro di sistema e quindi accedere con un account utente diverso. Il client di Azure Information Protection esegue quindi automaticamente l'autenticazione tramite l'account utente usato per l'accesso.

- È possibile usare l'opzione **Ripristina le impostazioni** in **Guida e commenti** per disconnettersi ed eliminare i criteri di Azure Information Protection scaricati.


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>Applicare la modalità di sola protezione quando l'organizzazione dispone di licenze miste

Se l'organizzazione non ha alcuna licenza per Azure Information Protection, ma dispone di licenze per Office 365 che includono il servizio Azure Rights Management per la protezione dei dati, il client Azure Information Protection per Windows viene eseguito automaticamente in [modalità di sola protezione](../rms-client/client-protection-only-mode.md).

Tuttavia, se l'organizzazione ha una sottoscrizione per Azure Information Protection, tutti i computer Windows possono scaricare i criteri di Azure Information Protection per impostazione predefinita. Il client Azure Information Protection non gestisce il controllo e l'applicazione delle licenze. 

Se alcuni utenti non dispongono di una licenza di Azure Information Protection, ma hanno una licenza per Office 365 che include il servizio Azure Rights Management, modificare il Registro di sistema nei computer degli utenti per impedire loro di eseguire le funzionalità di classificazione ed etichettatura senza licenza da Azure Information Protection.

Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Controllare inoltre che in questi computer non esista un file denominato **Policy.msip** nella cartella **%LocalAppData%\Microsoft\MSIP**. Se il file esiste, eliminarlo. Questo file contiene i criteri di Azure Information Protection e potrebbe essere stato scaricato prima della modifica del Registro di sistema o se il client Azure Information Protection è stato installato con l'opzione demo.

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. Se si è conoscenza che il computer in uso non sarà in grado di connettersi a Internet per un determinato periodo di tempo, è possibile impedire al client di provare a connettersi al servizio modificando il Registro di sistema. 

Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Verificare che nel client sia presente un file di criteri validi denominato **Policy.msip**, nella cartella **%LocalAppData%\Microsoft\MSIP**. Se necessario, è possibile esportare i criteri dal portale di Azure e copiare il file esportato nel computer client. È anche possibile usare questo metodo per sostituire un file di criteri non aggiornato con i criteri pubblicati più recenti.

Quando si esporta il criterio, questa azione carica un file compresso con più versioni dei criteri che corrispondono a versioni diverse del client Azure Information Protection:

1. Decomprimere il file e usare la tabella seguente per identificare il file di criteri necessario. 
    
    |Nome file|Versione del client corrispondente|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |versione 1.2|
    |Policy1.2.msip |versione 1.3 - 1.7|
    |Policy1.3.msip |versione 1.8 e successive|
    
2. Rinominare il file identificato come **Policy.msip**, quindi copiare la cartella **%LocalAppData%\Microsoft\MSIP** nei computer in cui è installato il client Azure Information Protection. 


## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Nascondere o visualizzare il pulsante Non inoltrare in Outlook

Il metodo consigliato per configurare questa opzione è tramite l'[impostazione dei criteri](../deploy-use/configure-policy-settings.md) **Add the Do Not Forward button to the Outlook ribbon** (Aggiungi il pulsante Non inoltrare alla barra multifunzione di Outlook). Tuttavia, è possibile configurare questa opzione anche tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) configurata nel portale di Azure.

Quando è configurata, questa impostazione nasconde o visualizza il pulsante **Non inoltrare** sulla barra multifunzione in Outlook. Questa impostazione non influisce sull'opzione Non inoltrare nei menu di Office.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **DisableDNF**

- Valore: **True** per nascondere il pulsante o **False** per visualizzarlo

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate

Il metodo consigliato per configurare questa opzione è tramite l'[impostazione dei criteri](../deploy-use/configure-policy-settings.md) **Make the custom permissions option available for users** (Rendi disponibile l'opzione per le autorizzazioni personalizzate). Tuttavia, è possibile configurare questa opzione anche tramite un'[impostazione client avanzata](#how-to-configure-advanced-client-configuration-settings-in-the-portal) configurata nel portale di Azure. 

Quando si configura questa impostazione e si pubblicano i criteri per gli utenti, le opzioni per le autorizzazioni personalizzate diventano disponibili per gli utenti in modo che possano selezionare impostazioni di protezione personali oppure non sono disponibili e quindi gli utenti non possono selezionare impostazioni di protezione personali, se non richiesto.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableCustomPermissions**

- Valore: **True** per rendere disponibile l'opzione per le autorizzazioni personalizzate o **False** per non renderla disponibile

> [!IMPORTANT]
> A meno che non si stia usando la versione di anteprima corrente del client, non impostare questa opzione su **False** se sono state configurate etichette per le autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file. In caso contrario, quando viene applicata l'etichetta, agli utenti non viene chiesto di configurare le autorizzazioni personalizzate. Il risultato è che il documento viene etichettato ma non protetto come previsto.

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Nascondere in modo permanente la barra di Azure Information Protection

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Usarla solo quando l'[impostazione dei criteri](../deploy-use/configure-policy-settings.md) **Display the Information Protection bar in Office apps** (Visualizza la barra di Information Protection nelle app di Office) è impostata su **On** (Attiva).

Quando si configura questa impostazione, si pubblicano i criteri per gli utenti e un utente sceglie di non visualizzare la barra di Azure Information Protection nelle applicazioni di Office, la barra rimane nascosta. Ciò si verifica se l'utente deseleziona l'opzione **Mostra barra**: nella scheda **Home**, nel gruppo **Protezione**, fare clic sul pulsante **Proteggi**. Questa impostazione non ha alcun effetto se l'utente chiude la barra tramite l'icona **Chiudi questa barra**.

Anche se la barra di Azure Information Protection rimane nascosta, gli utenti possono visualizzarla temporaneamente per selezionare un'etichetta, se è stata configurata la classificazione consigliata o se un documento o un messaggio di posta elettronica deve avere un'etichetta. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableBarHiding**

- Valore: **True**


## <a name="enable-recommended-classification-in-outlook"></a>Abilitare la classificazione consigliata in Outlook

Questa opzione di configurazione è attualmente in anteprima ed è soggetta a modifiche.

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure.

Quando si configura un'etichetta per la classificazione consigliata, agli utenti viene richiesto di accettare o ignorare l'etichetta consigliata in Word, Excel e PowerPoint. Questa impostazione estende questa indicazione per l'etichetta anche per la visualizzazione in Outlook.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **OutlookRecommendationEnabled**

- Valore: **True**


## <a name="set-a-different-default-label-for-outlook"></a>Impostare un'etichetta predefinita diversa per Outlook

Questa opzione di configurazione è attualmente in anteprima ed è soggetta a modifiche. Questa opzione di configurazione richiede inoltre la versione di anteprima del client.

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si configura questa impostazione, Outlook non applica l'etichetta predefinita configurata nei criteri di Azure Information Protection per l'impostazione **Selezionare l'etichetta predefinita**. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta.

Per applicare un'etichetta diversa, è necessario specificare il relativo ID. Il valore dell'ID etichetta è visualizzato nel pannello **Etichetta**, quando si visualizzano o si configurano i criteri di Azure Information Protection nel portale di Azure. Per i file a cui sono state applicate etichette, è anche possibile eseguire il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) per identificare l'ID etichetta (MainLabelId o SubLabelId). Quando un'etichetta ha etichette secondarie, specificare sempre l'ID della sola etichetta secondaria e non dell'etichetta padre.

Per fare in modo che Outlook non applichi l'etichetta predefinita, specificare **Nessuna**.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **OutlookDefaultLabel**

- Valore: \<**ID etichetta**> o **Nessuna**

## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>Etichettare un documento di Office usando una proprietà personalizzata esistente

Questa opzione di configurazione è attualmente in anteprima ed è soggetta a modifiche. 

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

Si supponga, ad esempio, di avere una colonna di SharePoint denominata **Classificazione** con i valori possibili **Pubblico**, **Generale** e **Riservato**. I documenti sono archiviati in SharePoint e viene loro assegnato uno di questi valori impostati per la proprietà Classificazione.

Per etichettare un documento di Office con uno di questi valori di classificazione, impostare **SyncPropertyName** su **Classificazione** e **SyncPropertyState** a  **OneWay**. 

A questo punto, quando un utente apre e salva uno di questi documenti di Office, il documento viene etichettato come **Pubblico**, **Generale** o **Riservato** se sono presenti etichette con questi nomi nei criteri di Azure Information Protection. In assenza di etichette con questi nomi, il documento rimane senza etichetta.

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Integrazione con la classificazione dei messaggi di Exchange per una soluzione di etichettatura dei dispositivi mobili

Benché Outlook sul Web non supporti ancora in modo nativo la protezione e la classificazione di Azure Information Protection, è possibile usare la classificazione dei messaggi di Exchange per estendere le etichette di Azure Information Protection agli utenti dei dispositivi mobili.

Per ottenere questa soluzione: 

1. Usare il cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) di Exchange PowerShell per creare le classificazioni dei messaggi con la proprietà Name che esegue il mapping ai nomi di etichetta nei criteri di Azure Information Protection. 

2. Creare una regola di trasporto di Exchange per ogni etichetta: applicare la regola quando le proprietà del messaggio includono la classificazione configurata e modificare le proprietà del messaggio per impostare un'intestazione del messaggio. 

    Per l'intestazione del messaggio, è possibile trovare le informazioni da specificare nelle intestazioni Internet di un messaggio di posta elettronica inviato e classificato tramite l'etichetta di Azure Information Protection. Cercare l'intestazione **msip_labels** e la stringa immediatamente successiva fino al punto e virgola incluso. Usando l'esempio precedente:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Quindi, per l'intestazione del messaggio nella regola, specificare **msip_labels** per l'intestazione e la parte rimanente della stringa per il valore dell'intestazione. Ad esempio:
    
    ![Regola di trasporto di Exchange Online di esempio che imposta l'intestazione del messaggio per un'etichetta di Azure Information Protection specifica](../media/exchange-rule-for-message-header.png)

Prima di eseguire il test della configurazione, tenere presente che spesso si verifica un ritardo quando vengono create o modificate le regole di trasporto. Ad esempio, può essere necessario attendere un'ora. Se la regola è attiva, quando gli utenti usano Outlook sul Web o un client per dispositivi mobili che supporta la protezione con Rights Management, si verificano gli eventi seguenti: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Se i destinatari visualizzano il messaggio di posta elettronica in Outlook e hanno installato il client di Azure Information Protection , vedono l'etichetta di Azure Information Protection assegnata e l'eventuale intestazione, piè di pagina o filigrana corrispondente del messaggio di posta elettronica. 

Se le etichette di Azure Information Protection applicano la protezione di Rights Management, aggiungere quest'ultima alla configurazione della regola: selezionando l'opzione per modificare la sicurezza del messaggio, applicare la protezione dei diritti e quindi selezionare il modello RMS o l'opzione Non inoltrare.

È anche possibile configurare regole di trasporto per eseguire il mapping inverso. Quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente:

- Per ogni etichetta di Azure Information Protection, creare una regola di trasporto da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **General**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver personalizzato il client di Azure Information Protection, vedere le risorse seguenti per altre informazioni eventualmente necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
