---
title: Configurare i criteri con ambito per Azure Information Protection
description: "Per configurare impostazioni ed etichette diverse per utenti specifici, è necessario configurare un criterio con ambito per Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c7aa1c3aa18a246457c00a5a61c6004e55f76b4b
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Come configurare i criteri di Azure Information Protection per utenti specifici attraverso criteri con ambito

>*Si applica a: Azure Information Protection*

Quando i criteri di Azure Information Protection vengono scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), a tutti gli utenti vengono applicate le impostazioni e le etichette dei criteri predefiniti o le modifiche configurate per i criteri globali. Se si desidera integrare tali criteri per utenti specifici con impostazioni ed etichette diverse, è necessario creare **criteri con ambito**configurati per tali utenti.

Tutti gli utenti riceveranno i criteri globali, i quali contengono titolo della barra e descrizione comando, impostazioni globali ed etichette globali di Information Protection. Se sono stati configurati criteri con ambito per utenti specifici, tali utenti riceveranno le impostazioni e le etichette aggiuntive. 

I criteri con ambito, analogamente alle etichette, vengono ordinati nel portale di Azure. Se un utente è configurato per più ambiti, viene calcolato un criterio valido per tale utente prima del download. In base all'ordine dei criteri, viene applicata l'ultima impostazione dei criteri. Le etichette visualizzate dall'utente fanno parte dei criteri globali, mentre tutte le etichette aggiuntive fanno parte dei criteri con ambito a cui l'utente appartiene. 

Poiché un criterio con ambito eredita sempre le etichette e le impostazioni dai criteri globali, tali etichette vengono visualizzate quando si crea o si modifica un criterio con ambito. Tuttavia, non è possibile modificare le etichette dei criteri globali quando si modifica un criterio con ambito, ma è comunque possibile aggiungere etichette secondarie a queste etichette ereditate.

Ad esempio, se si ha un'etichetta denominata **Confidential** (Confidenziale) nei criteri globali, l'etichetta sarà visibile a tutti gli utenti. Non è possibile rimuovere né riordinare le etichette con un criterio con ambito. È possibile tuttavia creare un criterio con ambito per il reparto Marketing che aggiunga una nuova etichetta secondaria a Confidential (Confidenziale), in modo che tali utenti visualizzino **Confidential \ Promotions** (Confidenziale \ Promozioni). Viene creato anche un altro criterio con ambito per il reparto Vendite, il quale aggiunge una nuova etichetta secondaria a Confidential (Confidenziale), in modo che gli utenti visualizzino **Confidential \ Partners** (Confidenziale \ Partner). Ogni etichetta secondaria può quindi essere configurata per diverse impostazioni ed è visibile solo agli utenti dei rispettivi reparti.

Per configurare un criterio con ambito per Azure Information Protection:

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza, quindi passare al pannello **Azure Information Protection**. 

    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel menu **CRITERI** selezionare **Criteri con ambito**.

3. Nel pannello **Azure Information Protection - Criteri con ambito** selezionare **Aggiungi un nuovo criterio**. Verrà visualizzato il pannello **Criteri** con i criteri globali esistenti, in cui sarà possibile configurare i nuovi criteri con ambito.

4. Specificare un nome e una descrizione per il criterio visibile solo agli amministratori nel portale di Azure. ll nome deve essere univoco nel tenant. Selezionare quindi **Specify which users/groups get this policy** (Specificare gli utenti e i gruppi ai quali applicare i criteri) e nei pannelli successivi cercare e selezionare gli utenti e i gruppi di tali criteri. Le etichette e le impostazioni configurate in questo criterio con ambito verranno applicate solo a tali utenti.
    
    Per motivi di prestazioni, l'appartenenza ai gruppi per i criteri con ambito viene [memorizzata nella cache](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection).

5. A questo punto, creare nuove etichette o configurare le impostazioni dei criteri con ambito. I criteri globali vengono sempre applicati per primi, pertanto è possibile integrare i criteri globali con nuove etichette ed eseguire l'override delle impostazioni globali. Ad esempio, i criteri globali potrebbero non avere alcuna etichetta predefinita specificata ed è possibile configurare un'etichetta predefinita diversa in criteri con ambito diversi per reparti specifici.

    Se è necessario ottenere informazioni sulla configurazione delle etichette o delle impostazioni, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

6. Analogamente alla modifica dei criteri globali, quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Salva** per salvare le modifiche, oppure su **Rimuovi** per ripristinare le ultime impostazioni salvate. 

7. Una volta completate le modifiche ai criteri con ambito, nel pannello iniziale **Azure Information Protection - Criteri con ambito** verificare che questi criteri con ambito siano visualizzati nell'ordine in cui si desidera che vengano applicati. Si tratta di un aspetto importante quando si seleziona lo stesso utente per più criteri con ambito. Per modificare l'ordine, selezionare il menu di scelta rapida (**...**) e scegliere **Sposta su** o **Sposta giù**. 

8. Per distribuire le modifiche, fare clic su **Pubblica**. 

Il client di Azure Information Protection ricerca eventuali modifiche ogni volta che viene avviata un'applicazione di Office supportata o viene aperto Esplora file. Il client scarica le eventuali modifiche dei criteri globali o dei criteri con ambito applicabili a tale utente.

> [!TIP]
> Dopo aver salvato i criteri con ambito, nella sezione **CRITERI** è possibile usare l'opzione **Tutti - visualizzazione tra criteri** per visualizzare e riconfigurare tutte le etichette dai criteri di Azure Information Protection. Si tratta di un metodo semplice per confrontare le etichette tra i criteri globali e tutti i criteri con ambito. 

## <a name="next-steps"></a>Passaggi successivi

Per un esempio su come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
