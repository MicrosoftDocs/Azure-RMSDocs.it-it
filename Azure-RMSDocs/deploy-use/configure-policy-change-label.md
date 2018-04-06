---
title: Modificare un'etichetta di Azure Information Protection
description: È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: aac1d87fb76848e31a21a046f14442293d29aa9f
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria. È possibile specificare se l'etichetta applica contrassegni visivi come un piè di pagina o una filigrana. È inoltre possibile specificare se l'etichetta applica la protezione e la classificazione consigliata o automatica.

Per modificare un'etichetta, seguire queste istruzioni:

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Per modificare un'etichetta nei criteri globali in modo che sia applicata a tutti gli utenti, selezionare l'etichetta da modificare nel pannello **Azure Information Protection - Criteri globali** ed eventualmente nei pannelli successivi. Per modificare un'etichetta nei [criteri con ambito](configure-policy-scope.md) in modo che sia applicata solo agli utenti selezionati, per prima cosa selezionare **Criteri con ambito** nel menu **CRITERI**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

    L'eccezione si verifica quando si vuole riordinare un'etichetta. Nel pannello dei criteri dai criteri globali o da un criterio con ambito selezionato fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida per l'etichetta. Selezionare quindi le opzioni **Sposta su** o **Sposta giù**.

3. Ogni volta che si apportano modifiche in un pannello, fare clic su **Save** (Salva) in quel pannello per mantenere le modifiche.

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

5. Se il nome visualizzato dell'etichetta e la descrizione sono stati modificati e configurati per le lingue aggiuntive, esportare di nuovo i criteri di Azure Information Protection, specificare nuove traduzioni e importare le modifiche. Per altre informazioni, vedere [How to configure labels for different languages](configure-policy-languages.md) (Come configurare etichette per lingue diverse).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, usare le informazioni fornite in [Criterio predefinito di Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


