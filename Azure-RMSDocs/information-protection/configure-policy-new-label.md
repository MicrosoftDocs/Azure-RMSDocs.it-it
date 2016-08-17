---
title: Come creare una nuova etichetta per Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: c2f8f3204e3d5947137e7e9111ba4eba2628293b


---

# Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'etichetta **Secret** (Segreto) inclusa nel [criterio predefinito](configure-policy-default.md) contiene etichette secondarie.

Seguire queste istruzioni per aggiungere una nuova etichetta ai criteri di Azure Information Protection.

1. Se non è già stato fatto, accedere al [portale di Azure](https://portal.azure.com) e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** effettuare una delle operazioni seguenti:

    - Per creare una nuova etichetta, fare clic su **Aggiungi una nuova etichetta**.

    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Aggiungi un'etichetta secondaria**.

3. Nel pannello **Etichetta** o **Etichetta secondaria** selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.

    > [!NOTE]
    >Per informazioni sull'impostazione della protezione, vedere [Come configurare un'etichetta per applicare la protezione](configure-policy-protection.md).

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Aug16_HO2-->


