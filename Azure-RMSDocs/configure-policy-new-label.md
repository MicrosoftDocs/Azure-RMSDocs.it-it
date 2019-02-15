---
title: Nuova etichetta per Azure Information Protection - AIP
description: Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie da mostrare all'utente sulla barra Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 8761b6225c46460aa782568fae8fe27f12fd81b6
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259304"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Come creare una nuova etichetta per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection offre etichette predefinite personalizzabili, ma è anche possibile creare etichette proprie.

Si può aggiungere una nuova etichetta oppure aggiungere una nuova etichetta secondaria a un'etichetta esistente quando è necessario un ulteriore livello di classificazione. Ad esempio, l'ultima etichetta dei [criteri predefiniti](configure-policy-default.md) include etichette secondarie.

Quando si crea la prima etichetta secondaria per un'etichetta, gli utenti non possono più selezionare l'etichetta padre originale. Se necessario, creare una nuova etichetta secondaria per ricreare le impostazioni dell'etichetta padre in modo che gli utenti possano applicare le stesse impostazioni.

Seguire queste istruzioni per aggiungere una nuova etichetta che sarà poi possibile aggiungere ai criteri di Azure Information Protection.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Classificazioni** > **Etichette**: Nel pannello **Azure Information Protection - Etichette** effettuare una delle operazioni seguenti:
    
    - Per creare una nuova etichetta: Fare clic su **Aggiungi una nuova etichetta**.
    
    - Per creare una nuova etichetta secondaria: Fare clic con il pulsante destro del mouse o selezionare il menu di scelta rapida (**...**) per l'etichetta per cui si vuole creare un'etichetta secondaria, quindi scegliere **Aggiungi un'etichetta secondaria**.

3. Nel pannello **Etichetta** o **Etichetta secondaria** selezionare le opzioni desiderate per la nuova etichetta, quindi fare clic su **Salva**.
    
    Quando si specifica un nome visualizzato, non è consentito specificare alcuni caratteri (ad esempio barra rovesciata ed e commerciale) perché non tutti i servizi e le applicazioni che usano Azure Information Protection supportano questi caratteri. Oltre ai caratteri bloccati, non specificare il carattere **#**.    
    
    Si noti che alle nuove etichette viene assegnato automaticamente il colore nero. Scegliere un colore distintivo dall'elenco dei colori o immettere un codice tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, **#DAA520**. Se è necessario un riferimento per questi codici, un utile punto di partenza è l'articolo [Colors by Name](https://msdn.microsoft.com/library/aa358802(v=vs.85).aspx) (Colori per nome), disponibile nella documentazione MSDN; questi codici sono anche presenti in molti programmi di modifica immagini, come Microsoft Paint, in cui scegliendo un colore personalizzato da una tavolozza vengono visualizzati automaticamente i valori RGB.

4. Per rendere disponibile la nuova etichetta per gli utenti: Dall'opzione di menu **Classificazioni** > **Criteri** selezionare i criteri in cui includere la nuova etichetta. Selezionare **Add or remove labels** (Aggiungi o rimuovi etichette). Selezionare l'etichetta nel pannello **Policy: Add or remove labels** (Criteri: Aggiungi o rimuovi etichette), selezionare **OK** e quindi selezionare **Salva**.
    
    >[!TIP]
    >Per quanto riguarda le nuove etichette, valutare la possibilità di aggiungerle in un primo momento a un criterio con ambito usato a scopi di test. Quando si è soddisfatti dei risultati, rimuovere l'etichetta da questo ambito di test e quindi aggiungerla a un criterio in uso nell'ambiente di produzione.     
    
    Per altre informazioni sull'aggiunta di etichette, vedere [Come aggiungere o rimuovere un'etichetta](configure-policy-add-remove-label.md).
    
    Le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

5. Se si vuole che il nome e la descrizione della nuova etichetta vengano visualizzati in lingue diverse per gli utenti: Seguire le procedure descritte in [Come configurare etichette per lingue diverse](configure-policy-languages.md). 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  


