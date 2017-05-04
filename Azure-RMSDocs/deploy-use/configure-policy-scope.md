---
title: Configurare i criteri con ambito per Azure Information Protection
description: "Per configurare impostazioni ed etichette diverse per utenti specifici, è necessario configurare un criterio con ambito per Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 253a08736352b04b4f730b250b888102836f7e6d
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito

>*Si applica a: Azure Information Protection*

Quando i criteri di Azure Information Protection vengono scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), a tutti gli utenti vengono applicate le impostazioni e le etichette dei criteri predefiniti o le modifiche configurate per i criteri globali. Se si vuole integrare questi criteri per utenti specifici, con impostazioni ed etichette diverse, è necessario creare **criteri con ambito** configurati per tali utenti.

Tutti gli utenti riceveranno i criteri globali contenenti titolo della barra e descrizione comando, impostazioni globali ed etichette globali di Information Protection. Se sono stati configurati criteri con ambito per utenti specifici, tali utenti riceveranno le impostazioni e le etichette aggiuntive. 

I criteri con ambiti, analogamente alle etichette, vengono ordinati nel portale di Azure. Se un utente è configurato per più ambiti, viene calcolato un criterio effettivo per tale utente prima del download. In base all'ordine dei criteri, viene applicata l'ultima impostazione dei criteri. Le etichette visualizzate dall'utente fanno parte dei criteri globali, mentre tutte le etichette aggiuntive fanno parte dei criteri con ambiti a cui l'utente appartiene. 

Poiché un criterio con ambito eredita sempre le etichette e le impostazioni dai criteri globali, tali etichette vengono visualizzate quando si crea o si modifica un criterio con ambito. Tuttavia, non è possibile modificare le etichette dei criteri globali quando si modifica un criterio con ambito. È comunque possibile aggiungere etichette secondarie a queste etichette ereditate.

Se ad esempio si ha un'etichetta denominata **Confidential** nei criteri globali, l'etichetta sarà visibile a tutti gli utenti. Non è possibile rimuovere né riordinare le etichette con un criterio con ambito. È possibile tuttavia creare un criterio con ambito per il reparto Marketing che aggiunga una nuova etichetta secondaria a Confidential in modo che gli utenti visualizzino **Confidential \ Promotions**. Viene anche creato un altro criterio con ambito per il reparto Vendite che aggiunge una nuova etichetta secondaria a Confidential in modo che gli utenti visualizzino **Confidential \ Partners**. Ogni etichetta secondaria può quindi essere configurato per diverse impostazioni e l'etichetta secondaria è visibile solo agli utenti dei rispettivi reparti.


Per configurare un criterio con ambito per Azure Information Protection:

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza.

2. Passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **More services** (Altri servizi) e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 

    Nel pannello iniziale di **Azure Information Protection** selezionare **Aggiungi un nuovo criterio**. Verrà quindi visualizzato il secondo pannello usato per mostrare l'aggiornamento dei criteri globali, in modo da potere configurare il nuovo criterio con ambito.

3. Specificare un nome e una descrizione per il criterio visibile solo agli amministratori nel portale di Azure. Il nome deve essere univoco nel tenant. Fare quindi clic su **Selezionare gli utenti/gruppi a cui viene applicato il criterio** e nei pannelli successivi è possibile cercare e selezionare gli utenti e i gruppi per questo criterio. Le etichette e le impostazioni configurate in questo criterio con ambito verranno applicate solo a tali utenti.

4. A questo punto creare nuove etichette o configurare le impostazioni dei criteri con ambito. I criteri globali vengono sempre applicati per primi, pertanto è possibile integrare i criteri globali con nuove etichette ed eseguire l'override delle impostazioni globali. Ad esempio, i criteri globali potrebbero non avere alcuna etichetta predefinita specificata ed è possibile configurare un'etichetta predefinita diversa in criteri con ambito diversi per reparti specifici.

    Se è necessario ottenere informazioni sulla configurazione delle impostazioni o delle etichette, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

5. Analogamente alla modifica dei criteri globali, quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Salva** per salvare le modifiche oppure su **Rimuovi** per ripristinare le ultime impostazioni salvate. 

6. Dopo avere apportato le modifiche desiderate a questo criterio con ambito, nel pannello iniziale di **Azure Information Protection** assicurarsi che il criterio con ambito sia nell'ordine in cui si vuole applicarlo. Questo aspetto è importante quando si seleziona lo stesso utente per più criteri con ambito. Fare quindi clic su **Pubblica**. 

Il client di Azure Information Protection ricerca eventuali modifiche ogni volta che viene avviata un'applicazione di Office supportata o viene aperto Esplora file. Il client scarica le eventuali modifiche dei criteri globali o dei criteri con ambito applicabili a tale utente.

> [!TIP]
> Dopo aver salvato i criteri con ambito, è possibile usare **Editor tra criteri** nel pannello iniziale **Azure Information Protection** per visualizzare e riconfigurare tutte le etichette dai criteri di Azure Information Protection. Questo metodo fornisce un modo semplice per confrontare le etichette da più criteri (i criteri globali e tutti i criteri con ambito). Questo editor non consente tuttavia di aggiungere o riordinare le etichette, né di visualizzare o configurare le impostazioni dei criteri.

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
