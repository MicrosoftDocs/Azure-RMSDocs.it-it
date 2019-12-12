---
title: Eliminare o riordinare un'etichetta per Azure Information Protection - AIP
description: È possibile eliminare o riordinare le etichette di Azure Information Protection visualizzate dagli utenti.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: cd38bef41bd2e1d0f422958c150ad06eba1793b9
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935062"
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Come eliminare o riordinare un'etichetta per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

È possibile eliminare o riordinare le etichette di Azure Information Protection che gli utenti vedono nelle applicazioni di Office selezionando le azioni corrispondenti per le etichette.

![Eliminare o riordinare le etichette nel criterio di Azure Information Protection](./media/info-protect-contextmenu.png)

Quando si elimina un'etichetta applicata a documenti e messaggi di posta elettronica, alla successiva apertura di tali documenti e massaggi da parte del client di Azure Information Protection gli utenti vedranno lo stato dell'etichetta come **Non impostato**. Tuttavia, le informazioni dell'etichetta restano nei metadati e possono ancora essere lette dai servizi che cercano queste informazioni di etichetta.

Inoltre, se l'etichetta eliminata applicava la protezione, la protezione non viene rimossa. Le impostazioni di protezione dall'etichetta vengono mantenute e visualizzate nella sezione **Modelli di protezione**. Ora il modello può essere convertito in una nuova etichetta. Sebbene il modello venga mantenuto, non è possibile creare una nuova etichetta con lo stesso nome dell'etichetta eliminata. Se si vuole eseguire questa operazione, sono disponibili le opzioni seguenti:

- Convertire il modello in un'etichetta. 
    
    Questa azione è consigliata perché, se necessario, è possibile cambiare il nome del modello e modificare le impostazioni di protezione.

- Usare PowerShell per rinominare il modello o eliminarlo.
    
    Prima di eseguire queste azioni, valutare se altri amministratori o servizi usano il modello o lo hanno usato in passato. È possibile identificare il modello dal relativo ID di modello che non cambia o dal nome (che può essere modificato). Come procedura consigliata, eliminare un modello solo se gli utenti sicuramente non dovranno aprire documenti o messaggi di posta elettronica protetti dal modello.

Per altre informazioni sulla gestione dei modelli di protezione, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

Prima di eliminare un'etichetta, valutare piuttosto la possibilità di disabilitarla o rimuoverla dal criterio:
    
- Quando si disabilita un'etichetta applicata a documenti e messaggi di posta elettronica, l'etichetta non viene rimossa da questi documenti e messaggi. Quello che accade è che rimane nel criterio, ma non viene più visualizzata come un'etichetta che gli utenti possono selezionare sulla barra di Information Protection. La disabilitazione di un'etichetta consente di mantenere la configurazione originale nel caso si voglia consentire agli utenti nello stesso criterio di selezionare l'etichetta in un secondo momento, quando sarà sufficiente riabilitarla.

- Inoltre, quando si rimuove un'etichetta da un criterio, l'etichetta applicata non viene rimossa da questi documenti e messaggi di posta elettronica. Quando però si rimuove l'etichetta dal criterio, diventa disponibile per essere aggiunta a un altro criterio. Per altre informazioni, vedere [Aggiungere o rimuovere un'etichetta a o da un criterio di Azure Information Protection](configure-policy-add-remove-label.md).

Ordinare le etichette in modo che gli utenti le vedano in una progressione logica sulla barra Information Protection. Ad esempio, ordinare le etichette per livello crescente di riservatezza, in modo che l'etichetta della minima riservatezza venga mostrata per prima e quella della massima riservatezza per ultima. I [criteri predefiniti](configure-policy-default.md) usano questa configurazione e riflettono la riservatezza sempre maggiore nei nomi di etichetta.

> [!IMPORTANT]
>Se si configurano [condizioni](configure-policy-classification.md) che potrebbero riguardare più etichette, è necessario ordinare le etichette dalla minima alla massima riservatezza. Questo ordinamento garantisce che venga applicata l'etichetta della massima riservatezza quando vengono valutate le condizioni.


Per apportare le modifiche, seguire queste istruzioni.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Passare quindi al riquadro **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca per risorse, servizi e documenti: iniziare a digitare **informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni** > **etichette** : nel riquadro **etichette Azure Information Protection** eseguire una o più delle azioni seguenti: 

    - Per eliminare un'etichetta: fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida ( **...** ) per l'etichetta che si vuole eliminare, scegliere **Elimina questa etichetta** e fare clic su **OK** per confermare. 

    - Per disabilitare un'etichetta: selezionare l'etichetta che si vuole disabilitare. Nel riquadro **etichetta** per **abilitato**Selezionare **disattivato**, quindi fare clic su **Salva**.

    - Per riordinare un'etichetta: fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida ( **...** ) per l'etichetta che si vuole riordinare, scegliere **Sposta su** o **Sposta giù** fino a quando l'etichetta non è nell'ordine desiderato.  

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  


