---
title: Configurare i criteri di Azure Information Protection
description: "Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: f412d36e8c58d874360c55c5c90416c2629ed69e
ms.sourcegitcommit: e3974cc1490581414084669632cad54b12b05d5a
ms.translationtype: HT
ms.contentlocale: it-IT
---
# <a name="configuring-azure-information-protection-policy"></a>Configurazione dei criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection. Questi criteri vengono quindi scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Per configurare i criteri di Azure Information Protection:

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza.

2. Passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **More services** (Altri servizi) e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 

    Quando il pannello **Azure Information Protection** viene caricato, il pannello **Criteri: Globale** viene aperto automaticamente per consentire di visualizzare e modificare i criteri globali ottenuti da tutti gli utenti. È tuttavia possibile anche aggiungere e modificare i criteri con ambito. I criteri di Azure Information Protection contengono gli elementi seguenti che è possibile configurare:

    - Etichette che consentono agli utenti di classificare i documenti e i messaggi di posta elettronica.

    - Titolo e descrizione comando della barra Information Protection visualizzata nelle applicazioni di Office.

    - Opzione per applicare la classificazione quando gli utenti salvano documenti e inviano messaggi di posta elettronica.

    - Opzione per impostare un'etichetta predefinita come punto di partenza per la classificazione di documenti e messaggi di posta elettronica.

    - Opzione per richiedere agli utenti di specificare un motivo quando selezionano un'etichetta con un livello di riservatezza inferiore rispetto all'originale.

    - Opzione per etichettare automaticamente un messaggio di posta elettronica, in base ai relativi allegati.

    - Opzione per fornire un collegamento alla guida personalizzata per gli utenti.

Azure Information Protection viene distribuito con [criteri predefiniti](configure-policy-default.md), che contengono cinque etichette principali. Queste etichette sono utilizzabili con l'intera gamma di dati che un'organizzazione in genere crea e archivia, dalla classificazione minima dei dati personali alla classificazione più elevata di dati particolarmente riservati. È possibile usare le etichette predefinite così come sono oppure personalizzarle, eliminarle e crearne di nuove.

Quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Save** (Salva) per salvare le modifiche oppure su **Discard** (Ignora) per ripristinare le ultime impostazioni salvate. 

Dopo avere apportato le modifiche desiderate, fare clic su **Publish** (Pubblica). 

Il client Azure Information Protection verifica la disponibilità di eventuali modifiche ogni volta che viene avviata un'applicazione di Office supportata e scarica le modifiche come criteri di Azure Information Protection più recenti. I criteri del client vengono aggiornati anche nei modi seguenti:

- Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella.

- Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione (Get-AIPFileStatus e Set-AIPFileLabel).

- Ogni 24 ore.

>[!NOTE]
>Quando il client scarica i criteri, prevedere un'attesa di alcuni minuti prima che ritorni completamente operativo. Il tempo effettivo varia a seconda di fattori quali le dimensioni e la complessità della configurazione dei criteri e la connettività di rete. Se l'azione risultante delle etichette non corrisponde alle ultime modifiche, attendere fino a 15 minuti e riprovare.

## <a name="configuring-your-organizations-policy"></a>Configurazione dei criteri dell'organizzazione

Usare le informazioni seguenti per configurare i criteri di Azure Information Protection:

- [Criteri predefiniti di Information Protection](configure-policy-default.md)

- [Come configurare le impostazioni dei criteri](configure-policy-settings.md)

- [Come creare una nuova etichetta](configure-policy-new-label.md)

- [Come eliminare o riordinare un'etichetta](configure-policy-delete-reorder.md)

- [Come modificare o personalizzare un'etichetta esistente](configure-policy-change-label.md)

- [Come configurare un'etichetta per la protezione](configure-policy-protection.md)

- [Come configurare un'etichetta per applicare i contrassegni visivi](configure-policy-markings.md)

- [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)

- [Come configurare i criteri per utenti specifici con i criteri con ambito](configure-policy-scope.md)

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
