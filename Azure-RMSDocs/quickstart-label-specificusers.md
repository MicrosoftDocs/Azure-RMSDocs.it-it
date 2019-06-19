---
title: 'Guida di avvio rapido: nuova etichetta di Azure Information Protection per utenti specifici - AIP'
description: Creare e configurare una nuova etichetta che consenta di classificare documenti e messaggi di posta elettronica per un subset di utenti usando criteri con ambito.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 3a3c1e2ed27bfa8923301c3d0afbe04f864df315
ms.sourcegitcommit: a26d033ccd557839b61736284456370393f3b52a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156689"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>Guida introduttiva: Creare una nuova etichetta di Azure Information Protection per utenti specifici

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

In questa guida introduttiva si creerà una nuova etichetta che solo determinati utenti possono vedere e applicare per classificare e proteggere documenti e messaggi di posta elettronica.

Questa configurazione usa criteri con ambito.

È possibile completare questa configurazione in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

1. Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Aver aggiunto il pannello di Azure Information Protection nel portale di Azure e aver verificato che il servizio di protezione è attivato.

    Se occorre assistenza per queste azioni, vedere [Avvio rapido: Attività iniziali nel portale di Azure](quickstart-viewpolicy.md).

3. Un gruppo abilitato per la posta elettronica in Azure AD in cui siano inclusi gli utenti che potranno vedere e applicare la nuova etichetta.
    
    Se non si ha un gruppo adatto, crearne uno denominato **Team vendite** e aggiungere almeno un utente.

4. Per testare la nuova etichetta: il client Azure Information Protection deve essere installato nei computer degli utenti. 
    
    Per provare l'etichetta, è possibile installare il client accedendo all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection.exe** dalla pagina di Azure Information Protection.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).
    
## <a name="create-a-new-label"></a>Creare una nuova etichetta

Per prima cosa, creare la nuova etichetta.

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Dall'opzione di menu **Classificazioni** > **Etichette**: Nel pannello **Azure Information Protection - Etichette** fare clic su **Aggiungi una nuova etichetta**.

3. Nel pannello **Etichetta** specificare almeno gli elementi seguenti:
    
    - **Nome visualizzato dell'etichetta**: il nome della nuova etichetta che sarà visibile agli utenti e che identifica la classificazione del contenuto. Ad esempio: `Sales - Restricted`.
    
    - **Description**: una descrizione comando che consenta agli utenti di capire quando è opportuno selezionare questa nuova etichetta. ad esempio `Business data that is restricted to the Sales Team.`

4. Assicurarsi che l'opzione **Abilitato** sia impostata su **Sì** (impostazione predefinita) e selezionare **Salva**.

## <a name="add-the-label-to-a-new-scoped-policy"></a>Aggiungere l'etichetta ai nuovi criteri con ambito

Aggiungere ora l'etichetta appena creata ai nuovi criteri con ambito.

1. Dall'opzione di menu **Classificazioni** > **Criteri**: Nel pannello **Azure Information Protection - Criteri** selezionare **Aggiungi un nuovo criterio**. 

2. Nel pannello **Criteri**, nella casella **Nome criterio**, immettere un nome che identifichi il gruppo di utenti che potranno vedere la nuova etichetta creata. Ad esempio, `Sales`

3. Selezionare l'opzione **Selezionare gli utenti o i gruppi a cui viene applicato il criterio**.

4. Nel pannello **Utenti e gruppi di AAD** selezionare **Utenti/Gruppi**. Quindi, nel nuovo pannello **Utenti/Gruppi** cercare e selezionare il gruppo identificato nei prerequisiti. Ad esempio: **Team vendite**. In questo pannello fare clic su **Seleziona** e quindi su **OK**.

5. Tornare al pannello **Criteri** e selezionare **Aggiungi o rimuovi etichette**.

6. Nel pannello **Criteri: Aggiungi o rimuovi etichette** selezionare l'etichetta creata, ad esempio **Vendite - Con restrizioni**, quindi selezionare **OK**.

7. Nel pannello **Criteri** fare clic su **Salva**. 

La nuova etichetta è ora pubblicata solo per i membri del gruppo specificato. 

## <a name="test-your-new-label"></a>Testare la nuova etichetta

Per testare questa etichetta sono necessari almeno due computer, poiché il client Azure Information Protection non supporta più utenti nello stesso computer:

 - Nel primo computer accedere come membro del gruppo Team vendite. Aprire Word e verificare che sia possibile visualizzare la nuova etichetta. Se Word è già aperto, riavviarlo per forzare un aggiornamento dei criteri.

- Nel secondo computer accedere come utente non membro del gruppo Team vendite. Aprire Word e verificare che non sia possibile visualizzare la nuova etichetta. Come in precedenza, se Word è già aperto, riavviarlo.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vuole mantenere questa etichetta e i criteri con ambito, seguire questa procedura:

1. Dall'opzione di menu **Classificazioni** > **Criteri**: nel pannello **Azure Information Protection - Criteri** selezionare il menu di scelta rapida ( **...** ) relativo ai criteri con ambito appena creati. Ad esempio: **Vendite**.

2. Selezionare **Elimina criteri** e, se viene richiesto di confermare l'operazione, scegliere **OK**.

3. Dall'opzione di menu **Classificazioni** > **Etichetta**: nel pannello **Azure Information Protection - Etichetta** selezionare il menu di scelta rapida ( **...** ) per l'etichetta appena creata.  Ad esempio: **Vendite - Con restrizioni**.

4.  Selezionare **Elimina questa etichetta** e, se viene richiesto di confermare l'operazione, scegliere **OK**.


## <a name="next-steps"></a>Passaggi successivi

Questa guida introduttiva include le informazioni strettamente indispensabili per creare rapidamente una nuova etichetta per utenti specifici. Per istruzioni complete, vedere gli articoli seguenti:

- [Come creare una nuova etichetta](configure-policy-new-label.md)

- [Come configurare i criteri per utenti specifici con i criteri con ambito](configure-policy-scope.md)

Se si vuole che l'etichetta protegga i contenuti in modo che possano essere aperti solo dai membri del Team vendite, è necessario configurare l'etichetta per l'applicazione della protezione. Per istruzioni, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md).

