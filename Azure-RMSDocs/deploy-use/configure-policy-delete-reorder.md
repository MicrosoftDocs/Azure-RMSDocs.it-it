---
title: Come eliminare o riordinare un'etichetta | Azure Information Protection
description: "È possibile eliminare o riordinare le etichette mostrate sulla barra Information Protection configurandole nel criterio di Azure Information Protection."
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: ebb11148718f22c79bb49c82b9855f5e6f2a5b18
ms.openlocfilehash: 3e73e928c8a0189c275e02c189db5c872993d9dd


---

# Come eliminare o riordinare un'etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection*

È possibile eliminare o riordinare le etichette mostrate sulla barra Information Protection configurandole nel criterio di Azure Information Protection.

![Eliminare o riordinare le etichette nel criterio di Azure Information Protection](../media/info-protect-contextmenu.png)

Anziché eliminare un'etichetta, può essere sufficiente disabilitarla se si vuole mantenerne la configurazione ma impedire che l'etichetta venga visualizzata sulla barra Information Protection.

Ordinare le etichette in modo che gli utenti le vedano in una progressione logica sulla barra Information Protection. Ad esempio, ordinare le etichette per livello crescente di riservatezza, in modo che l'etichetta della minima riservatezza venga mostrata per prima e quella della massima riservatezza per ultima. Il [criterio predefinito](configure-policy-default.md) usa questa configurazione.

> [!IMPORTANT]
>Se si configurano [condizioni](configure-policy-classification.md) che potrebbero riguardare più etichette, è necessario ordinare le etichette dalla minima alla massima riservatezza. Questo ordinamento garantisce che venga applicata l'etichetta della massima riservatezza quando vengono valutate le condizioni.


Per apportare le modifiche, seguire queste istruzioni.

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** eseguire una delle azioni seguenti a seconda dell'operazione da eseguire, ovvero eliminare, disabilitare o riordinare un'etichetta:

    - Per eliminare un'etichetta: fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta che si vuole eliminare, scegliere **Elimina questa etichetta** e fare clic su **Sì** per confermare. Fare clic su **Save** (Salva). 

    - Per disabilitare un'etichetta: selezionare l'etichetta che si vuole disabilitare. Nel pannello **Etichetta** per **Abilitato** fare clic su **No**fare clic su **Salva**.

    - Per riordinare un'etichetta: fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta che si vuole riordinare, scegliere **Sposta su** o **Sposta giù** fino a quando l'etichetta non è nell'ordine desiderato. Fare clic su **Save** (Salva). 

3. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Sep16_HO4-->

