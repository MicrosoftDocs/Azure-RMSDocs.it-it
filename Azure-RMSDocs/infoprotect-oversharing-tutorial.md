---
title: Esercitazione - Usare Azure Information Protection per il controllo dell'oversharing - AIP
description: Esercitazione introduttiva per configurare e vedere in azione le impostazioni avanzate con le quali il client di Azure Information Protection mostra un avviso, chiede una giustificazione o blocca l'invio di messaggi da Outlook.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e386cfb416d508f46e60b4c75a7ac7710d510088
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048496"
---
# <a name="tutorial-configure-azure-information-protection-to-control-oversharing-of-information-using-outlook"></a>Esercitazione: configurare Azure Information Protection per il controllo dell'oversharing delle informazioni con Outlook

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Configurare le impostazioni che implementano messaggi di avviso, giustificazione o di blocco popup in Outlook
> * Vedere le impostazioni in azione
> * Esaminare i messaggi utente e le azioni registrati nel log eventi 


La posta elettronica è uno dei metodi più comuni con cui gli utenti condividono informazioni in modo inappropriato, sia nel messaggio in sé che negli allegati. È possibile usare soluzioni di prevenzione della perdita di dati (DLP) in grado di identificare informazioni sensibili note e impedire che escano dai confini dell'organizzazione. È tuttavia anche possibile usare il client di Azure Information Protection con alcune impostazioni avanzate del client per prevenire l'oversharing e anche per istruire gli utenti con messaggi interattivi che forniscono feedback in tempo reale.

Questa esercitazione descrive una configurazione di base che usa una sola etichetta per illustrare i messaggi di avviso, giustificazione e blocco a cui gli utenti possono rispondere.

È possibile completare questa esercitazione in circa 15 minuti.

## <a name="prerequisites"></a>Prerequisiti 

Per completare questa esercitazione, è necessario:

1. Disporre di una sottoscrizione che includa un piano 2 di Azure Information Protection.
    
    In assenza di una sottoscrizione con questo piano, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Avere aggiunto il riquadro Azure Information Protection al portale di Azure e aver pubblicato almeno un'etichetta nei criteri globali di Azure Information Protection.
    
    Anche se questa esercitazione usa l'etichetta **General** predefinita, questa etichetta può essere eventualmente sostituita con un'altra. Per informazioni sull'aggiunta del riquadro Azure Information Protection oppure se non sono ancora state pubblicate etichette nei criteri globali, vedere [Avvio rapido: Aggiungere Azure Information Protection al portale di Azure e visualizzare i criteri](quickstart-viewpolicy.md).

3. Un computer con Windows (almeno Windows 7 con Service Pack 1) in cui sia possibile accedere ad Outlook. Prepararsi a riavviare Outlook più volte durante questa esercitazione.

4. Il client Azure Information Protection (versione classica) deve essere installato nel computer in uso con Windows.
    
    È possibile installare la versione classica del client accedendo all'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018) e scaricando **AzInfoProtection.exe** dalla pagina di Azure Information Protection. 
    
    Se si usa il client di etichettatura unificato anziché la versione classica del client, vedere le istruzioni seguenti che illustrano come usare le impostazioni avanzate di PowerShell per le configurazioni equivalenti in questa esercitazione:
    
    - Istruzioni per la guida dell'amministratore: [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](./rms-client/clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - Video: [Configurazione popup di Outlook di Azure Information Protection](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/)

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

A questo punto, procedere con l'esercitazione.

## <a name="identify-a-label-id-for-testing"></a>Identificare un ID etichetta per il test

Per questa esercitazione si userà una sola etichetta per visualizzare il comportamento ottenuto per gli utenti. È possibile usare qualsiasi etichetta, ma un buon esempio per il test è l'etichetta predefinita denominata **General**, che è in genere adatta per i dati aziendali non destinati all'uso pubblico e non applica protezione.

Per specificare un'etichetta è necessario conoscerne l'ID, individuabile nel portale di Azure:

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale. Passare quindi ad **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Information** e selezionare **Azure Information Protection**.
    
    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Selezionare **Classificazioni** > **Etichette** e quindi selezionare l'etichetta **General** per aprire il pannello **Etichetta: Generale**. 

