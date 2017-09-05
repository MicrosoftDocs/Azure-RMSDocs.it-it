---
title: Eliminare o riordinare un'etichetta per Azure Information Protection
description: "È possibile eliminare o riordinare le etichette mostrate sulla barra Information Protection configurandole nel criterio di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: 2d11eb649ecec835d2ddf0045d8672c5b45af95f
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Come eliminare o riordinare un'etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection*

È possibile eliminare o riordinare le etichette mostrate sulla barra Information Protection configurandole nel criterio di Azure Information Protection.

![Eliminare o riordinare le etichette nel criterio di Azure Information Protection](../media/info-protect-contextmenu.png)

Quando si elimina un'etichetta che è stata applicata a documenti e messaggi di posta elettronica e si pubblica il criterio di Azure Information Protection, l'etichetta viene rimossa automaticamente dai documenti o messaggi di posta elettronica quando vengono successivamente aperti dal client Azure Information Protection.

Prima di eliminare un'etichetta, valutarne la disabilitazione in alternativa. Quando si disabilita un'etichetta applicata a documenti e messaggi di posta elettronica, l'etichetta applicata non verrà rimossa da questi documenti e messaggi di posta elettronica, ma non sarà più visualizzata come etichetta selezionabile dagli utenti nella barra di Information Protection. La disabilitazione di un'etichetta consente anche di mantenere la configurazione originale nel caso si voglia consentire agli utenti di selezionare l'etichetta in un secondo momento, quando sarà sufficiente riabilitarla.

Ordinare le etichette in modo che gli utenti le vedano in una progressione logica sulla barra Information Protection. Ad esempio, ordinare le etichette per livello crescente di riservatezza, in modo che l'etichetta della minima riservatezza venga mostrata per prima e quella della massima riservatezza per ultima. I [criteri predefiniti](configure-policy-default.md) usano questa configurazione e riflettono la riservatezza sempre maggiore nei nomi di etichetta.

> [!IMPORTANT]
>Se si configurano [condizioni](configure-policy-classification.md) che potrebbero riguardare più etichette, è necessario ordinare le etichette dalla minima alla massima riservatezza. Questo ordinamento garantisce che venga applicata l'etichetta della massima riservatezza quando vengono valutate le condizioni.


Per apportare le modifiche, seguire queste istruzioni.

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza. Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se l'etichetta da configurare viene applicata a tutti gli utenti, restare nel pannello **Azure Information Protection - Criteri globali**.
    
    Se l'etichetta da configurare si trova in un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata solo agli utenti selezionati, nel menu **CRITERI** selezionare **Criteri con ambito**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

3. Nel pannello **Azure Information Protection - Criteri globali** o nel pannello **Criteri:\<nome>**, eseguire una o più delle operazioni seguenti. 

    - Per eliminare un'etichetta: fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta che si vuole eliminare, scegliere **Elimina questa etichetta** e fare clic su **Sì** per confermare. Fare clic su **Save** (Salva). 

    - Per disabilitare un'etichetta: selezionare l'etichetta che si vuole disabilitare. Nel pannello **Etichetta** per **Abilitato** fare clic su **No**fare clic su **Salva**.

    - Per riordinare un'etichetta: fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta che si vuole riordinare, scegliere **Sposta su** o **Sposta giù** fino a quando l'etichetta non è nell'ordine desiderato. Fare clic su **Save** (Salva). 

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

