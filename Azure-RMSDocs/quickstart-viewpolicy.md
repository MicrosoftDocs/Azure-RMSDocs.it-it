---
title: Guida introduttiva - Attività iniziali nel portale di Azure
description: Se l'organizzazione non ha familiarità con Azure Information Protection, iniziare da qui per aggiungere il servizio al portale di Azure, verificare che il servizio di protezione sia attivato e visualizzare i criteri.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/05/2018
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: adcaa1e0f15536d83a20c54017813d7e1546d860
ms.sourcegitcommit: ad37950f6a747c86f6496c6de859e18446f9b03f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2018
ms.locfileid: "51644710"
---
# <a name="quickstart-get-started-in-the-azure-portal"></a>Guida introduttiva: Attività iniziali nel portale di Azure

In questa guida introduttiva si aggiungerà Azure Information Protection al portale di Azure, si verificherà che il servizio di protezione sia attivato e si visualizzeranno i criteri predefiniti dell'organizzazione. 

È possibile completare questa guida introduttiva in 5 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

- Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Aggiungere Azure Information Protection al portale di Azure

Azure Information Protection non è automaticamente disponibile nel portale di Azure, ma è necessario aggiungerlo.

1. Accedere al [portale di Azure](https://portal.azure.com) usando l'account di amministratore globale per il tenant. 
    
    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Nel menu dell'hub selezionare **Crea una risorsa** e quindi nella casella di ricerca per il Marketplace digitare **Azure Information Protection**. 
    
3. Selezionare **Azure Information Protection** nell'elenco dei risultati. Fare quindi clic su **Crea** nel pannello **Azure Information Protection**.
    
    > [!TIP] 
    > Facoltativamente, selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.
    
    Fare di nuovo clic su **Crea**.

## <a name="confirm-the-protection-service-is-activated"></a>Verificare che il servizio di protezione sia attivato

Il servizio di protezione viene attivato automaticamente per i nuovi tenant, ma è consigliabile verificare che non sia necessario attivarlo manualmente. 

1. Nel pannello **Azure Information Protection** selezionare **Gestisci** > **Attivazione della protezione**.

2. Verificare che la protezione sia attivata per il tenant: 
    
    - Se la protezione è attivata, viene visualizzato il messaggio di conferma seguente:
        
        ![Stato di Azure Information Protection per Azure RMS](./media/info-protect-azurerms-activated.png)
        
    - Se la protezione non è attivata, le informazioni sullo stato indicano questa condizione e viene visualizzata l'opzione per l'attivazione:
        
        ![Stato di Azure Information Protection per Azure RMS](./media/info-protect-azurerms-deactivated.png)

3. Se la protezione non è attivata, selezionare **Attiva**. 

    Una volta completata l'attivazione, sulla barra delle informazioni verrà visualizzato il messaggio **Activation finished successfully** (Attivazione completata).

## <a name="view-your-organizations-default-policy---labels-and-policy-settings"></a>Visualizzare i criteri predefiniti dell'organizzazione: etichette e impostazioni dei criteri

La prima volta che ci si connette al servizio Azure Information Protection tramite il portale di Azure, vengono creati criteri predefiniti per il tenant. I criteri predefiniti contengono etichette e impostazioni utilizzabili così come sono o personalizzabili.

1. Select **Classificazioni** > **Criteri** > **Globale** per visualizzare i criteri predefiniti di Azure Information Protection creati per il tenant.
    
2. Dedicare alcuni minuti ad acquisire familiarità con le etichette visualizzate:
    
    - Etichette per la classificazione: **Personal**, **Public**, **General**, **Confidential** (Riservato) e **Highly Confidential** (Riservatezza elevata). Le ultime due etichette si espandono per visualizzare le etichette secondarie, offrendo esempi di come una classificazione può avere sottocategorie:
    
    - Con la configurazione predefinita, alcune etichette non hanno contrassegni visivi configurati. I contrassegni visivi sono il piè di pagina, l'intestazione e la filigrana. In base ai criteri predefiniti, per alcune etichette può essere impostata una protezione. Ad esempio: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](./media/info-protect-policy-default-labelsv2.png)
    
3. Dopo le etichette, nella sezione **Configure settings to display and apply on Information Protection end users** (Configurare le impostazioni da visualizzare e applicare per gli utenti finali di Information Protection) vengono visualizzate anche alcune impostazioni dei criteri. Ad esempio non è presente un'etichetta predefinita (non tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta) e gli utenti non devono dare una giustificazione quando modificano le etichette:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](./media/info-protect-policy-default-settings.png) 

4. Poiché si stanno visualizzando solo le etichette e le impostazioni, è possibile chiudere tutti i pannelli aperti.

## <a name="next-steps"></a>Passaggi successivi

Dopo avere esaminato le etichette e le impostazioni dei criteri nel portale di Azure, potrebbe essere utile seguire l'esercitazione seguente come passaggio successivo: [Modificare i criteri e creare una nuova etichetta per Azure Information Protection](infoprotect-quick-start-tutorial.md).

In alternativa, per istruzioni dettagliate per la configurazione di tutti gli aspetti dei criteri di Azure Information Protection, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).
