---
title: Come configurare le impostazioni dei criteri globali per Azure Information Protection | Azure Information Protection
description: Nei criteri di Azure Information Protection sono disponibili 3 impostazioni valide per tutti gli utenti e tutti i dispositivi.
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: 872ea7da6f3b72a355a73c8b0589beda86ded20d


---

# Come configurare le impostazioni dei criteri globali per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Nei criteri di Azure Information Protection sono disponibili 3 impostazioni valide per tutti gli utenti e tutti i dispositivi:

![Impostazioni globali dei criteri di Azure Information Protection](../media/info-protect-policy-settings.png)


Per configurare queste impostazioni:

1. Se non è già stato fatto, accedere al [portale di Azure](https://portal.azure.com) e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** configurare queste impostazioni globali:

    - **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**: quando si imposta questa opzione su **Sì**, a tutti i documenti e messaggi di posta elettronica inviati deve essere applicata un'etichetta. L'etichetta può essere assegnata manualmente da un utente, automaticamente o come risultato di una [condizione](configure-policy-classification.md) oppure per impostazione predefinita selezionando l'opzione **Selezionare l'etichetta predefinita**. 

    Se al momento del salvataggio di un documento o dell'invio di un messaggio di posta elettronica non è assegnata un'etichetta, all'utente viene chiesto di selezionarne una:

    ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](../media/info-protect-enforce-label.png)

    - **Selezionare l'etichetta predefinita**: quando si seleziona questa opzione, selezionare l'etichetta da assegnare ai documenti e ai messaggi di posta elettronica che non hanno un'etichetta. Non è possibile impostare un'etichetta come predefinita se contiene etichette secondarie. 

    - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Gli utenti sono obbligati a giustificare un abbassamento del livello di classificazione dell'etichetta, la rimozione di un'etichetta o la rimozione della protezione). Quando l'opzione viene impostata su **On** (On) e viene eseguita un'azione qualsiasi, ad esempio viene modificata l'etichetta **Segret** (Segreto) in **Personal** (Personale), all'utente viene chiesto di dare una spiegazione per questa azione. L'utente può ad esempio spiegare che il documento non contiene informazioni riservate. L'azione e la relativa giustificazione vengono registrati nel registro eventi di Windows locale: **Application** > **Microsoft Azure Information Protection**.  

    ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](../media/info-protect-lower-justification.png)

    Questa opzione non è applicabile alle etichette secondarie.

3. Fare clic su **Save** (Salva) per salvare le modifiche.

4. Per mettere le modifiche a disposizione degli utenti, fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  












<!--HONumber=Sep16_HO1-->


