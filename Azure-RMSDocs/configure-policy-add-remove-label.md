---
title: Aggiungere o rimuovere un'etichetta in o da criteri di Azure Information Protection - AIP
description: Aggiungere o rimuovere un'etichetta di Azure Information Protection a o dai criteri globali per tutti gli utenti oppure a o da un criterio con ambito per un sottoinsieme di utenti.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 650530014053444f3bd3e1d0a8f53cff3316b709
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806788"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Aggiungere o rimuovere un'etichetta a o da un criterio di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Dopo aver creato un'etichetta di Azure Information Protection, è possibile aggiungerla a un criterio in modo da renderla disponibile per gli utenti. Se l'etichetta è per tutti gli utenti, aggiungerla ai criteri globali. Se l'etichetta è per un subset di utenti, aggiungerla a un criterio con ambito. Un'etichetta può essere aggiunta a un solo criterio. 

Per aggiungere un'etichetta secondaria, l'etichetta padre deve essere nello stesso criterio o nei criteri globali. Quando si aggiunge un'etichetta secondaria, le impostazioni dell'etichetta principale non vengono ereditate. Per gli utenti a cui è assegnata l'etichetta secondaria nei criteri, l'etichetta principale è supportata solo come contenitore visualizzato per il nome e il colore. In questo scenario altre impostazioni di configurazione nell'etichetta principale non sono supportate per contrassegni visivi, protezione e condizioni. Sebbene sia comunque possibile configurarle, tali impostazioni dell'etichetta principale sono supportate solo per gli utenti che nei criteri hanno l'etichetta principale senza etichetta secondaria.

Se un'etichetta è già in un criterio, è possibile rimuoverla dal criterio. Questa azione non elimina l'etichetta, che resta disponibile per essere usata in un altro criterio.

Se non si è ancora creata l'etichetta, vedere [Come creare una nuova etichetta per Azure Information Protection](configure-policy-new-label.md).

Se è necessario creare un criterio con ambito in modo che l'etichetta si applichi a un sottoinsieme di utenti, vedere [Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Per aggiungere o rimuovere un'etichetta a o da un criterio

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni**  >  **criteri** : nel riquadro   -  **criteri** di Azure Information Protection selezionare **globale** se l'etichetta da aggiungere o rimuovere si applica a tutti gli utenti.

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
