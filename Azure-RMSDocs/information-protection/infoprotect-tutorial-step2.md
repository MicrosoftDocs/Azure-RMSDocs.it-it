---
title: Esercitazione introduttiva di Azure Information Protection, passaggio 2 | Azure Information Protection
description: "Passaggio 2 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in meno di 15 minuti."
author: cabailey
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: ba0f05619e1d13e16b8d4f6d86231b89e9326726
ms.openlocfilehash: 9dfbeb4c887c619d07b11be0da304ac4f4e7d4a9


---

# Passaggio 2: Configurare e pubblicare criteri di Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Il criterio predefinito disponibile con Azure è utilizzabile senza alcuna operazione di configurazione. Tuttavia si esaminerà questo criterio e vi si apporterà qualche modifica.

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com). Se si vuole testare la protezione nonché la classificazione e l'applicazione di etichette, accedere come amministratore globale in modo da recuperare i modelli di Azure Rights Management.
 
2. Nel menu hub: fare clic su **Nuovo** > **Sicurezza e identità** > **Azure Information Protection (anteprima)** > **Crea**.

    Verrà creato il pannello **Azure Information Protection** in modo che al successivo accesso al portale sarà possibile selezionare il servizio dall'elenco **More services** (Altri servizi) dell'hub. 

    > [!TIP] 
    > Selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.

3.  Analizzare il pannello **Azure Information Protection** principale che illustra il criterio di Information Protection creato automaticamente:
    
    - Etichette per la classificazione: **Personal** (Personale), **Public** (Pubblico), **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto). Leggere la descrizione di ognuna per comprendere l'uso a cui è destinata. Si noti che per **Secret** (Segreto) esistono due etichette secondarie: **All Company** (Tutta la società) e **My Group** (Gruppo personale). Questo è un esempio di sottocategorie di una classificazione.

    - Per impostazione predefinita, per le etichette **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto) sono configurati contrassegni visivi (ad esempio piè di pagina, intestazione, filigrana). Per nessuna delle etichette è impostata la protezione. Le tre impostazioni globali, poi, non sono impostate. I documenti e i messaggi di posta elettronica non devono quindi necessariamente avere un'etichetta. Non esiste un'etichetta predefinita e gli utenti non sono obbligati a giustificare un eventuale abbassamento del livello di classificazione.

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy.png)

Nel corso di questa esercitazione verranno modificate alcune impostazioni globali per scoprirne il funzionamento:

-  **Select the default label** (Selezionare l'etichetta predefinita): selezionare **Internal** (Interno).

- **Users must provide justification to set a lower classification label, remove a label, or remove protection. **. (Gli utenti sono obbligati a giustificare un abbassamento del livello di classificazione, la rimozione di un'etichetta o la rimozione della protezione). Impostare su **On** (On).

Verranno ora modificate le impostazioni di una delle etichette, **Confidential** (Riservato):

1. Fare clic sull'etichetta **Confidential** (Riservato).

2. Nel pannello **Label: Confidential** (Etichetta: Riservato) sono ora visibili le impostazioni disponibili per ogni etichetta. Apportare le modifiche seguenti:

    a. Se Azure Rights Management è attivato: nella sezione **Configurare il modello RMS per la protezione di documenti e messaggi di posta elettronica contenenti questa etichetta** per **Selezionare il modello RMS da**, mantenere il valore predefinito **Azure RMS**. Quindi, per **Select RMS template** (Selezionare il modello RMS), fare clic sull'elenco a discesa e selezionare il modello predefinito **\<Nome organizzazione> - Confidential** (Riservato). Ad esempio, se il nome dell'organizzazione è VanArsdel, Ltd, verrà visualizzata la voce **VanArsdel, Ltd - Confidential** e sarà possibile selezionarla. Se questo modello di Azure Rights Management è disabilitato, selezionare un modello alternativo. Tuttavia, se si seleziona un modello di reparto, assicurarsi che l'account sia incluso nell'ambito.
    
    Se Azure Rights Management non è attivato, non è possibile usare questa opzione.
    
    b. **Documents with this label have a watermark** (I documenti con questa etichetta hanno una filigrana): fare clic su **On** e nella casella **Watermark Text** (Testo della filigrana) digitare il nome dell'organizzazione. Ad esempio, **VanArsdel, Ltd**. 
    
    c. Fare clic su **Add a new condition** (Aggiungi una nuova condizione) e quindi nel pannello **Condition** (Condizione) selezionare quanto segue:
    
    - **Choose the type of condition** (Scegliere il tipo di condizione): **Built-in** (Predefinita)
    
    - **Select built-in** (Selezionare tipo predefinito): **Credit Card Number** (N. carta di credito)
    
    - **Minimum number of occurrences** (Numero minimo di occorrenze): **1**
    
    - **Conta solo le occorrenze con valori univoci**: **Sì**
    
    - Fare clic su **Save** (Salva) per tornare al pannello **Label: Confidential** (Etichetta: Riservato).

3. Nel pannello **Label: Confidential** (Etichetta: Riservato) **Credit Card Number** (N. carta di credito) è visualizzato come **CONDITION NAME** (NOME CONDIZIONE) **1** **OCCURRENCES** (OCCORRENZE).

4. Lasciare **Select how this label is applied** (Selezionare come applicare l'etichetta) impostato su **Recommended** (Consigliata)

5. Nella casella **Enter notes for internal housekeeping** (Note per la gestione interna) digitare **For testing purposes only** (Solo a scopo di test).

6. Fare clic su **Save** (Salva) nel pannello **Label: Confidential** (Etichetta: Riservato) e nel pannello principale **Azure Information Protection** fare di nuovo clic su **Save** (Salva).

7. Ora che le modifiche sono state apportate e salvate, devono essere rese disponibili agli utenti. A tale scopo fare clic su **Publish** (Pubblica) e su **Sì** per confermare.

![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurazione del criterio predefinito](../media/info-protect-policy-configured.png)

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

Dopo aver esaminato il criterio predefinito e aver apportato alcune modifiche, il passaggio successivo prevede l'installazione del client di Azure Information Protection.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sulle opzioni di configurazione per i criteri|[Configurazione dei criteri di Azure Information Protection](configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 1](infoprotect-tutorial-step1.md)
[Passaggio 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Sep16_HO3-->

