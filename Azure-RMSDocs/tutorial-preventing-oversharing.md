---
title: Esercitazione - Prevenzione dell'oversharing con Azure Information Protection (AIP)
description: Esercitazione dettagliata per l'uso del client di Azure Information Protection (AIP) per impedire l'oversharing del contenuto da parte degli utenti.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6936402c9b58bf46b94e71ab597ce04c0391f59d
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240819"
---
# <a name="tutorial-preventing-oversharing-in-outlook-using-azure-information-protection-aip"></a>Esercitazione: Prevenzione dell'oversharing in Outlook con Azure Information Protection (AIP)

>**Si applica a*: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client di etichettatura unificata di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

In qualità di amministratore di sistema è necessario assicurarsi che il contenuto dell'organizzazione rimanga sicuro e venga condiviso solo con utenti attendibili. Uno dei modi più comuni usato dagli utenti per condividere contenuto in modo non appropriato è la posta elettronica. Configurare i criteri in modo da impedire l'oversharing tramite Outlook, ad esempio limitando l'accesso solo a utenti specifici oppure consentendo agli utenti di condividere il contenuto solo con utenti esterni attendibili.

**Tempo necessario**: è possibile completare questa esercitazione in 30 minuti.

In questa esercitazione verranno illustrate le procedure per:
> [!div class="checklist"]
> * Configurare i comportamenti di avviso, giustificazione e blocco per condizioni di etichettatura specifiche
> * Vedere le impostazioni in azione
> * Esaminare i messaggi utente e le azioni registrati nel log eventi 

## <a name="tutorial-prerequisites"></a>Prerequisiti per l'esercitazione

Prima di iniziare questa esercitazione, assicurarsi di disporre dei requisiti di sistema seguenti.

|Prerequisiti  |Descrizione  |
|---------|---------|
|**Requisiti per il computer**     | Verificare quanto segue: <br /><br />- Disponibilità di un computer Windows con il client di etichettatura unificata di Azure Information Protection installato. Per altre informazioni, vedere [Avvio rapido: Distribuzione del client di etichettatura unificata di Azure Information Protection (AIP)](quickstart-deploy-client.md). <br /><br />- Disponibilità di PowerShell installato e possibilità di eseguire PowerShell come amministratore. <br /><br />- Possibilità di accedere a Outlook. Prepararsi a riavviare Outlook più volte durante questa esercitazione.     |
|**Sottoscrizione di Azure Information Protection**     |   Sarà necessaria una sottoscrizione che includa [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br /><br />In assenza di una di queste sottoscrizioni, creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.       |
|**Etichette di riservatezza e criteri di test**     |  Un etichetta di riservatezza **Generale** configurata nei criteri. <br /><br />Configurare le etichette di riservatezza nell'interfaccia di amministrazione dell'etichettatura, ovvero il Centro conformità di Microsoft 365, il Centro sicurezza Microsoft 365 o il Centro sicurezza e conformità di Microsoft 365. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels). <br /><br />Si consiglia di usare criteri di test per questa esercitazione, per evitare effetti sui criteri attivi. <br />Assicurarsi di avere a portata di mano il nome del criterio, nonché il GUID per l'etichetta **Generale**.   |
| | |

È possibile iniziare subito. 

## <a name="implement-a-warning-message-for-emails-labeled-as-general"></a>Implementare un messaggio di avviso per i messaggi di posta elettronica con l'etichetta Generale

Questa procedura descrive come configurare un criterio per avvisare gli utenti di Outlook prima dell'invio di un messaggio di posta elettronica con l'etichetta **Generale**. 

Gli utenti possono scegliere di tenere conto dell'avviso e modificare l'etichetta o il contenuto oppure possono scegliere di inviare comunque il messaggio di posta elettronica.

1. Nel computer client eseguire PowerShell come amministratore.

