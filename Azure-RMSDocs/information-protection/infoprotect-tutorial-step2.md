---
title: Esercitazione introduttiva di Azure Information Protection, passaggio 2 | Azure Rights Management
description: "Passaggio 2 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in meno di 15 minuti."
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 463c0bc1fa86f73e2623faf5a624afeabcadeedb
ms.openlocfilehash: c6ecf22b72d862c605f8be2ab1f75fd2126f8575


---

# Passaggio 2: Configurare e pubblicare criteri di Azure Information Protection

*Si applica a: Azure Information Protection (anteprima)*

Il criterio predefinito disponibile con Azure è utilizzabile senza alcuna operazione di configurazione. Tuttavia si esaminerà questo criterio e vi si apporterà qualche modifica.

1. Accedere al portale di Azure tramite questo collegamento speciale per Azure Information Protection: https://portal.azure.com/?microsoft_azure_informationprotection=true
 
2. Nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

- Verrà visualizzato il pannello **Azure Information Protection** con il criterio di Information Protection creato automaticamente. Il criterio predefinito contiene le seguenti etichette per la classificazione: **Personal** (Personale), **Public** (Pubblico), **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto). Leggere la descrizione di ognuna per comprendere l'uso a cui è destinata. Si noti che per **Secret** (Segreto) esistono due etichette secondarie: **All Company** (Tutta la società) e **My Group** (Gruppo personale). Questo è un esempio di sottocategorie di una classificazione.

- Per le impostazioni predefinite **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto) sono configurati contrassegni visivi (ad esempio piè di pagina, intestazione, filigrana). Per nessuna delle etichette è impostata la protezione. Le tre impostazioni globali, poi, non sono impostate. I documenti e i messaggi di posta elettronica non devono quindi necessariamente avere un'etichetta. Non esiste un'etichetta predefinita e gli utenti non sono obbligati a giustificare un eventuale abbassamento del livello di riservatezza.

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy.png)

Nel corso di questa esercitazione verranno modificate alcune impostazioni globali per scoprirne il funzionamento:

-  **Select the default label** (Selezionare l'etichetta predefinita): selezionare **Internal** (Interno).

- **Users must provide justification when lowering the sensitivity level** (Gli utenti devono giustificare l'abbassamento del livello di riservatezza): selezionare **On**.

Verranno ora modificate le impostazioni di una delle etichette, **Confidential** (Riservato):

1. Fare clic sulla voce dell'etichetta **Confidential** (Riservato).

2. Nel pannello **Label: Confidential** (Etichetta: Riservato) sono ora visibili le impostazioni disponibili per ogni etichetta. Apportare le modifiche seguenti:

    a. Se Azure Rights Managment è attivato, per **Select RMS template** (Selezionare il modello RMS) fare clic sull'elenco a discesa e selezionare il modello predefinito **\<Nome organizzazione> - Confidential** (Riservato). Ad esempio, se il nome dell'organizzazione è VanArsdel, Ltd, verrà visualizzata la voce **VanArsdel, Ltd - Confidential** e sarà possibile selezionarla. Se questo modello di Azure Rights Management è disabilitato, selezionare un modello alternativo. Tuttavia, se si seleziona un modello di reparto, assicurarsi che l'account sia incluso nell'ambito.

    Se Azure Rights Management non è attivato, non è possibile usare questa opzione.

    b. **Documents with this label have a watermark** (I documenti con questa etichetta hanno una filigrana): fare clic su **On** e nella casella **Watermark Text** (Testo della filigrana) digitare il nome dell'organizzazione. Ad esempio, **VanArsdel, Ltd**. 

    c. Fare clic su **Add a new condition** (Aggiungi una nuova condizione) e quindi nel pannello **Condition** (Condizione) selezionare quanto segue:

    - **Choose the type of condition** (Scegliere il tipo di condizione): **Built-in** (Predefinita)

    - **Select built-in** (Selezionare tipo predefinito): **Credit Card Number** (N. carta di credito)

    - **Minimum number of occurrences** (Numero minimo di occorrenze): **1**

    - Fare clic su **Save** (Salva) per tornare al pannello **Label: Confidential** (Etichetta: Riservato).

3. Nel pannello **Label: Confidential** (Etichetta: Riservato) **Credit Card Number** (N. carta di credito) è visualizzato come **CONDITION NAME** (NOME CONDIZIONE) **1** **OCCURRENCES** (OCCORRENZE).

4. Lasciare **Select how this label is applied** (Selezionare come applicare l'etichetta) impostato su **Recommended** (Consigliata)

5. Nella casella **Enter notes for internal housekeeping** (Note per la gestione interna) digitare **For testing purposes only** (Solo a scopo di test).

6. Fare clic su **Save** (Salva) nel pannello **Label: Confidential** (Etichetta: Riservato) e nel pannello principale **Azure Information Protection** fare di nuovo clic su **Save** (Salva).

7. Ora che le modifiche sono state apportate e salvate, devono essere rese disponibili agli utenti. A tale scopo fare clic su **Publish** (Pubblica) e su **Sì** per confermare.

![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurazione del criterio predefinito](../media/info-protect-policy-configured.png)

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

Dopo aver esaminato il criterio predefinito e aver apportato alcune modifiche, il passaggio successivo prevede l'installazione del client di Azure Information Protection.


>[!div class="step-by-step"]
[&#171; Passaggio 1](infoprotect-tutorial-step1.md)
[Passaggio 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Jul16_HO3-->


