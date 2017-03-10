---
title: Configurare i criteri di Azure Information Protection
description: "Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 64a3daa57d71087d11098a1e71465f17b6b8f3b7
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="configuring-azure-information-protection-policy"></a>Configurazione dei criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection. Questi criteri vengono quindi scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Per configurare i criteri di Azure Information Protection:

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale.

2. Passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **More services** (Altri servizi) e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 

    Verrà quindi visualizzato il pannello di **Azure Information Protection**, dove è possibile aprire il criterio **Globale** assegnato a tutti gli utenti. È anche possibile aggiungere e modificare i criteri con ambito. Il criterio **Globale** di Azure Information Protection contiene gli elementi seguenti che è possibile configurare:

    - Etichette che consentono agli utenti di classificare i documenti e i messaggi di posta elettronica.

    - Titolo e descrizione comando della barra Information Protection visualizzata nelle applicazioni di Office.

    - Opzione per applicare la classificazione quando gli utenti salvano documenti e inviano messaggi di posta elettronica.

    - Opzione per impostare un'etichetta predefinita come punto di partenza per la classificazione di documenti e messaggi di posta elettronica.

    - Opzione per richiedere agli utenti di specificare un motivo quando selezionano un'etichetta con un livello di riservatezza inferiore rispetto all'originale.

    - Opzione per fornire un collegamento alla guida personalizzata per gli utenti.

Azure Information Protection include un [criterio predefinito](configure-policy-default.md), che contiene le etichette **Personal** (Personale), **Public** (Pubblico), **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto). È possibile usare le etichette predefinite così come sono oppure personalizzarle, eliminarle e crearne di nuove.

Quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Save** (Salva) per salvare le modifiche oppure su **Discard** (Ignora) per ripristinare le ultime impostazioni salvate. 

Dopo avere apportato le modifiche desiderate, fare clic su **Publish** (Pubblica). 

Il client di Azure Information Protection ricerca eventuali modifiche ogni volta che viene avviata dell'applicazione di Office supportata e scarica le modifiche come proprio criterio di Azure Information Protection.

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
