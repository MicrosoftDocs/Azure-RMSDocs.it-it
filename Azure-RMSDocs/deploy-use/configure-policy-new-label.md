---
title: Nuova etichetta per Azure Information Protection
description: "Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all&quot;utente sulla barra Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 602fef628f882eb79fe78b5acf89bde1721aa0ec
ms.lasthandoff: 02/24/2017


---

# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection*

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'etichetta **Secret** (Segreto) inclusa nel [criterio predefinito](configure-policy-default.md) contiene etichette secondarie.

Seguire queste istruzioni per aggiungere una nuova etichetta ai criteri di Azure Information Protection.

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se la nuova etichetta da aggiungere verrà applicata a tutti gli utenti, eseguire una delle operazioni seguenti nel pannello **Criteri:Globale**. 

    - Per creare una nuova etichetta, fare clic su **Aggiungi una nuova etichetta**.

    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Aggiungi un'etichetta secondaria**.
    
     Se la nuova etichetta da aggiungere si trova in un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata solo agli utenti selezionati, selezionare prima di tutto il criterio con ambito nel pannello iniziale di **Azure Information Protection**.

3. Nel pannello **Etichetta** o **Etichetta secondaria** selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.

    > [!NOTE]
    >Per informazioni sull'impostazione della protezione, vedere [Come configurare un'etichetta per applicare la protezione](configure-policy-protection.md).

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


