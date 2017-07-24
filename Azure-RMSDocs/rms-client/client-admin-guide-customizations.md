---
title: Configurazioni personalizzate per il client Azure Information Protection
description: Informazioni sulla personalizzazione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 41e9e8aff35727a40413e0bf18e46f1ad14e9222
ms.sourcegitcommit: 724b0b5d7a3ab694643988148ca68c0eac769f1e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2017
---
# <a name="custom-configurations-for-the-azure-information-protection-client"></a>Configurazioni personalizzate per il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client di Azure Information Protection.

Alcune di queste impostazioni richiedono la modifica del Registro di sistema e alcune usano impostazioni avanzate che è necessario configurare nel Portale di Azure e quindi pubblicare perché i client possano scaricarle. 

Alcune impostazioni, poi, potrebbero essere disponibili solo in una versione di anteprima del client di Azure Information Protection. Per queste impostazioni la documentazione indica una versione minima del client. Per le impostazioni e le configurazioni supportate nella versione del client con disponibilità generale, la documentazione non indica alcun numero di versione minima del client.

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Come configurare le impostazioni avanzate di configurazione del client nel portale

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza e quindi passare al pannello **Azure Information Protection**.

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

## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, in genere gli utenti non hanno bisogno di accedere con un nome utente diverso quando usano il client Azure Information Protection. Per un amministratore, tuttavia, può essere necessario accedere con le credenziali di un altro utente durante una fase di testing. 

È possibile verificare con quale account è stato eseguito l'accesso usando la finestra di dialogo di **Microsoft Azure Information Protection**: nell'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'uso di un account non corretto è l'impossibilità di scaricare i criteri di Azure Information Protection, di visualizzare le etichette corrette o di ottenere il comportamento previsto.

Per accedere come utente diverso:

1. A seconda della versione del client di Azure Information Protection: 
    
    - Per la versione disponibile a livello generale del client Azure Information Protection: usando un editor del Registro di sistema, passare a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** ed eliminare il valore **TokenCache** (con i dati associati).
    
    - Per la versione di anteprima corrente del client Azure Information Protection: passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzato un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e fare clic su **Accedi** dalla sezione **Stato del client** aggiornata.

Inoltre:

- Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. Per testare Azure Information Protection con più tenant, usare computer diversi.

- Se si usa la funzione Single Sign-On, è necessario uscire da Windows, modificare il Registro di sistema e quindi accedere con un account utente diverso. Il client di Azure Information Protection esegue quindi automaticamente l'autenticazione tramite l'account utente usato per l'accesso.

- Se si vogliono reimpostare le impostazioni utente per il servizio Azure Rights Management, è possibile farlo tramite l'opzione **Guida e commenti**.

- Per eliminare i criteri di Azure Information Protection attualmente scaricati, rimuovere il file **Policy.msip** dalla cartella **%localappdata%\Microsoft\MSIP**.

- Se è disponibile la versione di anteprima corrente del client Azure Information Protection, è possibile usare l'opzione **Ripristina le impostazioni** in **Guida e commenti e suggerimenti** per disconnettersi ed eliminare i criteri di Azure Information Protection scaricati.

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

È possibile definire questa configurazione avanzata modificando il Registro di sistema se si usa il client di Azure Information Protection versione 1.3.0.0 o successiva. 

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. Se si è conoscenza che il computer in uso non sarà in grado di connettersi a Internet per un determinato periodo di tempo, è possibile impedire al client di provare a connettersi al servizio modificando il Registro di sistema. 

Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Verificare che nel client sia presente un file di criteri validi denominato **Policy.msip**, nella cartella **%localappdata%\Microsoft\MSIP**. Se necessario, è possibile esportare i criteri dal portale di Azure e copiare il file esportato nel computer client. È anche possibile usare questo metodo per sostituire un file di criteri non aggiornato con i criteri pubblicati più recenti.

## <a name="hide-the-do-not-forward-button-in-outlook"></a>Nascondere il pulsante Non inoltrare in Outlook

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. Questa impostazione richiede anche una versione di anteprima del client di Azure Information Protection con il numero di versione minimo **1.8.41.0**.

Quando è configurata, questa impostazione nasconde il pulsante **Non inoltrare** della barra multifunzione in Outlook. Questa opzione, però, non viene nascosta nel menu di Office.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **DisableDNF**

- Valore: **True**

## <a name="make-the-custom-permissions-options-unavailable-to-users"></a>Rendere non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate

Questa configurazione usa un'[impostazione avanzata del client](#how-to-configure-advanced-client-configuration-settings-in-the-portal) che deve essere configurata nel Portale di Azure. 

Quando si configura questa impostazione e si pubblicano i criteri per gli utenti, le opzioni relative alle autorizzazioni personalizzate presenti nelle posizioni seguenti non sono più disponibili per la selezione da parte degli utenti:

- Nelle applicazioni di Office: scheda **Home** > gruppo **Protezione** > **Proteggi** > **Autorizzazioni personalizzate**

- In File Explorer fare clic con il pulsante destro del mouse su > **Classifica e proteggi** > **Autorizzazioni personalizzate**

Questa impostazione non influisce sulle autorizzazioni personalizzate che è possibile configurare dalle opzioni del menu di Office. 

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableCustomPermissions**

- Valore: **False**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Nascondere in modo permanente la barra di Azure Information Protection

Questa configurazione usa un'impostazione avanzata che deve essere configurata nel Portale di Azure. Questa impostazione richiede anche una versione di anteprima del client di Azure Information Protection con il numero di versione minimo **1.9.58.0**.

Quando si configura questa impostazione, si pubblicano i criteri per gli utenti e un utente sceglie di non visualizzare la barra di Azure Information Protection nelle applicazioni di Office, la barra rimane nascosta. Ciò si verifica se l'utente deseleziona l'opzione **Mostra barra**: nella scheda **Home**, nel gruppo **Protezione**, fare clic sul pulsante **Proteggi**. Questa impostazione non ha alcun effetto se l'utente chiude la barra tramite l'icona **Chiudi questa barra**.

Anche se la barra di Azure Information Protection rimane nascosta, gli utenti possono visualizzarla temporaneamente per selezionare un'etichetta, se è stata configurata la classificazione consigliata o se un documento o un messaggio di posta elettronica deve avere un'etichetta. L'impostazione, poi, non influisce sulle etichette configurate dall'utente connesso o da altri utenti, ad esempio la classificazione manuale o automatica, o sull'impostazione di un'etichetta predefinita.

Per configurare questa impostazione avanzata, immettere le stringhe seguenti:

- Chiave: **EnableBarHiding**

- Valore: **True**

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
