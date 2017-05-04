---
title: Modificare un&quot;etichetta di Azure Information Protection
description: "È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 48faf9703176ba8f67f57582ea584733fe3e9b01
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: Azure Information Protection*

È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria e specificare se applica contrassegni visivi come un piè di pagina o una filigrana, se applica la protezione di Azure Rights Management e la classificazione consigliata o automatica.

Per modificare un'etichetta, seguire queste istruzioni.


1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Per modificare un'etichetta dai criteri globali in modo che sia applicata a tutti gli utenti, selezionare l'etichetta da modificare nel pannello **Policy: Global** (Criteri: Globale), quindi apportare le modifiche nel pannello **Label** (Etichetta) ed eventualmente nei pannelli successivi. Per modificare un'etichetta da un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata agli utenti selezionati, selezionare prima di tutto il criterio nel pannello iniziale di **Azure Information Protection**.

    L'eccezione si verifica quando si vuole riordinare un'etichetta, operazione che si esegue nel pannello dei criteri dai criteri globali o da un criterio con ambito selezionato: fare clic con il pulsante destro del mouse sull'etichetta o selezionare il menu di scelta rapida per l'etichetta, quindi scegliere **Sposta su** o **Sposta giù** fino a quando l'etichetta non è nell'ordine desiderato.

3. Ogni volta che si apportano modifiche in un pannello, fare clic su **Save** (Salva) in quel pannello per mantenere le modifiche.

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, usare le informazioni fornite in [Criterio predefinito di Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


