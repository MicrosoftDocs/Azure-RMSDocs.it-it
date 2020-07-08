---
title: Modificare un'etichetta di Azure Information Protection - AIP
description: È possibile modificare o affinare una qualsiasi etichetta visualizzata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e62a8086197a7e6fcd5715b9dc15e42cda72d4c9
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047746"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

È possibile modificare o affinare qualsiasi etichetta visualizzata sulla barra di Information Protection o dal pulsante **Proteggi** sulla barra multifunzione di Office configurando le etichette nel portale di Azure.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria e specificare se applica contrassegni visivi come un piè di pagina o una filigrana, nonché se applica la protezione e la classificazione consigliata o automatica.

Per modificare un'etichetta, usare le istruzioni seguenti:

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni**  >  **etichette** : nel riquadro **Azure Information Protection etichette** selezionare l'etichetta che si vuole modificare.

    L'eccezione si verifica quando si vuole riordinare un'etichetta: invece di selezionare l'etichetta, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida per l'etichetta. Selezionare quindi **Sposta su** o **Sposta giù**.

3. Quando si apportano modifiche in un nuovo riquadro, fare clic su **Salva** nel riquadro se si desidera conservare le modifiche.
    
    Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

4. Se la descrizione o il nome visualizzato dell'etichetta è stato modificato o configurato per altre lingue, esportare di nuovo i criteri di Azure Information Protection, specificare nuove traduzioni e importare le modifiche. Per altre informazioni, vedere [Come configurare etichette e modelli per varie lingue in Azure Information Protection](configure-policy-languages.md).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, vedere le informazioni in [Criteri predefiniti di Azure Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione delle opzioni disponibili per le etichette e su altre impostazioni per i criteri di Azure Information Protection, usare i collegamenti disponibili nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).



