---
title: Modificare un'etichetta di Azure Information Protection
description: "È possibile modificare o affinare una qualsiasi etichetta visualizzata sulla barra Information Protection configurandola nei criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: f1ffd4c459f2fa194372450f5713c920422f744d
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: Azure Information Protection*

È possibile modificare o affinare una qualsiasi etichetta visualizzata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria e specificare se applica contrassegni visivi come un piè di pagina o una filigrana, nonché se applica la protezione e la classificazione consigliata o automatica.

Per modificare un'etichetta, usare le istruzioni seguenti:

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza. Passare quindi al pannello **Azure Information Protection**. 
    
    Nel menu Hub, ad esempio, fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Per modificare un'etichetta nei criteri globali in modo che sia applicata a tutti gli utenti, selezionare l'etichetta da modificare nel pannello **Azure Information Protection - Criteri globali** ed eventualmente nei pannelli successivi. Per modificare un'etichetta dai [criteri con ambito](configure-policy-scope.md) in modo che venga applicata solo agli utenti selezionati, selezionare innanzitutto **Criteri con ambito** nel menu **CRITERI**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

    La procedura è diversa se si vuole riordinare un'etichetta. Nel pannello dei criteri fare clic con il pulsante destro del mouse sull'etichetta o selezionare il menu di scelta rapida relativo all'etichetta dai criteri globali o dai criteri con ambito selezionati. Selezionare quindi **Sposta su** o **Sposta giù**.

3. Ogni volta che si apportano modifiche in un pannello, fare clic su **Salva** in tale pannello se si intende mantenere le modifiche.

4. Per rendere disponibili le modifiche agli utenti, nel pannello **Azure Information Protection** fare clic su **Pubblica**.

5. Se la descrizione o il nome visualizzato dell'etichetta è stato modificato o configurato per altre lingue, esportare di nuovo i criteri di Azure Information Protection, specificare nuove traduzioni e importare le modifiche. Per altre informazioni, vedere [Come configurare etichette e modelli per varie lingue in Azure Information Protection](configure-policy-languages.md).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, vedere le informazioni in [Criteri predefiniti di Azure Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione delle opzioni disponibili per le etichette e su altre impostazioni per i criteri di Azure Information Protection, usare i collegamenti disponibili nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


