---
title: 'Guida di avvio rapido: nuova etichetta di Azure Information Protection per utenti specifici - AIP'
description: Creare e configurare una nuova etichetta che consenta di classificare documenti e messaggi di posta elettronica per un subset di utenti usando criteri con ambito.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 31a4b4151d692a7bcb25516081b70de57a96ee16
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807468"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>Guida introduttiva: Creare una nuova etichetta di Azure Information Protection per utenti specifici

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

In questa guida introduttiva si creerà una nuova etichetta di Azure Information Protection che solo determinati utenti possono vedere e applicare per classificare e proteggere documenti e messaggi di posta elettronica.

Questa configurazione usa criteri con ambito.

**Tempo necessario**: È possibile completare questa configurazione in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

|Requisito  |Descrizione  |
|---------|---------|
|**Una sottoscrizione di supporto**     |  Sarà necessaria una sottoscrizione che includa [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). </br></br>In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.       |
|**AIP aggiunto al portale di Azure**    |  Aver aggiunto il riquadro Azure Information Protection al portale di Azure e aver verificato che il servizio di protezione sia attivato. </br></br>Per altre informazioni, vedere [Avvio rapido: Attività iniziali nel portale di Azure](quickstart-viewpolicy.md).       |
|**Un gruppo abilitato per la posta elettronica in Azure AD**     | È necessario un gruppo abilitato per la posta elettronica in Azure AD che contiene gli utenti che potranno visualizzare e applicare la nuova etichetta. </br></br>Se non si ha un gruppo adatto, crearne uno denominato **Team vendite** e aggiungere almeno un utente. |
|**Client classico installato**    |   Per testare la nuova etichetta, è necessario che il client classico sia installato nel computer. </br></br>Il client classico Azure Information Protection verrà deprecato nel marzo 2021. Per distribuire il client classico AIP, aprire un ticket di supporto per ottenere l'accesso al download.  |
| | |

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="create-a-new-label"></a>Creare una nuova etichetta

Per prima cosa, creare la nuova etichetta.

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com). Passare quindi al riquadro **Azure Information Protection**.

    Ad esempio, nella casella di ricerca di risorse, servizi e documenti iniziare a digitare **Information** e selezionare **Azure Information Protection**.

    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

1. In **Classificazioni** selezionare **Etichette** e quindi fare clic su **+ Aggiungi una nuova etichetta**.

1. Nel riquadro **Etichetta** specificare almeno i campi seguenti:

    |Campo  |Descrizione  |
    |---------|---------|
    |**Nome visualizzato dell'etichetta**     |    il nome della nuova etichetta che sarà visibile agli utenti e che identifica la classificazione del contenuto. </br>Ad esempio: **Vendite - Accesso limitato**    |
    |**Descrizione**     |   una descrizione comando che consenta agli utenti di capire quando è opportuno selezionare questa nuova etichetta. </br> Ad esempio: **Dati aziendali con accesso limitato al team vendite.**     |
    | | | 

1. Assicurarsi che l'opzione **Abilitato** sia impostata su **Sì** (impostazione predefinita) e selezionare **Salva** ![Salva](media/qs-tutor/save-icon.png "Salva").

    Selezionare la **X** nella parte superiore destra per chiudere il riquadro **Nuova etichetta**.

## <a name="add-the-label-to-a-new-scoped-policy"></a>Aggiungere l'etichetta ai nuovi criteri con ambito

Aggiungere ora l'etichetta appena creata ai nuovi criteri con ambito.

1. A sinistra in **Classificazioni** selezionare **Criteri** e quindi fare clic su **Aggiungi un nuovo criterio**.

1. Nel campo **Nome criterio** immettere un valore significativo che descriva gli utenti che visualizzeranno la nuova etichetta.

    Ad esempio: **Vendite**.

1. Selezionare la riga **Selezionare gli utenti o i gruppi a cui viene applicato il criterio** per aprire il riquadro **Utenti e gruppi di AAD**.

1. Nel riquadro **Utenti e gruppi di AAD** cercare e selezionare il gruppo identificato nei prerequisiti, ad esempio **Team vendite**.

    Fare clic su **Seleziona** per chiudere il riquadro.

1. Nel riquadro **Criteri** in **Nome visualizzato dell'etichetta** fare clic su **Aggiungi o rimuovi etichette**.

1. Nel pannello **Criteri: Aggiungi o rimuovi etichette** selezionare l'etichetta creata, ad esempio **Vendite - Con restrizioni**, quindi selezionare **OK**.

1. Nel riquadro **Criteri** selezionare **Salva** ![Salva](media/qs-tutor/save-icon.png "Salva").

La nuova etichetta è ora pubblicata solo per i membri del gruppo specificato.

## <a name="test-your-new-label"></a>Testare la nuova etichetta

Per testare questa etichetta sono necessari almeno due computer, poiché il client Azure Information Protection non supporta più utenti nello stesso computer:

- **Nel primo computer** accedere come membro del gruppo Team vendite. Aprire Word e verificare che sia possibile visualizzare la nuova etichetta. Se Word è già aperto, riavviarlo per forzare un aggiornamento dei criteri.

- **Nel secondo computer** accedere come utente *non* membro del gruppo Team vendite. Aprire Word e verificare che non sia possibile visualizzare la nuova etichetta. Come in precedenza, se Word è già aperto, riavviarlo.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vuole mantenere questa etichetta e i criteri con ambito, seguire questa procedura:

1. Dall'area **Classificazioni** > **Criteri**: nel riquadro **Azure Information Protection - Criteri** selezionare il menu di scelta rapida ( **...** ) relativo ai criteri con ambito creati. Ad esempio: **Vendite**.

1. Selezionare **Elimina criteri** e, se viene richiesto di confermare l'operazione, scegliere **OK**.

1. Dall'area **Classificazioni** > **Etichetta**: nel riquadro **Azure Information Protection - Etichetta** selezionare il menu di scelta rapida ( **...** ) per l'etichetta creata.  Ad esempio: **Vendite - Con restrizioni**.

1. Selezionare **Elimina questa etichetta** e, se viene richiesto di confermare l'operazione, scegliere **OK**.

## <a name="next-steps"></a>Passaggi successivi

Questo avvio rapido include le informazioni strettamente indispensabili per creare rapidamente una nuova etichetta per utenti specifici usando il client classico. Per istruzioni complete, vedere gli articoli seguenti:

- [Come creare una nuova etichetta](configure-policy-new-label.md)

- [Come configurare i criteri per utenti specifici con i criteri con ambito](configure-policy-scope.md)

Se si vuole che l'etichetta protegga i contenuti in modo che possano essere aperti solo dai membri del Team vendite, è necessario configurare l'etichetta per l'applicazione della protezione. Per istruzioni, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md).
