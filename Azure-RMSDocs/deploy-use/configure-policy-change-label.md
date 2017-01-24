---
title: Come modificare o personalizzare un&quot;etichetta esistente | Azure Information Protection
description: "È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: ca792464e616ad08370e065a0a99405740ec1e3f


---

# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Come modificare o personalizzare un'etichetta esistente per Azure Information Protection

>*Si applica a: Azure Information Protection*

È possibile modificare o affinare qualsiasi etichetta mostrata sulla barra Information Protection configurandola nei criteri di Azure Information Protection.

Ad esempio, si può cambiare il nome, la descrizione comando, il colore e l'ordine di un'etichetta o etichetta secondaria e specificare se applica contrassegni visivi come un piè di pagina o una filigrana, se applica la protezione di Azure Rights Management e la classificazione consigliata o automatica.

Per modificare un'etichetta, seguire queste istruzioni.


1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Per modificare un'etichetta dai criteri globali in modo da essere applicata a tutti gli utenti, selezionare l'etichetta da modificare nel pannello **Criteri:Globale**, quindi apportare le modifiche nel pannello **Etichetta** ed eventualmente nei pannelli successivi. Per modificare un'etichetta da un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata agli utenti selezionati, selezionare prima di tutto il criterio nel pannello iniziale di **Azure Information Protection**.

    L'eccezione si verifica quando si vuole riordinare un'etichetta, operazione che si esegue nel pannello dei criteri dai criteri globali o da un criterio con ambito selezionato: fare clic con il pulsante destro del mouse sull'etichetta o selezionare il menu di scelta rapida per l'etichetta, quindi scegliere **Sposta su** o **Sposta giù** fino a quando l'etichetta non è nell'ordine desiderato.

3. Ogni volta che si apportano modifiche in un pannello, fare clic su **Save** (Salva) in quel pannello per mantenere le modifiche.

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

> [!TIP]
>Per ripristinare i valori predefiniti per una delle etichette predefinite, usare le informazioni fornite in [Criterio predefinito di Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


