---
title: Modificare un'etichetta di Azure Information Protection
description: È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 9b13ad7cff8431314086882cac8ddb73ab0404ec
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39374692"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

È possibile modificare o affinare qualsiasi etichetta visualizzata sulla barra di Information Protection o dal pulsante **Proteggi** sulla barra multifunzione di Office configurando le etichette nel portale di Azure.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria. È possibile specificare se l'etichetta applica contrassegni visivi come un piè di pagina o una filigrana. È inoltre possibile specificare se l'etichetta applica la protezione e la classificazione consigliata o automatica.

Per modificare un'etichetta, seguire queste istruzioni:

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **CLASSIFICAZIONI** > **Etichette**: nel pannello **Azure Information Protection - Etichette** selezionare l'etichetta che si vuole modificare.

    L'eccezione si verifica quando si vuole riordinare un'etichetta: invece di selezionare l'etichetta, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida per l'etichetta. Selezionare quindi le opzioni **Sposta su** o **Sposta giù**.

3. Ogni volta che si apportano modifiche in un nuovo pannello, fare clic su **Salva** in quel pannello per mantenere le modifiche.
    
    Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

4. Se il nome visualizzato dell'etichetta e la descrizione sono stati modificati e configurati per le lingue aggiuntive, esportare di nuovo i criteri di Azure Information Protection, specificare nuove traduzioni e importare le modifiche. Per altre informazioni, vedere [How to configure labels for different languages](configure-policy-languages.md) (Come configurare etichette per lingue diverse).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, usare le informazioni fornite in [Criterio predefinito di Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).



