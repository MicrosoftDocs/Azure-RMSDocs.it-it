---
title: Esercitazione per l&quot;avvio rapido - Passaggio 2 - AIP
description: Passaggio 2 dell&quot;esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell&quot;organizzazione. L&quot;esecuzione dell&quot;esercitazione richiede circa 20 minuti.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 39dfa8a1c4dabf32f8b62f08a674152f41a5b96a
ms.lasthandoff: 02/24/2017


---

# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>Passaggio 2: Configurare e pubblicare criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

Il criterio predefinito disponibile con Azure è utilizzabile senza alcuna operazione di configurazione. Tuttavia si esaminerà questo criterio e vi si apporterà qualche modifica.

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale del tenant.

2. Nel menu hub fare clic su **Nuovo** e quindi, nell'elenco **Marketplace**, selezionare **Sicurezza e identità**. Nel pannello**Sicurezza e identità**, nell'elenco **App in primo piano**, selezionare **Azure Information Protection**. Nel pannello **Azure Information Protection** fare clic su **Crea**.

    Verrà creato il pannello **Azure Information Protection** in modo che al successivo accesso al portale sarà possibile selezionare il servizio dall'elenco **More services** (Altri servizi) dell'hub. 

    > [!TIP] 
    > Selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.

3.  Nel pannello di Azure Information Protection fare clic su **Globale** e analizzare il pannello **Criteri: Globale** che illustra i criteri predefiniti di Information Protection creati automaticamente:
    
    - Etichette per la classificazione: **Personale**, **Public** (Pubblico), **Interno**, **Confidential** (Riservato) e **Secret** (Segreto). Leggere la descrizione di ognuna per comprendere l'uso a cui è destinata. Si noti che per **Secret** (Segreto) esistono due etichette secondarie: **All Company** (Tutta la società) e **My Group** (Gruppo personale). Questo è un esempio di sottocategorie di una classificazione.

    - Per impostazione predefinita, per le etichette **Interno**, **Confidential** (Riservato) e **Secret** (Segreto) sono configurati contrassegni visivi (ad esempio piè di pagina, intestazione, filigrana). Per nessuna delle etichette è impostata la protezione: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy-default-labels.png)
    
    Alcune impostazioni dei criteri globali, inoltre, non sono impostate: i documenti e i messaggi di posta elettronica non devono necessariamente avere un'etichetta, non esiste un'etichetta predefinita, gli utenti non sono obbligati a giustificare un'eventuale variazione delle etichette e il client non è configurato per un collegamento alla guida personalizzato:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-global-settings-for-a-default-template-and-prompt-for-justification"></a>Modifica delle impostazioni globali per un modello predefinito e richiesta di giustificazione

Nel corso di questa esercitazione verranno modificate alcune impostazioni dei criteri globali per scoprirne il funzionamento:

1. Impostare **Selezionare l'etichetta predefinita** su **Interno**.

2. Impostare **Gli utenti devono fornire una giustificazione per la configurazione di un'etichetta di classificazione più bassa, la rimozione di un'etichetta o la rimozione della protezione** su **On**.

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>Configurazione di un'etichetta per la protezione, di una filigrana e di una condizione per la richiesta di classificazione

Verranno ora modificate le impostazioni di una delle etichette, **Confidential** (Riservato):

1. Fare clic sull'etichetta **Confidential** (Riservato). 
    
    Nel nuovo pannello **Etichetta: Confidential** (Riservato) sono ora visibili le impostazioni disponibili per ogni etichetta. 

2. Nel pannello **Etichetta: Riservato** individuare la sezione **Set permissions for documents and emails containing this label** (Impostare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta).

    Selezionare l'opzione **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-bar.png) 
    
    Per effetto di questa operazione viene aperto il pannello **Autorizzazioni**.
    
3. Nel pannello **Autorizzazioni** verificare che le opzioni **Azure RMS** e **Seleziona modello** siano selezionate e quindi fare clic sulla casella a discesa e selezionare il modello predefinito **\<nome dell'organizzazione> - Riservato**.     
    
    Ad esempio, se il nome dell'organizzazione è VanArsdel, Ltd, verrà visualizzata la voce **VanArsdel, Ltd - Confidential** e sarà possibile selezionarla: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Impostare la protezione di Azure RMS](../media/step2-select-rms-template.png)
    
    Se questo modello di Azure Rights Management è disabilitato, selezionare un modello alternativo. Tuttavia, se si seleziona un modello di reparto, assicurarsi che l'account sia incluso nell'ambito.
    
4. Fare clic su **Fine** per salvare le modifiche e chiudere il pannello **Autorizzazioni**.

5. Nel pannello **Etichetta: Riservato** individuare la sezione **Configurare il contrassegno visivo**:
    
    Per l'opzione **I documenti con questa etichetta includono un'intestazione** fare clic su **On** e quindi, nella casella **Testo della filigrana**, digitare il nome dell'organizzazione. Ad esempio, **VanArsdel, Ltd**: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Impostare la protezione di Azure RMS](../media/step2-configure-watermark.png)
    
    Anche se è possibile modificare le dimensioni, il colore e il layout delle filigrane, per il momento verranno mantenute le impostazioni predefinite.
    
6. Individuare la sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**:
    
    Fare clic su **Add a new condition** (Aggiungi una nuova condizione) e quindi nel pannello **Condition** (Condizione) selezionare quanto segue:
    
    a. **Scegliere il tipo di condizione**: mantenere il valore **Predefinito**.
    
    b. **Seleziona predefinito**: dal menu a discesa selezionare **Numero carta di credito**.
    
    c. **Numero minimo di occorrenze**: mantenere il valore predefinito **1**.
    
    d. **Conta solo le occorrenze con valori univoci**: mantenere il valore predefinito **Off**.
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](../media/step2-configure-condition.png)
    
    Fare clic su **Salva** per tornare al pannello **Etichetta: Confidential** (Riservato).

7. Nel pannello **Etichetta: Confidential** (Riservato) **Numero carta di credito** è visualizzato come **NOME DELLA CONDIZIONE** **1** **OCCORRENZE**:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](../media/step2-see-condition.png)

8. Per **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente**: mantenere l'impostazione predefinita **Consigliata** e non modificare il suggerimento per i criteri predefiniti:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Classificazione consigliata](../media/step2-keep-recommended.png)

9. Nella casella **Immettere note per la manutenzione interna** digitare **For testing purposes only** (Solo a scopo di test):
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Digitare le note](../media/step2-type-notes.png)

10. Fare clic su **Salva** su questo pannello **Etichetta: Confidential** (Riservato). Quindi, nel pannello **Criteri: Globale** fare di nuovo clic su **Salva**.

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurazione del criterio predefinito](../media/info-protect-policy-configured.png)

11. Ora che le modifiche sono state apportate e salvate, devono essere rese disponibili agli utenti. A tale scopo, nel pannello iniziale di **Azure Information Protection** fare clic su **Publish** (Pubblica) e su **Sì** per confermare.

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

Dopo aver esaminato il criterio predefinito e aver apportato alcune modifiche, il passaggio successivo prevede l'installazione del client di Azure Information Protection.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sulle opzioni di configurazione per i criteri|[Configurazione dei criteri di Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 1](infoprotect-tutorial-step1.md)
[Passaggio 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