1. Eseguire il comando seguente per definire un messaggio di avviso per l'etichetta **Generale**. Quando si copia questo comando, sostituire **Global** con il nome del criterio e la stringa di caratteri lunga con l'ID dell'etichetta.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
    ```

    In questo esempio, il nome del criterio è **Global** e il GUID per l'etichetta **Generale** è **8faca7b8-8d20-48a3-8ea2-0f96310a848e**.

    > [!TIP]
    > Se si volesse applicare questa impostazione a più etichette, sarebbe sufficiente elencare i relativi GUID nel valore separati da virgole.

1. Testare l'impostazione in Outlook:

    1. Nel computer client aprire o riavviare Outlook per eseguire il pull delle impostazioni aggiornate.

    1. Creare un nuovo messaggio di posta elettronica e applicare l'etichetta **General**. Nella barra degli strumenti del messaggio selezionare il pulsante :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: **Riservatezza** e quindi selezionare **Generale**.

    1. Specificare il proprio indirizzo di posta elettronica nel campo **A**, `Testing a warning message for the General label` nel campo **Oggetto** e quindi inviare il messaggio di posta elettronica.

        Verrà visualizzato l'avviso seguente che richiede la conferma prima dell'invio del messaggio di posta elettronica. Ad esempio:

        :::image type="content" source="media/qs-tutor/ul-see-warnmessage.png" alt-text="Test di un messaggio di avviso per l'etichetta Generale":::

    1. Si supponga di essere un utente che ha provato per errore a inviare un messaggio con etichetta **Generale**. In questo caso si vuole tenere conto dell'avviso e quindi selezionare **Annulla**.

        Il messaggio di posta elettronica non viene inviato, ma rimane aperto in modo che sia possibile modificare il contenuto o l'etichetta.

    1. Non è necessario apportare modifiche ed è possibile decidere che il contenuto è appropriato per l'invio. Selezionare di nuovo **Invia**. Questa volta, quando viene visualizzato l'avviso, selezionare **Conferma e invia**.

        Il messaggio di posta elettronica è stato inviato.

Continuare con [Visualizzare un messaggio di avviso per i messaggi di posta elettronica con etichetta Generale solo quando vengono inviati esternamente](#show-a-warning-message-for-general-emails-only-when-theyre-sent-externally).

## <a name="show-a-warning-message-for-general-emails-only-when-theyre-sent-externally"></a>Visualizzare un messaggio di avviso per i messaggi di posta elettronica con etichetta Generale solo quando vengono inviati esternamente

Questa procedura descrive come aggiungere un'eccezione al messaggio di avviso configurato in precedenza, in modo che il messaggio di avviso venga visualizzato solo per i destinatari esterni.

Quando si invia un messaggio di posta elettronica con etichetta **Generale** internamente, il messaggio di avviso non viene visualizzato.

1. Nel computer client eseguire PowerShell come amministratore.

1. Eseguire il comando seguente per definire il dominio come attendibile per i messaggi di avviso. Quando si copia questo comando, sostituire **Global** con il nome del criterio specifico e **contoso.com** con il nome del dominio personale.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnTrustedDomains="contoso.com"}    
    ```

    > [!TIP]
    > Se si volesse applicare questa impostazione a più domini, ad esempio per aggiungere i partner attendibili, sarebbe sufficiente elencare i relativi domini nel valore separati da virgole.

1. Testare l'impostazione in Outlook:

    1. Nel computer client aprire o riavviare Outlook per eseguire il pull delle impostazioni aggiornate.

    1. Creare un nuovo messaggio di posta elettronica e applicare l'etichetta **General**. Nella barra degli strumenti del messaggio selezionare il pulsante :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: **Riservatezza** e quindi selezionare **Generale**.

    1. Specificare il proprio indirizzo di posta elettronica nel campo **A**, `Testing a warning message for the General label` nel campo **Oggetto** e quindi inviare il messaggio di posta elettronica.

        Il messaggio di posta elettronica viene inviato e non viene visualizzato alcun avviso.

## <a name="request-users-to-justify-sending-unlabeled-content"></a>Richiedere agli utenti di giustificare l'invio di contenuto senza etichetta

Questa procedura descrive come configurare le impostazioni avanzate in modo che gli utenti debbano giustificare l'invio di contenuto senza etichetta. 

