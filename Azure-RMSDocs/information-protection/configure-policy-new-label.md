---
title: Come creare una nuova etichetta per Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 26f22fb616f66332abf87501f782f1f8e8f0c013


---

# Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'etichetta **Secret** (Segreto) inclusa nel [criterio predefinito](configure-policy-default.md) contiene etichette secondarie.

Seguire queste istruzioni per aggiungere una nuova etichetta ai criteri di Azure Information Protection.

1. Accedere al [portale di Azure](https://portal.azure.com).
 
2. Nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

3. Nel pannello **Azure Information Protection** effettuare una delle operazioni seguenti:

    - Per creare una nuova etichetta, fare clic su **Add a new label** (Aggiungi nuova etichetta).

    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Add a sub-label** (Aggiungi etichetta secondaria).

4. Nel pannello **Label** (Etichetta) o **Sub-label** (Etichetta secondaria) selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Save** (Salva).

    > [!NOTE]
    >Per informazioni sull'impostazione della protezione, vedere [Come configurare un'etichetta per applicare la protezione](configure-policy-protection.md).

5. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Jul16_HO5-->


