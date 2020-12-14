---
title: Nuova etichetta per Azure Information Protection - AIP
description: Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: b1f2ec33fefd75ea117cd88519de32a952a8a9b1
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383186"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Come creare una nuova etichetta per Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'ultima etichetta nel [criterio predefinito](configure-policy-default.md)contiene le etichette secondarie.

Quando si crea la prima etichetta secondaria per un'etichetta, gli utenti non possono più selezionare l'etichetta padre originale. Se necessario, creare una nuova etichetta secondaria per ricreare le impostazioni dell'etichetta padre in modo che gli utenti possano applicare le stesse impostazioni.

Seguire queste istruzioni per aggiungere una nuova etichetta che sarà poi possibile aggiungere ai criteri di Azure Information Protection.

## <a name="to-create-a-new-label"></a>Per creare una nuova etichetta

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni**  >  **etichette** : nel riquadro **Azure Information Protection etichette** eseguire una delle operazioni seguenti:
    
    - Per creare una nuova etichetta, fare clic su **Aggiungi una nuova etichetta**.
    
    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi fare clic su **Aggiungi un'etichetta secondaria**.

3. Nel riquadro **etichetta** o **etichetta secondaria** Selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.
    
    Quando si specifica un nome visualizzato, non è consentito specificare alcuni caratteri (ad esempio barra rovesciata ed e commerciale) perché non tutti i servizi e le applicazioni che usano Azure Information Protection supportano questi caratteri. Oltre ai caratteri bloccati, non specificare il **#** carattere.    
    
    Si noti che alle nuove etichette viene assegnato automaticamente il colore nero. Scegliere un colore distintivo dall'elenco dei colori o immettere un codice tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, **#DAA520**. Se è necessario un riferimento per questi codici, è possibile trovare una tabella utile dalla [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) pagina della documentazione Web di MSDN. Questi codici sono disponibili anche in molte applicazioni che consentono di modificare le immagini. Ad esempio quando in Microsoft Paint si sceglie un colore personalizzato in una tavolozza vengono visualizzati automaticamente i valori RGB corrispondenti ed è possibile copiarli.

4. Per rendere disponibile la nuova etichetta agli utenti: dall'opzione di menu **classificazioni**  >  **criteri** selezionare i criteri che contengono la nuova etichetta. Selezionare **Add or remove labels** (Aggiungi o rimuovi etichette). Selezionare l'etichetta nel riquadro **criteri: Aggiungi o Rimuovi etichette** , selezionare **OK** e quindi fare clic su **Salva**.
    
    >[!TIP]
    >Per quanto riguarda le nuove etichette, valutare la possibilità di aggiungerle in un primo momento a un criterio con ambito usato a scopi di test. Quando si è soddisfatti dei risultati, rimuovere l'etichetta da questo ambito di test e quindi aggiungerla a un criterio in uso nell'ambiente di produzione.     
    
    Per altre informazioni sull'aggiunta di etichette, vedere [Come aggiungere o rimuovere un'etichetta](configure-policy-add-remove-label.md).
    
    Le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

5. Per visualizzare il nuovo nome di etichetta e la descrizione in lingue diverse per gli utenti, seguire le procedure descritte in [Come configurare etichette per lingue diverse](configure-policy-languages.md). 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  


