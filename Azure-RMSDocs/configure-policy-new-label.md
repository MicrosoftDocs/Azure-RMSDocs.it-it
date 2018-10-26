---
title: Nuova etichetta per Azure Information Protection
description: Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 71baa99f944a8fd6aa1f28bcc6dd935df3e20ac0
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2018
ms.locfileid: "49170268"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'ultima etichetta dei [criteri predefiniti](configure-policy-default.md) include etichette secondarie.

Quando si crea la prima etichetta secondaria per un'etichetta, gli utenti non possono più selezionare l'etichetta padre originale. Se necessario, creare una nuova etichetta secondaria per ricreare le impostazioni dell'etichetta padre in modo che gli utenti possano applicare le stesse impostazioni.

Seguire queste istruzioni per aggiungere una nuova etichetta che sarà poi possibile aggiungere ai criteri di Azure Information Protection.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Classificazioni** > **Etichette**: nel pannello **Azure Information Protection - Etichette** eseguire una delle operazioni seguenti:
    
    - Per creare una nuova etichetta, fare clic su **Aggiungi una nuova etichetta**.
    
    - Per creare una nuova etichetta secondaria, fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Aggiungi un'etichetta secondaria**.

4. Nel pannello **Etichetta** o **Etichetta secondaria** selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.
    
    Quando si specifica un nome visualizzato, non è consentito specificare alcuni caratteri (ad esempio barra rovesciata ed e commerciale) perché non tutti i servizi e le applicazioni che usano Azure Information Protection supportano questi caratteri. Oltre ai caratteri bloccati, non specificare il carattere **#**.    
    
    Si noti che alle nuove etichette viene assegnato automaticamente il colore nero. Scegliere un colore distintivo dall'elenco dei colori o immettere un codice tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, **#DAA520**. Se è necessario un riferimento per questi codici, un utile punto di partenza è costituito dall'articolo [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx) (Colori per nome) disponibile nella documentazione MSDN; inoltre, questi codici sono presenti in molti programmi di modifica delle immagini, come Microsoft Paint, in cui scegliendo un colore personalizzato da una tavolozza vengono visualizzati automaticamente i valori RGB.

5. Per rendere disponibile la nuova etichetta agli utenti: nell'opzione di menu **Classificazioni** > **Criteri** selezionare i criteri in cui includere la nuova etichetta. Selezionare **Add or remove labels** (Aggiungi o rimuovi etichette). Selezionare l'etichetta nel pannello**Policy: Add or remove labels** (Criteri: Aggiungi o rimuovi etichette), selezionare **OK** e quindi selezionare **Salva**.
    
    >[!TIP]
    >Per quanto riguarda le nuove etichette, valutare la possibilità di aggiungerle in un primo momento a un criterio con ambito usato a scopi di test. Quando si è soddisfatti dei risultati, rimuovere l'etichetta da questo ambito di test e quindi aggiungerla a un criterio in uso nell'ambiente di produzione.     
    
    Per altre informazioni sull'aggiunta di etichette, vedere [Come aggiungere o rimuovere un'etichetta](configure-policy-add-remove-label.md).
    
    Le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

6. Per visualizzare il nuovo nome di etichetta e la descrizione in lingue diverse per gli utenti, seguire le procedure descritte in [Come configurare etichette per lingue diverse](configure-policy-languages.md). 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  