3. Individuare l'ID etichetta nella parte inferiore del riquadro:
    
    ![Esercitazione di Azure Information Protection - Individuare l'ID etichetta](./media/label-id.png)

4. Copiare e incollare il valore dell'ID etichetta in un file temporaneo, in modo che questo valore possa essere facilmente copiato per un passaggio successivo. In questo esempio, il valore dell'ID etichetta è **0e421e6d-ea17-4fdb-8f01-93a3e71333b8**.

5. Chiudere il pannello **Etichetta: Generale**, ma non chiudere il portale di Azure.

## <a name="create-a-scoped-policy-to-test-the-new-advanced-client-settings"></a>Creare un criterio con ambito per testare le nuove impostazioni avanzate del client

Verrà creato un nuovo criterio con ambito in modo che le nuove impostazioni avanzate del client saranno applicabili solo all'utente, per obiettivi di test.

1. Nel riquadro **Azure Information Protection - Criteri** selezionare **Aggiungi un nuovo criterio**. Verrà quindi visualizzato il riquadro **Criteri** con le etichette e le impostazioni dei criteri globali esistenti.

2. Specificare il nome **Oversharing tutorial** (Esercitazione sull'oversharing) per il criterio ed eventualmente la descrizione **Advanced client settings to control oversharing using Outlook** (Impostazioni avanzate del client per il controllo dell'oversharing con Outlook).

3. Scegliere **Selezionare gli utenti o i gruppi a cui viene applicato il criterio** e specificare il proprio account utente usando i riquadri successivi.

4. Con il nome account ora visualizzato nel riquadro **Criteri**, selezionare **Salva** senza apportare altre modifiche alle etichette o alle impostazioni presenti in questo riquadro. Potrebbe essere necessario confermare la scelta. 

Questo criterio con ambito è ora pronto per l'aggiunta di impostazioni client avanzate. Chiudere il pannello **Criteri: Oversharing tutorial**, ma non chiudere il portale di Azure.

## <a name="configure-and-test-advanced-client-settings-to-warn-prompt-for-justification-or-block-emails-that-have-the-general-label"></a>Configurare e testare le impostazioni avanzate del client per visualizzare avvisi, richiedere una giustificazione o bloccare l'invio in caso di messaggi di posta elettronica con etichetta General

Per questo passaggio dell'esercitazione, verranno specificate le seguenti impostazioni avanzate del client, che verranno testate una alla volta:

- **OutlookWarnUntrustedCollaborationLabel**
- **OutlookJustifyUntrustedCollaborationLabel**
- **OutlookBlockUntrustedCollaborationLabel**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>Creare l'impostazione avanzata del client per avvisare gli utenti se un messaggio di posta elettronica o un allegato ha l'etichetta General

Usando il criterio con ambito appena creato, verrà aggiunta una nuova impostazione avanzata del client denominata **OutlookWarnUntrustedCollaborationLabel** con l'ID dell'etichetta**General**: 

1. Tornare al riquadro **Azure Information Protection - Criteri** e selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** digitare il nome dell'impostazione avanzata, ovvero **OutlookWarnUntrustedCollaborationLabel**, e incollare il proprio ID etichetta per il valore. Usando l'ID etichetta di esempio:
    
    
    ![Esercitazione di Azure Information Protection: creare l'impostazione avanzata OutlookWarnUntrustedCollaborationLabel del client ](./media/configure-warnmessage.png)

3. Selezionare **Salva e chiudi**.

Non chiudere il riquadro **Criteri** o il portale di Azure.

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>Testare le impostazioni avanzate del client per avvisare gli utenti se un messaggio di posta elettronica o un allegato ha l'etichetta General

Nel computer client si vedranno ora i risultati della configurazione di questa impostazione avanzata del client.

1. Aprire Outlook nel computer client. 
    
    Se Outlook è già aperto, riavviarlo. Il riavvio è necessario per scaricare le modifiche appena apportate.

2. Creare un nuovo messaggio di posta elettronica e applicare l'etichetta **General**. Ad esempio, dalla scheda **File** selezionare il pulsante **Proteggi**, quindi selezionare **General**.

3. Specificare il proprio indirizzo e-mail nel campo **A** e digitare **Testing the General label for the Warn message** come oggetto. Inviare il messaggio di posta elettronica.

4. Come risultato dell'impostazione avanzata del client viene visualizzato il seguente avviso, che richiede la conferma prima di inviare il messaggio di posta elettronica. Ad esempio:
    
    ![Esercitazione di Azure Information Protection: vedere l'impostazione avanzata OutlookWarnUntrustedCollaborationLabel del client ](./media/see-warnmessage.png)
    
5. Supponendo di essere un utente che ha provato per errore a inviare un messaggio con etichetta **General**, selezionare **Annulla**. Come si può vedere, il messaggio non viene inviato, ma viene conservato per consentire modifiche, ad esempio al contenuto o all'etichetta.

6. Senza apportare modifiche, selezionare nuovamente **Invia**. Supponendo di essere un utente che conferma l'appropriatezza del contenuto per l'invio, questa volta selezionare **Conferma e invia**. Il messaggio di posta elettronica è stato inviato.

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>Modificare l'impostazione avanzata del client per chiedere agli utenti una giustificazione se un messaggio di posta elettronica ha l'etichetta General

L'impostazione avanzata esistente del client verrà modificata conservando l'ID etichetta **General**, ma cambiando il nome in **OutlookJustifyUntrustedCollaborationLabel**: 

1. Nel riquadro **Azure Information Protection - Criteri** selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** sostituire il nome dell'impostazione avanzata creata in precedenza, ovvero **OutlookWarnUntrustedCollaborationLabel**, con il nuovo nome **OutlookJustifyUntrustedCollaborationLabel**:
    
    ![Esercitazione di Azure Information Protection: creare l'impostazione avanzata OutlookJustifyUntrustedCollaborationLabel del client ](./media/configure-justifymessage.png)

3. Selezionare **Salva e chiudi**.

Non chiudere il riquadro **Criteri** o il portale di Azure.

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>Testare l'impostazione avanzata del client che chiede agli utenti una giustificazione se un messaggio di posta elettronica ha l'etichetta General

Nel computer client si vedranno ora i risultati di questa nuova impostazione avanzata del client.

1. Nel computer client riavviare Outlook per scaricare la modifica appena apportata.

2. Creare un nuovo messaggio di posta elettronica e applicare l'etichetta **General** come in precedenza. Ad esempio, dalla scheda **File** selezionare il pulsante **Proteggi**, quindi selezionare **General**.

3. Specificare il proprio indirizzo e-mail nel campo **A** e digitare **Testing the General label for the Justify message** come oggetto. Inviare il messaggio di posta elettronica.

4. Questa volta viene visualizzato il messaggio seguente, che chiede di fornire una giustificazione prima di inviare il messaggio di posta elettronica. Ad esempio:
    
    ![Esercitazione di Azure Information Protection: vedere l'impostazione avanzata OutlookJustifyUntrustedCollaborationLabel del client ](./media/see-justifymessage.png)
    
5. Supponendo di essere un utente che ha provato per errore a inviare un messaggio con etichetta **General**, selezionare **Annulla**. Come si può vedere, il messaggio non viene inviato, ma viene conservato per consentire modifiche, ad esempio al contenuto o all'etichetta.

6. Senza apportare modifiche, selezionare nuovamente **Invia**. Questa volta selezionare una delle opzioni di giustificazione, ad esempio **I confirm the recipients are approved for sharing this content** (Confermo che i destinatari sono autorizzati per la condivisione di questo contenuto), quindi selezionare **Conferma e invia**. Il messaggio di posta elettronica è stato inviato.

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>Modificare l'impostazione avanzata del client per impedire agli utenti di inviare un messaggio di posta elettronica avente l'etichetta General

L'impostazione avanzata esistente del client verrà modificata ancora una volta, conservando l'ID etichetta **General**, ma cambiando il nome in **OutlookBlockUntrustedCollaborationLabel**: 

1. Nel riquadro **Azure Information Protection - Criteri** del portale di Azure selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** sostituire il nome dell'impostazione avanzata creata in precedenza, ovvero **OutlookJustifyUntrustedCollaborationLabel**, con il nuovo nome **OutlookBlockUntrustedCollaborationLabel**:
    
    ![Esercitazione di Azure Information Protection: creare l'impostazione avanzata OutlookBlockUntrustedCollaborationLabel del client ](./media/configure-blockmessage.png)

3. Selezionare **Salva e chiudi**.

Non chiudere il riquadro **Criteri** o il portale di Azure.

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>Testare l'impostazione avanzata del client che impedisce agli utenti di inviare un messaggio di posta elettronica avente l'etichetta General

Nel computer client si vedranno ora i risultati di questa nuova impostazione avanzata del client.

1. Nel computer client riavviare Outlook per scaricare la modifica appena apportata.

2. Creare un nuovo messaggio di posta elettronica e applicare l'etichetta **General** come in precedenza. Ad esempio, dalla scheda **File** selezionare il pulsante **Proteggi**, quindi selezionare **General**.

3. Specificare il proprio indirizzo e-mail nel campo **A** e digitare **Testing the General label for the Block message** come oggetto. Inviare il messaggio di posta elettronica.

4. Questa volta viene visualizzato il messaggio seguente che impedisce l'invio del messaggio di posta elettronica. Ad esempio:
    
    ![Tutorial di Azure Information Protection: messaggio popup di blocco del messaggio di posta elettronica](./media/see-blockmessage.png)

5. Agendo nei panni del proprio utente, l'unica opzione disponibile è **OK**, che riporta al messaggio di posta elettronica in cui è possibile apportare modifiche. Selezionare **OK** e annullare questo messaggio di posta elettronica.

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>Usare il log eventi per identificare i messaggi e le azioni dell'utente per l'etichetta General

Prima di passare allo scenario successivo per il caso in cui un messaggio di posta elettronica o un allegato non abbia un'etichetta, avviare Visualizzatore eventi e passare a **Registri applicazioni e servizi** > **Azure Information Protection**.

Per ognuno dei test effettuati, vengono creati eventi informativi per registrare sia il messaggio che la risposta dell'utente:

- Messaggi di avviso: ID informazioni 301

- Messaggi di giustificazione: ID informazioni 302

- Messaggi di blocco: ID informazioni 303

Ad esempio, il primo test consisteva nel visualizzare un avviso per l'utente ed è stato selezionato **Annulla**, quindi **User Response** (Risposta utente) visualizza **Dismissed** (Ignorato) nel primo evento 301. Ad esempio:

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

Successivamente è stato tuttavia selezionato **Conferma e invia** e questa azione si riflette nel successivo evento 301, in cui **User Response** (Risposta utente) visualizza **Confirmed** (Confermato):

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

Lo stesso schema si ripete per il messaggio di giustificazione, che ha un evento 302. Il primo evento ha per **User Response** (Risposta utente) il valore **Dismissed** (Ignorato) e il secondo mostra la giustificazione selezionata. Ad esempio:

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Justify message.msg
Item Name: Testing the General label for the Justify message
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

Nella parte superiore del log eventi viene visualizzata la registrazione del messaggio di blocco, con evento 303. Ad esempio:

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Block message.msg
Item Name: Testing the General label for the Block message
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

### <a name="optional-create-an-additional-advanced-client-setting-to-exempt-these-messages-for-internal-recipients"></a>Facoltativo: Creare un'impostazione client avanzata aggiuntiva per creare una deroga per questi messaggi se diretti a destinatari interni

I messaggi di avviso, giustificazione e blocco sono stati testati usando il proprio indirizzo di posta elettronica come destinatario. In un ambiente di produzione è possibile scegliere di visualizzare questi messaggi per le etichette specificate solo se i destinatari sono esterni alla propria organizzazione. La deroga può anche essere estesa ai partner con cui l'organizzazione collabora regolarmente.

Per illustrare il funzionamento, verrà creata un'impostazione client avanzata aggiuntiva denominata **OutlookBlockTrustedDomains** e verrà specificato il nome di dominio del proprio indirizzo di posta elettronica. In questo modo si eviterà che il messaggio di blocco visualizzato in precedenza venga visualizzato per i destinatari che condividono il nome di dominio nell'indirizzo di posta elettronica, ma verrà comunque visualizzato per altri destinatari. Allo stesso modo è possibile creare impostazioni client avanzate aggiuntive per **OutlookWarnTrustedDomains** e **OutlookJustifyTrustedDomains**.

1. Nel riquadro **Azure Information Protection - Criteri** del portale di Azure selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** digitare il nome dell'impostazione avanzata, ovvero **OutlookBlockTrustedDomains**, e incollare il nome di dominio del proprio indirizzo e-mail come valore. Ad esempio:
    
    ![Esercitazione di Azure Information Protection: creare l'impostazione avanzata OutlookBlockTrustedDomains del client](./media/configure-exemptblockdomain.png)

4. Selezionare **Salva e chiudi**. Non chiudere il riquadro **Criteri** o il portale di Azure.

5. A questo punto, ripetere il [test precedente per impedire agli utenti di inviare un messaggio di posta elettronica con l'etichetta General](#test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label) e non verrà più visualizzato il messaggio di blocco quando si usa il proprio indirizzo di posta elettronica. Il messaggio di posta elettronica viene inviato senza interruzioni.
    
    Per confermare che il messaggio di blocco viene visualizzato ancora per i destinatari esterni, ripetere il test un'altra volta specificando un destinatario all'esterno dell'organizzazione. Questa volta il messaggio di blocco viene visualizzato nuovamente ed indica il nuovo indirizzo del destinatario come non attendibile.

## <a name="configure-and-test-an-advanced-client-setting-to-warn-prompt-for-justification-or-block-emails-that-dont-have-a-label"></a>Configurare e testare un'impostazione avanzata del client per visualizzare avvisi, richiedere una giustificazione o bloccare l'invio in caso di messaggi di posta elettronica senza etichetta

Per questo passaggio dell'esercitazione verrà specificata una nuova impostazione avanzata del client con valori diversi, che verranno testati uno alla volta:

- **OutlookUnlabeledCollaborationAction**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>Creare l'impostazione avanzata del client per avvisare gli utenti se un messaggio di posta elettronica non ha un'etichetta

Questa nuova impostazione avanzata del client denominata **OutlookUnlabeledCollaborationAction** non richiede un ID etichetta, ma specifica l'azione da intraprendere per i contenuti senza etichetta: 

1. Nel riquadro **Azure Information Protection - Criteri** del portale di Azure selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** digitare il nome dell'impostazione avanzata, ovvero **OutlookUnlabeledCollaborationAction** e specificare **Warn** come valore:
    
    ![Esercitazione di Azure Information Protection: creare l'impostazione avanzata OutlookUnlabeledCollaborationAction del client con il valore Warn ](./media/configure-nolablewarn.png)

3. Selezionare **Salva e chiudi**.

Non chiudere il riquadro **Criteri** o il portale di Azure.

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>Testare l'impostazione avanzata del client che avvisa gli utenti se un messaggio di posta elettronica non ha un'etichetta

Nel computer client si vedranno ora i risultati della configurazione di questa impostazione avanzata del client per il caso in cui il contenuto non abbia un'etichetta:

1. Nel computer client riavviare Outlook per scaricare la modifica appena apportata.

2. Creare un nuovo messaggio di posta elettronica e questa volta non applicare un'etichetta.

3. Specificare il proprio indirizzo e-mail nel campo **A** e digitare **Testing send an email without a label for the Warn message** come oggetto. Inviare il messaggio di posta elettronica.

4. Questa volta viene visualizzato un messaggio **Conferma obbligatoria** al quale si può rispondere con **Conferma e invia** o **Annulla**:
    
    ![Esercitazione di Azure Information Protection: vedere l'impostazione avanzata OutlookUnlabeledCollaborationAction del client con il valore Warn](./media/see-nolablewarn.png)

5. Selezionare **Conferma e invia**.

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-is-unlabeled"></a>Modificare l'impostazione avanzata del client per chiedere agli utenti una giustificazione se un messaggio di posta elettronica non ha un'etichetta

L'impostazione avanzata esistente del client verrà modificata conservando il nome **OutlookUnlabeledCollaborationAction**, ma cambiando il valore in **Justify**: 

1. Nel riquadro **Azure Information Protection - Criteri** selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** individuare l'impostazione **OutlookUnlabeledCollaborationAction** e sostituire il valore **Warn** precedente con il nuovo valore **Justify**:
    
    ![Esercitazione di Azure Information Protection: modificare l'impostazione avanzata OutlookUnlabeledCollaborationAction del client con il valore Justify](./media/configure-justifymessage2.png)

3. Selezionare **Salva e chiudi**.

Non chiudere il riquadro **Criteri** o il portale di Azure.

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-isnt-labeled"></a>Testare l'impostazione avanzata del client che chiede agli utenti una giustificazione se un messaggio di posta elettronica non ha etichetta

Nel computer client si vedranno ora i risultati della modifica del valore per questa impostazione avanzata del client.

1. Nel computer client riavviare Outlook per scaricare la modifica appena apportata.

2. Creare un nuovo messaggio di posta elettronica e anche in questo caso non applicare un'etichetta.

3. Specificare il proprio indirizzo e-mail nel campo **A** e digitare **Testing send an email without a label for the Justify message** come oggetto. Inviare il messaggio di posta elettronica.

4. Questa volta verrà visualizzato il messaggio **La giustificazione è obbligatoria** con diverse opzioni:
    
    ![Esercitazione di Azure Information Protection: vedere l'impostazione avanzata OutlookUnlabeledCollaborationAction del client con il valore Justify](./media/see-nolabljustify.png)

5. Selezionare un'opzione, ad esempio **My manager approved sharing of this content** (Il manager ha approvato la condivisione di questo contenuto). Selezionare quindi **Conferma e invia**.

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>Modificare l'impostazione avanzata del client per impedire agli utenti di inviare un messaggio di posta elettronica senza etichetta

Come in precedenza, l'impostazione avanzata esistente del client verrà modificata conservando il nome **OutlookUnlabeledCollaborationAction**, ma cambiando il valore in **Block**: 

1. Nel riquadro **Azure Information Protection - Criteri** selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Impostazioni avanzate**.

2. Nel riquadro **Impostazioni avanzate** individuare l'impostazione **OutlookUnlabeledCollaborationAction** e sostituire il valore **Justify** precedente con il nuovo valore **Block**:
    
    ![Esercitazione di Azure Information Protection: modificare l'impostazione avanzata OutlookUnlabeledCollaborationAction del client con il valore Block](./media/configure-blockmessage2.png)

3. Selezionare **Salva e chiudi**.

Non chiudere il riquadro **Criteri** o il portale di Azure.

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>Testare l'impostazione avanzata del client che impedisce agli utenti di inviare un messaggio di posta elettronica senza etichetta

Nel computer client si vedranno ora i risultati della modifica del valore per questa impostazione avanzata del client.

1. Nel computer client riavviare Outlook per scaricare la modifica appena apportata.

2. Creare un nuovo messaggio di posta elettronica e anche in questo caso non applicare un'etichetta.

3. Specificare il proprio indirizzo e-mail nel campo **A** e digitare **Testing send an email without a label for the Block message** come oggetto. Inviare il messaggio di posta elettronica.

4. Questa volta viene visualizzato il messaggio seguente che impedisce l'invio del messaggio di posta elettronica, con una spiegazione per l'utente. Ad esempio:
    
    ![Esercitazione di Azure Information Protection: vedere l'impostazione avanzata OutlookWarnUntrustedCollaborationLabel del client con il valore Block](./media/see-blockmessage2.png)

5. Agendo nei panni del proprio utente, l'unica opzione disponibile è **OK**, che riporta al messaggio di posta elettronica in cui è possibile selezionare un'etichetta.
    
    Selezionare **OK** e annullare questo messaggio di posta elettronica.

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-unlabeled-email"></a>Usare il log eventi per identificare i messaggi e le azioni dell'utente per il messaggio di posta elettronica senza etichetta

Come in precedenza, i messaggi e le risposte dell'utente vengono registrati in Visualizzatore eventi, **Registri applicazioni e servizi** > **Azure Information Protection**, con gli stessi ID evento.

- Messaggi di avviso: ID informazioni 301

- Messaggi di giustificazione: ID informazioni 302

- Messaggi di blocco: ID informazioni 303

Ad esempio, i risultati della richiesta di giustificazione quando il messaggio di posta elettronica non ha un'etichetta:

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing send an email without a label for the Justify message.msg
Item Name: Testing send an email without a label for the Justify message
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vogliono mantenere le modifiche apportate in questa esercitazione, seguire questa procedura:

1. Nel riquadro **Azure Information Protection - Criteri** del portale di Azure selezionare il menu di scelta rapida ( **...** ) accanto a **Oversharing tutorial**. Selezionare quindi **Elimina criteri**.

2. Se viene chiesto di confermare, selezionare **OK**.

Riavviare Outlook in modo che non sia più configurato per le impostazioni che sono state definite per questa esercitazione.

## <a name="next-steps"></a>Passaggi successivi

Per test più rapidi, questa esercitazione ha usato un messaggio di posta elettronica per un singolo destinatario e senza allegati. È tuttavia possibile applicare lo stesso metodo a più destinatari e più etichette e applicare la stessa logica anche agli allegati di posta elettronica il cui stato di etichettatura è spesso meno evidente per gli utenti. Ad esempio, il messaggio di posta elettronica in sé è etichettato come Public, ma la presentazione di PowerPoint allegata ha l'etichetta General. Per altre informazioni sulle opzioni di configurazione, vedere la sezione seguente dalla guida dell'amministratore: [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](./rms-client/client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)

La Guida dell'amministratore contiene anche informazioni su altre impostazioni avanzate del client che è possibile usare per personalizzare il comportamento del client. Per un elenco completo, vedere [Impostazioni client avanzate disponibili](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings).