1. Nel computer client eseguire PowerShell come amministratore.

1. Per fare in modo che Outlook visualizzi un messaggio di giustificazione per gli utenti se tentano di inviare un messaggio di posta elettronica senza etichetta, sostituire **Global** con il nome del criterio specifico ed eseguire:
 
    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Justify"}
    ```

1. Testare l'impostazione in Outlook:

    1. Nel computer client aprire o riavviare Outlook per eseguire il pull delle impostazioni aggiornate.

    1. Creare un nuovo messaggio di posta elettronica e verificare che non sia stata applicata alcuna etichetta.
    
        Ad esempio, se il criterio applica un'etichetta predefinita, usare il pulsante :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: per rimuoverla. 

    1. Specificare il proprio indirizzo di posta elettronica nel campo **A**, `Testing the justification message for unlabeled content` nel campo **Oggetto** e quindi inviare il messaggio di posta elettronica.
    
        Viene visualizzato un popup simile all'esempio seguente:

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify.png" alt-text="Messaggio di giustificazione di esempio per contenuto senza etichetta":::

    1. Selezionare una delle opzioni disponibili. Se si seleziona la terza opzione **Altro, come indicato**, immettere un testo di esempio nella casella di testo. 
    
    1. Selezionare **Conferma e invia**.
    
        Il messaggio di posta elettronica è stato inviato.

Continuare con [Personalizzare la richiesta di giustificazione in formato di testo libero](#customize-the-free-text-justification-prompt).

## <a name="customize-the-free-text-justification-prompt"></a>Personalizzare la richiesta di giustificazione in formato di testo libero

Questa procedura descrive come personalizzare la terza opzione nel messaggio di giustificazione predefinito. 

Ad esempio, è possibile aggiungere un testo per richiedere all'utente di aggiungere dettagli specifici o ricordare agli utenti di non immettere dati sensibili.

1. Nel computer client eseguire PowerShell come amministratore.

1. Per personalizzare la richiesta in formato di testo libero nel messaggio di giustificazione visualizzato, sostituire **Global** con il nome del criterio specifico ed eseguire:

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
    ```

    > [!TIP]
    > È possibile sostituire il valore tra virgolette con qualsiasi altro testo da aggiungere. 

1. Testare l'impostazione in Outlook:

    1. Nel computer client aprire o riavviare Outlook per eseguire il pull delle impostazioni aggiornate.

    1. Creare un nuovo messaggio di posta elettronica e verificare che non sia stata applicata alcuna etichetta. 

        Ad esempio, se il criterio applica un'etichetta predefinita, usare il pulsante :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: per rimuoverla. 

    1. Specificare il proprio indirizzo di posta elettronica nel campo **A**, `Testing a customized free text justification prompt` nel campo **Oggetto** e quindi inviare il messaggio di posta elettronica.
    
        Viene visualizzata la finestra popup di giustificazione, questa volta con il testo personalizzato. Ad esempio: 

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify-custom.png" alt-text="Richiesta di giustificazione di esempio con richiesta in formato di testo libero personalizzata":::
        
## <a name="block-users-from-sending-unlabeled-powerpoint-messages"></a>Impedire agli utenti di inviare messaggi di PowerPoint senza etichetta

Questa procedura descrive come impedire agli utenti di inviare file di PowerPoint senza etichetta da Outlook.

1. Nel computer client eseguire PowerShell come amministratore.

1. Per impedire l'invio di contenuto senza etichetta da Outlook, sostituire **Global** con il nome del criterio specifico ed eseguire:

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Block"}
    ```

1. Per limitare il comportamento di blocco solo a specifici tipi di file di PowerPoint, sostituire **Global** con il nome del criterio specifico ed eseguire:

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.POTX,.POTM,.POT,.PPTX"}
    ```

