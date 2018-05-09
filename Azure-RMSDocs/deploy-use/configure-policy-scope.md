---
title: Configurare i criteri con ambito per Azure Information Protection
description: Per configurare impostazioni ed etichette diverse per utenti specifici, è necessario configurare un criterio con ambito per Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: b5e7bd86ea2e46939b8c4655287e58e3e270feb4
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Quando i criteri di Azure Information Protection vengono scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), a tutti gli utenti vengono applicate le impostazioni e le etichette dei criteri predefiniti o le modifiche configurate per i criteri globali. Se si vuole integrare questi criteri per utenti specifici, con impostazioni ed etichette diverse, è necessario creare **criteri con ambito** configurati per tali utenti.

Per le applicazioni che supportano il client di Azure Information Protection, tutti gli utenti ricevono i criteri globali, che contengono titolo della barra, descrizione comando, impostazioni globali ed etichette globali di Information Protection. Se sono stati configurati criteri con ambito per utenti specifici, tali utenti riceveranno le impostazioni e le etichette aggiuntive. 

Si noti che oltre alle applicazioni desktop di Office che supportano il client di Azure Information Protection, le etichette sono supportate anche con PowerShell e lo scanner di Azure Information Protection. Ciò significa che è possibile creare e configurare criteri con ambito per gli account che eseguono i comandi di Powershell o lo scanner. 

I criteri con ambiti, analogamente alle etichette, vengono ordinati nel portale di Azure. Se un utente è configurato per più ambiti, viene calcolato un criterio effettivo per tale utente prima del download. In base all'ordine dei criteri, viene applicata l'ultima impostazione dei criteri. Le etichette visualizzate dall'utente fanno parte dei criteri globali, mentre tutte le etichette aggiuntive fanno parte dei criteri con ambiti a cui l'utente appartiene. 

Poiché un criterio con ambito eredita sempre le etichette e le impostazioni dai criteri globali, tali etichette vengono visualizzate quando si crea o si modifica un criterio con ambito. Tuttavia, non è possibile modificare le etichette dei criteri globali quando si modifica un criterio con ambito. È comunque possibile aggiungere etichette secondarie a queste etichette ereditate.

Se ad esempio si ha un'etichetta denominata **Confidential** nei criteri globali, l'etichetta sarà visibile a tutti gli utenti. Non è possibile rimuovere né riordinare le etichette con un criterio con ambito. È possibile tuttavia creare un criterio con ambito per il reparto Marketing che aggiunga una nuova etichetta secondaria a Confidential in modo che gli utenti visualizzino **Confidential \ Promotions**. Viene anche creato un altro criterio con ambito per il reparto Vendite che aggiunge una nuova etichetta secondaria a Confidential in modo che gli utenti visualizzino **Confidential \ Partners**. Ogni etichetta secondaria può quindi essere configurata per diverse impostazioni e l'etichetta secondaria è visibile solo agli utenti dei rispettivi reparti.

Per configurare un criterio con ambito per Azure Information Protection:

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.

    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **CLASSIFICAZIONI** > **Criteri**: nel pannello **Azure Information Protection - Criteri** selezionare **Aggiungi un nuovo criterio**. Viene visualizzato il pannello **Criteri** con i criteri globali esistenti. Nel pannello ora è possibile configurare i nuovi criteri con ambito.

3. Specificare un nome e una descrizione per il criterio visibile solo agli amministratori nel portale di Azure. Il nome deve essere univoco nel tenant. Quindi selezionare **Specify which users/groups get this policy** (Specificare gli utenti e i gruppi ai quali applicare i criteri) e nei pannelli successivi cercare e selezionare gli utenti e i gruppi per i criteri. Le etichette e le impostazioni configurate in questo criterio con ambito verranno applicate solo a tali utenti.
    
    Per motivi di prestazioni, l'appartenenza ai gruppi per i criteri con ambito è [memorizzata nella cache](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection).

4. A questo punto aggiungere nuove etichette o configurare le impostazioni dei criteri con ambito. I criteri globali vengono sempre applicati per primi, pertanto è possibile integrare i criteri globali con nuove etichette ed eseguire l'override delle impostazioni globali. Ad esempio, i criteri globali potrebbero non avere alcuna etichetta predefinita specificata ed è possibile configurare un'etichetta predefinita diversa in criteri con ambito diversi per reparti specifici.

    Se è necessario ottenere informazioni sulla configurazione delle impostazioni o delle etichette, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

6. Analogamente alla modifica dei criteri globali, quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Salva** per salvare le modifiche oppure su **Rimuovi** per ripristinare le ultime impostazioni salvate. 

7. Una volta completate le modifiche ai criteri con ambito, nel pannello **Azure Information Protection - Criteri** iniziale verificare che questi criteri con ambito siano visualizzati nell'ordine in cui si desidera che vengano applicati. Questo aspetto è importante quando si seleziona lo stesso utente per più criteri con ambito. Per modificare l'ordine, selezionare il menu di scelta rapida (**...**) e scegliere **Sposta su** o **Sposta giù**. 

Il client di Azure Information Protection ricerca eventuali modifiche ogni volta che viene avviata un'applicazione di Office supportata o viene aperto Esplora file. Il client scarica le eventuali modifiche dei criteri globali o dei criteri con ambito applicabili a tale utente.

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
