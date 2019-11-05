---
title: Modificare un'etichetta di Azure Information Protection - AIP
description: È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 8cf449b26ced29b57a51dc6657105805bafbd9fe
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559262"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

È possibile modificare o affinare qualsiasi etichetta visualizzata sulla barra di Information Protection o dal pulsante **Proteggi** sulla barra multifunzione di Office configurando le etichette nel portale di Azure.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria. È possibile specificare se l'etichetta applica contrassegni visivi come un piè di pagina o una filigrana. È inoltre possibile specificare se l'etichetta applica la protezione e la classificazione consigliata o automatica.

Per modificare un'etichetta, seguire queste istruzioni:

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Passare quindi al riquadro **Azure Information Protection** . 
    
    Ad esempio, nella casella di ricerca per risorse, servizi e documenti: iniziare a digitare **informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni** > **etichette** : nel riquadro **etichette Azure Information Protection** selezionare l'etichetta che si desidera modificare.

    L'eccezione si verifica quando si vuole riordinare un'etichetta: invece di selezionare l'etichetta, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida per l'etichetta. Selezionare quindi le opzioni **Sposta su** o **Sposta giù**.

3. Quando si apportano modifiche in un nuovo riquadro, fare clic su **Salva** nel riquadro se si desidera conservare le modifiche.
    
    Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

4. Se il nome visualizzato dell'etichetta e la descrizione sono stati modificati e configurati per le lingue aggiuntive, esportare di nuovo i criteri di Azure Information Protection, specificare nuove traduzioni e importare le modifiche. Per altre informazioni, vedere [How to configure labels for different languages](configure-policy-languages.md) (Come configurare etichette per lingue diverse).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, usare le informazioni fornite in [Criterio predefinito di Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).