1. Testare l'impostazione in Outlook:

    1. Nel computer client aprire PowerPoint e creare un nuovo file con estensione **pptx**, assicurandosi di lasciare il file senza etichetta.

    1. Aprire o riavviare Outlook per eseguire il pull delle impostazioni aggiornate.
    
    1. Allegare il file di PowerPoint senza etichetta a un nuovo messaggio di Outlook.

    1. Specificare il proprio indirizzo di posta elettronica nel campo **A**, `Testing sending unlabeled PowerPoint files` nel campo **Oggetto** e quindi inviare il messaggio di posta elettronica.
    
        Outlook blocca l'invio del messaggio di posta elettronica e visualizza il messaggio seguente:

        :::image type="content" source="media/qs-tutor/ul-see-blockmessage.png" alt-text="Messaggio di blocco di esempio per un allegato di PowerPoint senza etichetta":::

Continuare con [Personalizzare il messaggio di blocco per i messaggi di PowerPoint senza etichetta](#customize-the-block-message-for-unlabeled-powerpoint-messages).

## <a name="customize-the-block-message-for-unlabeled-powerpoint-messages"></a>Personalizzare il messaggio di blocco per i messaggi di PowerPoint senza etichetta

Questa procedura descrive come personalizzare il messaggio visualizzato quando un utente tenta di inviare un file di PowerPoint senza etichetta a utenti esterni.

> [!IMPORTANT]
> Questa procedura sostituisce le impostazioni già definite usando la proprietà avanzata **OutlookUnlabeledCollaborationAction** e viene visualizzata solo per gli scopi dell'esercitazione.
>
> In ambiente di produzione è consigliabile evitare complicazioni usando la proprietà avanzata **OutlookUnlabeledCollaborationAction** per definire le regole, *o* definendo regole complesse con un file JSON come definito di seguito, ma non entrambi.
>

**Per definire la regola usando un file JSON**:

1. Creare un file **JSON** denominato **OutlookCollaborationRule_1.json** con il codice seguente:

    ```JSON
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
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".PPTX",
                                    ".PPTM",
                                    ".POTX",
                                    ".POTM",
                                    ".POT",
                                    ".PPTX"
                                 ]
                    
                },
                {                   
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "Sending PowerPoint files to external recipients requires that you label your files so that we can classify and protect Contoso content.<br><br>List of attachments that are not labeled:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>Label your document and send it again."              
                },          
            },          
            "DefaultLanguage": "en-us"      
        }   
      ] 
    }
    ```
1. Salvare il file **OutlookCollaborationRule_1.json** in una posizione accessibile dal computer client.

1. Nel computer client eseguire PowerShell come amministratore.

1. Per personalizzare il messaggio di blocco, copiare il codice seguente, sostituendo **C:\OutlookCollaborationRule_1.json** con il percorso del file JSON e **General** con il nome del criterio specifico. 

    ```PowerShell
    $filedata = Get-Content "C:\OutlookCollaborationRule_1.json”
    Set-LabelPolicy -Identity General -AdvancedSettings @{OutlookCollaborationRule_1 ="$filedata"}    
    ```

    Eseguire il codice per implementare le impostazioni definite nel file JSON.

1. Testare l'impostazione in Outlook:

    1. Nel computer client aprire PowerPoint e creare un nuovo file con estensione **pptx**, assicurandosi di lasciare il file senza etichetta.

    1. Aprire o riavviare Outlook per eseguire il pull delle impostazioni aggiornate.
    
    1. Allegare il file di PowerPoint senza etichetta a un nuovo messaggio di Outlook.

    1. Specificare il proprio indirizzo di posta elettronica nel campo **A**, `Testing customized blocking message for unlabeled PowerPoint files` nel campo **Oggetto** e quindi inviare il messaggio di posta elettronica.
    
        Outlook blocca l'invio del messaggio di posta elettronica e visualizza il messaggio seguente:

        :::image type="content" source="media/qs-tutor/ul-see-custom-blockmessage.png" alt-text="Messaggio di blocco personalizzato per i file di PowerPoint senza etichetta":::

Continuare con [Usare il registro eventi per identificare i messaggi e le azioni dell'utente per l'etichetta General](#use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label).

## <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>Usare il log eventi per identificare i messaggi e le azioni dell'utente per l'etichetta General

In questa esercitazione si è appreso come personalizzare il comportamento di AIP in Outlook per evitare alcuni tipi di oversharing, inclusi i messaggi di avviso, giustificazione e blocco. Si è visto anche come controllare il comportamento da Outlook nel computer client locale.

A questo punto è possibile avviare il Visualizzatore eventi di Windows per controllare le azioni che si sono verificate nei log.

**Per controllare gli eventi di registrazione AIP nel Visualizzatore eventi**:

Nel computer client aprire l'applicazione Visualizzatore eventi di Windows e passare a **Registri applicazioni e servizi** > **Azure Information Protection**.

Verrà visualizzato un evento informativo registrato per ogni test eseguito, inclusi i dettagli sul messaggio e la risposta dell'utente:

- **Messaggi di avviso**: ID informazioni 301
- **Messaggi di giustificazione**: ID informazioni 302
- **Messaggi di blocco**: ID informazioni 303

Ad esempio:

- [Controllare i test dei messaggi di avviso nel registro eventi](#check-the-event-log-for-your-warning-message-tests)
- [Controllare i test dei messaggi di giustificazione nel registro eventi](#check-the-event-log-for-your-justify-message-tests)
- [Controllare i test dei messaggi bloccati nel registro eventi](#check-the-event-log-for-your-block-message-tests)

### <a name="check-the-event-log-for-your-warning-message-tests"></a>Controllare i test dei messaggi di avviso nel registro eventi

Il primo test prevedeva l'invio di un messaggio di avviso all'utente e la selezione di **Annulla**. In questo caso il valore di **User Response** (Risposta utente) è **Dismissed** (Ignorato) nel primo evento 301:

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

Successivamente è stato tuttavia selezionato **Conferma e invia** e questa azione si riflette nel successivo evento 301, in cui **User Response** (Risposta utente) visualizza **Confirmed** (Confermato):

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

### <a name="check-the-event-log-for-your-justify-message-tests"></a>Controllare i test dei messaggi di giustificazione nel registro eventi

Lo stesso schema si ripete per il messaggio di giustificazione, che ha un evento 302. Il primo evento ha per **User Response** (Risposta utente) il valore **Dismissed** (Ignorato) e il secondo mostra la giustificazione selezionata. Ad esempio:

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the justification message for unlabeled content.msg
Item Name: Testing the justification message for unlabeled content
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

### <a name="check-the-event-log-for-your-block-message-tests"></a>Controllare i test dei messaggi bloccati nel registro eventi

Nella parte superiore del log eventi viene visualizzata la registrazione del messaggio di blocco, con evento 303. Ad esempio:

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing sending unlabeled PowerPoint files.msg
Item Name: Testing sending unlabeled PowerPoint files
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

## <a name="clean-up-resources"></a>Pulire le risorse

Al termine di questa esercitazione è possibile conservare i criteri di test per farvi riferimento in futuro o eliminarli per pulire le risorse.

Se si vogliono eliminare i criteri, farlo nell'interfaccia di amministrazione in cui sono stati creati, ovvero il Centro conformità di Microsoft 365, il Centro sicurezza di Microsoft 365 o il Centro sicurezza e conformità di Microsoft 365.

Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)

Dopo l'eliminazione, riavviare Outlook nel computer client in modo che non sia più configurato con le impostazioni definite in questa esercitazione.

## <a name="next-steps"></a>Passaggi successivi

Per test più rapidi, questa esercitazione ha usato un messaggio di posta elettronica per un singolo destinatario e senza allegati. 

Applicare gli stessi metodi a più destinatari ed etichette, oppure agli allegati, in cui lo stato delle etichette è talvolta meno ovvio per gli utenti.

Ad esempio, è possibile che venga visualizzato un messaggio popup nei messaggi di posta elettronica con etichetta **Pubblico**, ma che sia presente una presentazione di PowerPoint allegata con etichetta **Generale**.

Per altre informazioni sulle proprietà avanzate e sulle personalizzazioni di Outlook, vedere [Guida dell'amministratore: Configurazioni personalizzate per il client di etichettatura unificata di Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md).