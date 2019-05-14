---
title: Avvio rapido - Visualizzare Azure Information Protection nel portale di Azure - AIP
description: Se l'organizzazione non ha familiarità con Azure Information Protection, iniziare da qui per aggiungere il servizio al portale di Azure, verificare che il servizio di protezione sia attivato e visualizzare le etichette e le impostazioni dei criteri.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/25/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 099d35d7d4862aff3006b1d6cc57423b898234c4
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767884"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>Guida introduttiva: Introduzione ad Azure Information Protection nel portale di Azure

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

In questa guida di avvio rapido si aggiungerà Azure Information Protection al portale di Azure, si verificherà che il servizio di protezione sia attivato, si creeranno le etichette predefinite, se non sono già disponibili, e si visualizzeranno le impostazioni dei criteri per Azure Information Protection.

È possibile completare questa guida di avvio rapido in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

- Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

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

Il servizio di protezione viene attivato automaticamente per i nuovi clienti, ma è consigliabile verificare che non sia necessario attivarlo manualmente. 

1. Nel pannello **Azure Information Protection** selezionare **Gestisci** > **Attivazione della protezione**.

2. Verificare che la protezione sia attivata per il tenant: 
    
    - Se la protezione è attivata, viene visualizzato il messaggio di conferma seguente:
        
        ![Stato di Azure Information Protection per Azure RMS - attivato](./media/info-protect-azurerms-activated.png)
        
    - Se la protezione non è attivata, le informazioni sullo stato indicano questa condizione e viene visualizzata l'opzione per l'attivazione:
        
        ![Stato di Azure Information Protection per Azure RMS - non attivato](./media/info-protect-azurerms-deactivated.png)

3. Se la protezione non è attivata, selezionare **Attiva**. 

    Una volta completata l'attivazione, sulla barra delle informazioni verrà visualizzato il messaggio **Activation finished successfully** (Attivazione completata).

## <a name="create-labels---if-necessary"></a>Creare le etichette, se necessario

L'organizzazione potrebbe già disporre di etichette, in quanto create automaticamente per il tenant o perché dispone di etichette di riservatezza nel Centro sicurezza e conformità di Office 365, nel Centro sicurezza Microsoft 365 o nel Centro conformità Microsoft 365. Per verificarlo, eseguire questa procedura:

1. Selezionare **Classificazioni** > **Etichette**:
    
    Se è presente l'opzione **Generate default labels** (Genera etichette predefinite), significa che non sono disponibili etichette:
    
     ![Nessuna etichetta predefinita di Azure Information Protection](./media/info-protect-nodefaultlabels.png)
    
    Se l'opzione per la generazione di etichette predefinite non è visualizzata, significa che si dispone già di etichette, probabilmente simili a quelle dell'immagine seguente, che sono le etichette predefinite di Azure Information Protection:
    
    ![Etichette predefinite di Azure Information Protection](./media/info-protect-defaultlabels.png)

2. Se si dispone di etichette, passare alla sezione successiva per visualizzarle. Se non si dispone ancora di etichette, selezionare **Generate default labels** (Genera etichette predefinite).

4. Quindi, per pubblicare le etichette per tutti gli utenti, in **Classificazioni** > **Criteri** > **Globale**:
    
    a. Selezionare **Add or remove labels** (Aggiungi o rimuovi etichette).
    
    b. Nel pannello **Policy: Aggiungi o rimuovi etichette** selezionare tutte le etichette e quindi scegliere **OK**.
    
    c. Di nuovo nel pannello **Criteri: Globale** selezionare **Salva**.

## <a name="view-your-labels"></a>Visualizzare le etichette

Selezionare **Classificazioni** > **Etichette** e dedicare qualche minuto all'esplorazione delle etichette visualizzate nel pannello **Azure Information Protection - Etichette**.

Se non sono simili alle etichette visualizzate nell'immagine riportata nella sezione precedente, significa che non si stanno usando le etichette predefinite di Azure Information Protection bensì etichette create nel Centro sicurezza e conformità di Office 365, nel Centro sicurezza Microsoft 365 o nel Centro conformità Microsoft 365.

> [!TIP]
> Se non si vogliono usare le etichette personalizzate ma quelle predefinite di Azure Information Protection: 
> - Eliminare le etichette personalizzate per visualizzare l'opzione per la generazione di etichette predefinite nel pannello **Etichette**, come descritto nella [sezione precedente](#create-labels---if-necessary). 

Nel pannello **Azure Information Protection - Etichette**:

- Le etichette predefinite per la classificazione sono **Personale**, **Pubblico**, **Generale**, **Riservato** e **Riservatezza elevata**. Le ultime due etichette si espandono per visualizzare le etichette secondarie, offrendo esempi di come una classificazione può avere sottocategorie.

- Nelle colonne **CONTRASSEGNO** e **PROTEZIONE** è possibile notare che per alcune etichette sono configurati contrassegni visivi. I contrassegni visivi sono il piè di pagina, l'intestazione e la filigrana. Per alcune etichette potrebbe anche essere impostata la protezione. 

Ad esempio: 

![Avvio rapido di Azure Information Protection - panoramica delle etichette predefinite](./media/info-protect-policy-default-labelsv2.png)

Se si seleziona un'etichetta, vengono visualizzati i dettagli della configurazione di tale etichetta in un nuovo pannello.

## <a name="view-your-policy-settings"></a>Visualizzare le impostazioni dei criteri

La prima volta che ci si connette al servizio Azure Information Protection usando il portale di Azure, vengono sempre create automaticamente le impostazioni dei criteri predefinite usate dal client Azure Information Protection. Le impostazioni dei criteri e le etichette vengono scaricate in questo client nei criteri di Azure Information Protection.

Se si usa il client di etichettatura unificata Azure Information Protection, tenere presente che non usa queste impostazioni dei criteri. Questo client scarica invece le etichette e le impostazioni dei criteri dal Centro sicurezza e conformità di Office 365, dal Centro sicurezza Microsoft 365 o dal Centro conformità Microsoft 365.

Per visualizzare le impostazioni dei criteri predefinite di Azure Information Protection:

1. Selezionare **Classificazioni** > **Criteri** > **Globale** per visualizzare le impostazioni dei criteri predefinite di Azure Information Protection create per il tenant.
    
2. Le impostazioni dei criteri sono visualizzate dopo le etichette nella sezione **Configura le impostazioni da visualizzare e applicare agli utenti finali di Information Protection**. Ad esempio non è presente un'etichetta predefinita (non tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta) e gli utenti non devono dare una giustificazione quando modificano le etichette:
    
    ![Impostazioni globali dei criteri di Azure Information Protection](./media/info-protect-policy-default-settingsv3.png)

3. Poiché si stanno visualizzando solo le impostazioni, è possibile chiudere tutti i pannelli aperti nel portale.

## <a name="next-steps"></a>Passaggi successivi

Dopo avere esaminato le etichette e le impostazioni predefinite dei criteri nel portale di Azure, potrebbe essere utile seguire l'esercitazione seguente come passaggio successivo: [Modificare i criteri e creare una nuova etichetta per Azure Information Protection](infoprotect-quick-start-tutorial.md).

In alternativa, per istruzioni dettagliate per la configurazione di tutti gli aspetti dei criteri di Azure Information Protection, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).
