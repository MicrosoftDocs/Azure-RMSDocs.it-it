---
title: Nuova etichetta per Azure Information Protection
description: "Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 8628fa5b17659a49ff9f63ae6dad32f073e8ced6
ms.sourcegitcommit: 240378d216e386ad760460c50b7a664099c669e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2018
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: Azure Information Protection*

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'ultima etichetta dei [criteri predefiniti](configure-policy-default.md) include etichette secondarie.

Quando si crea la prima etichetta secondaria per un'etichetta, gli utenti non possono più selezionare l'etichetta padre originale. Se necessario, creare una nuova etichetta secondaria per ricreare le impostazioni dell'etichetta padre in modo che gli utenti possano applicare le stesse impostazioni.

Seguire queste istruzioni per aggiungere una nuova etichetta ai criteri di Azure Information Protection.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se l'etichetta da aggiungere è destinata a tutti gli utenti, restare nel pannello **Azure Information Protection - Criteri globali**.
    
    Se l'etichetta da aggiungere è destinata a utenti selezionati in [criteri con ambito](configure-policy-scope.md), nel menu **CRITERI** selezionare **Criteri con ambito**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

3. Nel pannello **Azure Information Protection - Criteri globali** o nel pannello **Criteri:\<nome>** eseguire una delle operazioni seguenti:
    
    - Per creare una nuova etichetta, fare clic su **Aggiungi una nuova etichetta**.
    
    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Aggiungi un'etichetta secondaria**.

4. Nel pannello **Etichetta** o **Etichetta secondaria** selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.
    
    Si noti che alle nuove etichette viene assegnato automaticamente il colore nero. Scegliere un colore distintivo dall'elenco dei colori o immettere un codice tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, **#DAA520**. Se è necessario un riferimento per questi codici, un utile punto di partenza è l'articolo [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx) (Colori per nome), disponibile nella documentazione MSDN; questi codici sono anche presenti in molti programmi di modifica immagini, come Microsoft Paint, in cui scegliendo un colore personalizzato da una tavolozza vengono visualizzati automaticamente i valori RGB.

5. Per mettere le modifiche a disposizione degli utenti, nel pannello iniziale di **Azure Information Protection** fare clic su **Publish** (Pubblica).

6. Per visualizzare il nuovo nome di etichetta e la descrizione in lingue diverse per gli utenti, seguire le procedure descritte in [How to configure labels for different languages](configure-policy-languages.md) (Come configurare le etichette per lingue diverse). 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

