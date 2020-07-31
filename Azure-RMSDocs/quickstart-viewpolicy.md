---
title: Avvio rapido - Visualizzare Azure Information Protection (AIP) nel portale di Azure
description: Se l'organizzazione non ha familiarità con Azure Information Protection (AIP), iniziare da qui per aggiungere il servizio al portale di Azure, verificare che il servizio di protezione sia attivato e pubblicare le etichette e le impostazioni dei criteri.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: ebe7260cdbd9a252323b13ffd91897e5cd423810
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927921"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>Guida introduttiva: Introduzione ad Azure Information Protection nel portale di Azure

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

In questa guida di avvio rapido si aggiungerà Azure Information Protection al portale di Azure, si verificherà che il servizio di protezione sia attivato, si creeranno le etichette predefinite, se non sono già disponibili, e si visualizzeranno le impostazioni dei criteri per il client Azure Information Protection (versione classica).

**Ora obbligatoria:** È possibile completare questa guida di avvio rapido in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare l'esercitazione introduttiva, sono necessari gli elementi seguenti:

- Accesso all'account del [**portale di Azure**](https://portal.azure.com/).

- Una sottoscrizione che includa un [**piano 1 o 2 di Azure Information Protection**](https://azure.microsoft.com/pricing/details/information-protection/).

    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Aggiungere Azure Information Protection al portale di Azure

Anche se si ha una sottoscrizione che include il piano 1 o piano 2 di Azure Information Protection, AIP non è automaticamente disponibile nel portale di Azure.

Per aggiungere AIP al portale di Azure, seguire questa procedura:

1. Accedere al [portale di Azure](https://portal.azure.com) usando l'account di amministratore globale per il tenant.

    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

1. Selezionare **+ Crea una risorsa**. Nella casella di ricerca per il Marketplace digitare e quindi selezionare **Azure Information Protection**. Nella pagina Azure Information Protection selezionare **Crea** e quindi di nuovo **Crea**.

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="Aggiungere Azure Information Protection al portale di Azure":::

    > [!TIP]
    > Se è la prima volta che si esegue questo passaggio, verrà visualizzata un'icona **Aggiungi al dashboard** ![icona Aggiungi al dashboard](media/qs-tutor/pin-to-dashboard.png "Icona Aggiungi al dashboard") accanto al nome del riquadro. Selezionare per creare un riquadro nel dashboard in modo che sia possibile passare direttamente a questa pagina in futuro.

## <a name="confirm-that-the-protection-service-is-activated"></a>Verificare che il servizio di protezione sia attivato

Il servizio di protezione viene ora attivato automaticamente per i nuovi clienti. Verificare che sia attivato o venga attivato in un momento successivo, come indicato di seguito:

1. Nel riquadro **Azure Information Protection** selezionare **Gestisci** > **Attivazione della protezione**.

1. Verificare che la protezione sia attivata per il tenant. Ad esempio:

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="Verificare l'attivazione di AIP":::

    Se la protezione non viene mai attivata, è necessario attivarla selezionando **Attiva** ![Attiva AIP](media/qs-tutor/activate.png "Attiva AIP"). Una volta completata l'attivazione, sulla barra delle informazioni verrà visualizzato il messaggio **Activation finished successfully** (Attivazione completata).

## <a name="create-and-publish-labels"></a>Creare e pubblicare etichette

L'organizzazione potrebbe già disporre di etichette, in quanto create automaticamente per il tenant o perché dispone di etichette di riservatezza nel Centro sicurezza e conformità di Office 365, nel Centro sicurezza Microsoft 365 o nel Centro conformità Microsoft 365. Per verificarlo, eseguire questa procedura:

1. In **Classificazioni** selezionare **Etichette**.

    È possibile che siano già state create etichette predefinite. L'immagine seguente mostra le etichette create per impostazione predefinita con Azure Information Protection:

    :::image type="content" source="media/info-protect-defaultlabels.png" alt-text="Etichette predefinite di Azure Information Protection":::

    **Se le etichette predefinite non vengono visualizzate o non viene visualizzata alcuna etichetta**:

    Se le etichette predefinite non vengono visualizzate o non viene visualizzata alcuna etichetta, selezionare **Genera etichette predefinite** per creare le etichette da usare nel client classico.

    Se non viene visualizzato il pulsante **Genera etichette predefinite** sopra la griglia, in **Gestisci** selezionare **Etichettatura unificata**. Se lo stato di Etichettatura unificata è **Non attivato**, selezionare **Attiva** e tornare al riquadro **Classificazioni** > **Etichette**.

    > [!NOTE]
    > Per il client di etichettatura unificata, le etichette vengono gestite in Microsoft M365. Per altre informazioni, vedere [Limitare l'accesso al contenuto usando la crittografia nelle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels).
    >

1. Pubblicare le etichette nel portale di Azure per renderle disponibili per il client classico Azure Information Protection:

    1. Aprire i criteri **Globale**. In **Classificazioni** selezionare **Criteri** > **Globale**.

    1. Selezionare **Add or remove labels** (Aggiungi o rimuovi etichette).

    1. Nel pannello **Policy: Aggiungi o rimuovi etichette** selezionare tutte le etichette e quindi scegliere **OK**.

    1. Di nuovo nel pannello **Criteri: Globale** selezionare il pulsante **Salva** ![Salva](media/qs-tutor/save-icon.png "Salva").

        Al prompt fare clic su **OK** per pubblicare le modifiche.

## <a name="view-your-labels"></a>Visualizzare le etichette

A questo punto è possibile acquisire familiarità con le etichette.

Se sono ancora aperti i criteri **Globale**, fare clic sulla **X** nella parte superiore destra per chiudere il riquadro. In **Classificazioni** selezionare **Etichette**.

Le etichette di classificazione predefinite di Azure Information Protection sono:

- **Personale**
- **Generalee**
- **Riservato**
- **Riservatezza elevata**

Per impostazione predefinita, per alcune etichette sono già configurati contrassegni visivi. Questi contrassegni visivi possono essere un piè di pagina, un'intestazione e/o una filigrana. La protezione è configurata anche per altre etichette.

Selezionare un'etichetta e spostarsi per visualizzare la configurazione dettagliata per l'etichetta.

> [!TIP]
> Espandere l'etichetta **Riservatezza elevata** per visualizzare l'esempio di una classificazione con sottocategorie.
>

## <a name="view-your-policy-settings"></a>Visualizzare le impostazioni dei criteri

La prima volta che ci si connette al servizio Azure Information Protection dal portale di Azure, vengono sempre create automaticamente le impostazioni dei criteri predefinite usate dal client Azure Information Protection.

- **Client classico.** Per il client classico, le impostazioni dei criteri e le etichette vengono scaricate nel client nei criteri di Azure Information Protection.

- **Client per l'etichettatura unificata.** Per il client di etichettatura unificata, vengono scaricate solo le etichette nel client. Le impostazioni dei criteri vengono scaricate dal Centro sicurezza e conformità di Office 365, dal Centro conformità Microsoft 365 o dal Centro sicurezza Microsoft 365. Usare questi centri di amministrazione per modificare le etichette ed etichettare i criteri anziché il portale di Azure.

    Per altre informazioni, vedere [Informazioni sulle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) nella documentazione di Microsoft 365.

**Istruzioni per il client classico:**

Per visualizzare le impostazioni dei criteri predefinite di Azure Information Protection per la versione classica del client:

1. In **Classificazioni** selezionare **Criteri** > **Globale** per visualizzare le impostazioni dei criteri predefinite di Azure Information Protection create per il tenant.

1. Le impostazioni dei criteri sono visualizzate dopo le etichette nella sezione **Configura le impostazioni da visualizzare e applicare agli utenti finali di Information Protection**. Ad esempio non è presente un'etichetta predefinita (non tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta) e gli utenti non devono dare una giustificazione quando modificano le etichette:

    :::image type="content" source="media/defaultsettings-aip.png" alt-text="Impostazioni globali dei criteri di Azure Information Protection":::

1. È ora possibile chiudere tutti i riquadri precedentemente aperti nel portale.

## <a name="next-steps"></a>Passaggi successivi

I passaggi successivi variano a seconda che si utilizzi un client classico o un client di etichettatura unificata. Non si è certi della differenza tra questi client? Vedere queste [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).

**Se si usa il client classico:**

- l'esercitazione seguente può risultare utile come passaggio successivo: [Modificare i criteri e creare una nuova etichetta per Azure Information Protection](infoprotect-quick-start-tutorial.md).

- In alternativa, per istruzioni dettagliate per la configurazione di tutti gli aspetti dei criteri di Azure Information Protection, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

**Se si usa il client di etichettatura unificata:**

Vedere [Informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) nella documentazione sulla conformità di Microsoft 365.
