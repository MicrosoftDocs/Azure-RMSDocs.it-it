---
title: Come configurare le impostazioni dei criteri globali per Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 3b22cf76f03a4d36281db7e705359402dcbbde0e


---

# Come configurare le impostazioni dei criteri globali per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Nei criteri di Azure Information Protection sono disponibili 3 impostazioni valide per tutti gli utenti e tutti i dispositivi:

![Impostazioni globali dei criteri di Azure Information Protection](../media/info-protect-policy-settings.png)


Per configurare queste impostazioni:

1. Accedere al [portale di Azure](https://portal.azure.com).
 
2. Nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

3. Nel pannello **Azure Information Protection** configurare queste impostazioni globali:

    - **All documents and emails must have a label** (Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta): quando si imposta questa opzione su **Sì**, a tutti i documenti e messaggi di posta elettronica inviati deve essere applicata un'etichetta. L'etichetta può essere assegnata manualmente da un utente, automaticamente o come risultato di una [condizione](configure-policy-classification.md) oppure per impostazione predefinita selezionando l'opzione **Select the default label** (Selezionare l'etichetta predefinita). 

    Se al momento del salvataggio di un documento o dell'invio di un messaggio di posta elettronica non è assegnata un'etichetta, all'utente viene chiesto di selezionarne una:

    ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](../media/info-protect-enforce-label.png)

    - **Select the default label** (Selezionare l'etichetta predefinita): quando si seleziona questa opzione, selezionare l'etichetta da assegnare ai documenti e ai messaggi di posta elettronica che non hanno un'etichetta. Non è possibile impostare un'etichetta come predefinita se contiene etichette secondarie. 

    - **Users must provide justification when lowering the sensitivity level** (Gli utenti devono giustificare l'abbassamento del livello di riservatezza): quando si imposta questa opzione su **Sì** e un utente cambia l'etichetta di un documento o messaggio di posta elettronica esistente applicando un'etichetta con un livello di riservatezza inferiore, ad esempio da **Secret** (Segreto) a **Public**, all'utente viene richiesto di motivare questa azione. L'utente può ad esempio spiegare che il documento non contiene informazioni riservate. L'azione e la relativa giustificazione vengono registrati nel registro eventi di Windows locale: **Application** > **Microsoft Azure Information Protection**.  

    ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](../media/info-protect-lower-justification.png)

    Questa opzione non è applicabile alle etichette secondarie.

4. Fare clic su **Save** (Salva) per salvare le modifiche.

5. Per mettere le modifiche a disposizione degli utenti, fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  












<!--HONumber=Jul16_HO5-->


