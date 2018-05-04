---
title: Aggiungere o rimuovere un'etichetta a o da un criterio di Azure Information Protection
description: Aggiungere o rimuovere un'etichetta di Azure Information Protection a o dai criteri globali per tutti gli utenti oppure a o da un criterio con ambito per un sottoinsieme di utenti.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.openlocfilehash: 73152d2202096775d315f874b30269c89213f8e1
ms.sourcegitcommit: 94d1c7c795e305444e9fde17ad73e46f242bcfa9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2018
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Aggiungere o rimuovere un'etichetta a o da un criterio di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

>[!NOTE]
> Questo articolo riflette gli ultimi aggiornamenti apportati al portale di Azure, che consentono di creare un'etichetta in modo indipendente dai criteri globali o da criteri con ambito. Inoltre, l'opzione per la pubblicazione dei criteri è stata rimossa. Se il tenant non è ancora aggiornato per queste modifiche, ad esempio se è ancora visibile l'opzione **Pubblica** per Azure Information Protection mentre l'opzione di menu **CLASSIFICAZIONI** non compare, attendere qualche giorno e quindi tornare a queste istruzioni.  

Dopo aver creato un'etichetta di Azure Information Protection, è possibile aggiungerla a un criterio in modo da renderla disponibile per gli utenti. Se l'etichetta è per tutti gli utenti, aggiungerla ai criteri globali. Se l'etichetta è per un subset di utenti, aggiungerla a un criterio con ambito. Attualmente, è possibile aggiungere un'etichetta a un solo criterio. Per aggiungere un'etichetta secondaria, l'etichetta padre deve essere nello stesso criterio o nei criteri globali.

Se un'etichetta è già in un criterio, è possibile rimuoverla dal criterio. Questa azione non elimina l'etichetta, che resta disponibile per essere usata in un altro criterio.

Se non si è ancora creata l'etichetta, vedere [Come creare una nuova etichetta per Azure Information Protection](configure-policy-new-label.md).

Se è necessario creare un criterio con ambito in modo che l'etichetta si applichi a un sottoinsieme di utenti, vedere [Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Per aggiungere o rimuovere un'etichetta a o da un criterio

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **CLASSIFICAZIONI** > **Criteri**: nel pannello **Azure Information Protection** - **Criteri** selezionare **Globale** se l'etichetta da aggiungere o rimuovere si applica a tutti gli utenti.

    Se l'etichetta da aggiungere o rimuovere si applica a un sottoinsieme di utenti, selezionare invece il criterio con ambito.

3. Nel pannello **Criteri** selezionare **Aggiungi o rimuovi etichette**.

4. Nel pannello **Criteri: Aggiungi o rimuovi etichette** sono visualizzate tutte le etichette, con una casella di controllo selezionata se sono già in un criterio e il nome del criterio corrispondente nella colonna **CRITERIO**.
     
    Le etichette secondarie vengono visualizzate come rientrate. In un criterio con ambito, le etichette ereditate dai criteri globali vengono visualizzate come non disponibili.
    
    Eseguire una delle operazioni seguenti, quindi fare clic su **OK**:
    
    - Per aggiungere un'etichetta, selezionarla. Questa operazione aggiunge una casella di controllo selezionata.
    
    - Per rimuovere un'etichetta, deselezionare la casella di controllo corrispondente.
  
5. Fare clic su **Save** (Salva) per salvare le modifiche.
   
    Le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
