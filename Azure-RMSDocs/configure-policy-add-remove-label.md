---
title: Aggiungere o rimuovere un'etichetta in o da criteri di Azure Information Protection - AIP
description: Aggiungere o rimuovere un'etichetta di Azure Information Protection a o dai criteri globali per tutti gli utenti oppure a o da un criterio con ambito per un sottoinsieme di utenti.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: bb4b9ad8cc8b6ec642f8e0553c038488f9d27ab3
ms.sourcegitcommit: d0012de76c9156dd9239f7ba09c044a4b42ffc71
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/06/2020
ms.locfileid: "75675058"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Aggiungere o rimuovere un'etichetta a o da un criterio di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection client (versione classica)** e la **gestione delle etichette** nel portale di Azure verranno **deprecati** a partire dal **31 marzo 2021**. Questo intervallo di tempo consente a tutti i clienti correnti Azure Information Protection di passare alla soluzione di assegnazione di etichette unificata usando la piattaforma Microsoft Information Protection Unified labeling. Ulteriori informazioni sono disponibili nell' [avviso ufficiale di deprecazione](https://aka.ms/aipclassicsunset).

Dopo aver creato un'etichetta di Azure Information Protection, è possibile aggiungerla a un criterio in modo da renderla disponibile per gli utenti. Se l'etichetta è per tutti gli utenti, aggiungerla ai criteri globali. Se l'etichetta è per un subset di utenti, aggiungerla a un criterio con ambito. Un'etichetta può essere aggiunta a un solo criterio. 

Per aggiungere un'etichetta secondaria, l'etichetta padre deve essere nello stesso criterio o nei criteri globali. Quando si aggiunge un'etichetta secondaria, le impostazioni dell'etichetta principale non vengono ereditate. Per gli utenti a cui è assegnata l'etichetta secondaria nei criteri, l'etichetta principale è supportata solo come contenitore visualizzato per il nome e il colore. In questo scenario altre impostazioni di configurazione nell'etichetta principale non sono supportate per contrassegni visivi, protezione e condizioni. Sebbene sia comunque possibile configurarle, tali impostazioni dell'etichetta principale sono supportate solo per gli utenti che nei criteri hanno l'etichetta principale senza etichetta secondaria.

Se un'etichetta è già in un criterio, è possibile rimuoverla dal criterio. Questa azione non elimina l'etichetta, che resta disponibile per essere usata in un altro criterio.

Se non si è ancora creata l'etichetta, vedere [Come creare una nuova etichetta per Azure Information Protection](configure-policy-new-label.md).

Se è necessario creare un criterio con ambito in modo che l'etichetta si applichi a un sottoinsieme di utenti, vedere [Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Per aggiungere o rimuovere un'etichetta a o da un criterio

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca per risorse, servizi e documenti: iniziare a digitare **informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni** > **criteri** : nel riquadro **criteri** di - **Azure Information Protection** selezionare **globale** se l'etichetta da aggiungere o rimuovere si applica a tutti gli utenti.

    Se l'etichetta da aggiungere o rimuovere si applica a un sottoinsieme di utenti, selezionare invece il criterio con ambito.

3. Nel riquadro **criteri** selezionare **Aggiungi o Rimuovi etichette**.

4. Nel riquadro **criteri: Aggiungi o Rimuovi etichette** è possibile visualizzare tutte le etichette con una casella di controllo selezionata se sono già presenti in un criterio e il nome dei criteri corrispondente nella colonna **criterio** .
     
    Le etichette secondarie vengono visualizzate come rientrate. In un criterio con ambito, le etichette ereditate dai criteri globali vengono visualizzate come non disponibili.
    
    Eseguire una delle operazioni seguenti, quindi fare clic su **OK**:
    
    - Per aggiungere un'etichetta, selezionarla. Questa operazione aggiunge una casella di controllo selezionata.
    
    - Per rimuovere un'etichetta, deselezionare la casella di controllo corrispondente.
  
5. Fare clic su **Save** (Salva) per salvare le modifiche.
   
    Le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).
