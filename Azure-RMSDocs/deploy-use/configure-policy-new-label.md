---
title: Nuova etichetta per Azure Information Protection
description: "Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: ac12ab9023499d5aac632159ef689a8f10a91418
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection*

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'ultima etichetta dei [criteri predefiniti](configure-policy-default.md) include etichette secondarie.

Seguire queste istruzioni per aggiungere una nuova etichetta ai criteri di Azure Information Protection.

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se la nuova etichetta che si vuole aggiungere verrà applicata a tutti gli utenti, eseguire una delle operazioni seguenti nel pannello **Policy: Global** (Criteri: Globale). 

    - Per creare una nuova etichetta, fare clic su **Aggiungi una nuova etichetta**.

    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Aggiungi un'etichetta secondaria**.
    
     Se la nuova etichetta da aggiungere si trova in un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata solo agli utenti selezionati, selezionare prima di tutto il criterio con ambito nel pannello iniziale di **Azure Information Protection**.

3. Nel pannello **Etichetta** o **Etichetta secondaria** selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.
    
    Si noti che alle nuove etichette viene assegnato automaticamente il colore nero. Scegliere un colore distintivo dall'elenco dei colori o immettere un codice tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, **#DAA520**. Se è necessario un riferimento per questi codici, un utile punto di partenza è costituito dall'articolo [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85) (Colori per nome) disponibile nella documentazione MSDN; inoltre, questi codici sono presenti in molti programmi di modifica delle immagini, come Microsoft Paint, in cui scegliendo un colore personalizzato da una tavolozza vengono visualizzati automaticamente i valori RGB.

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

5. Per visualizzare il nuovo nome di etichetta e la descrizione in lingue diverse per gli utenti, seguire le procedure descritte in [How to configure labels for different languages](configure-policy-languages.md) (Come configurare le etichette per lingue diverse). 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

