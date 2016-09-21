---
title: Configurazione di criteri di Azure Information Protection | Azure Information Protection
description: "Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 801ca11da602d4acb9c398c9a89aeb33e45cb0f4
ms.openlocfilehash: ba7acf835439d059874e0512997b2b591193f0c3


---

# Configurazione dei criteri di Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection. Questi criteri vengono quindi scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Per configurare i criteri di Azure Information Protection nella versione di anteprima di Azure Information Protection:

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com).

2. Passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **More services** (Altri servizi) e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 

    Verrà quindi visualizzato il pannello **Azure Information Protection** in cui è possibile configurare i criteri di Azure Information Protection, che contiene gli elementi seguenti:

    - Titolo e descrizione comando della barra Information Protection visualizzata nelle applicazioni di Office.

    - Etichette che consentono agli utenti di classificare i documenti e i messaggi di posta elettronica.

    - Opzione per applicare la classificazione quando gli utenti salvano documenti e inviano messaggi di posta elettronica.

    - Opzione per impostare un'etichetta predefinita come punto di partenza per la classificazione di documenti e messaggi di posta elettronica.

    - Opzione per richiedere agli utenti di specificare un motivo quando selezionano un'etichetta con un livello di riservatezza inferiore rispetto all'originale.


Azure Information Protection include un [criterio predefinito](configure-policy-default.md), che contiene le etichette **Personal** (Personale), **Public** (Pubblico), **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto). È possibile usare le etichette predefinite così come sono oppure personalizzarle, eliminarle e crearne di nuove.

Quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Save** (Salva) per salvare le modifiche oppure su **Discard** (Ignora) per ripristinare le ultime impostazioni salvate. 

Dopo avere apportato le modifiche desiderate, fare clic su **Publish** (Pubblica). 

Il client di Azure Information Protection ricerca eventuali modifiche ogni volta che viene avviata dell'applicazione di Office supportata e scarica le modifiche come proprio criterio di Azure Information Protection.

## Configurazione dei criteri dell'organizzazione

Usare le informazioni seguenti per configurare i criteri di Azure Information Protection:

- [Criterio predefinito di Information Protection](configure-policy-default.md)

- [Come configurare le impostazioni dei criteri globali](configure-policy-settings.md)

- [Come creare una nuova etichetta](configure-policy-new-label.md)

- [Come eliminare o riordinare un'etichetta](configure-policy-delete-reorder.md)

- [Come modificare o personalizzare un'etichetta esistente](configure-policy-change-label.md)

- [Come configurare un'etichetta per applicare la protezione](configure-policy-protection.md)

- [Come configurare un'etichetta per applicare i contrassegni visivi](configure-policy-markings.md)

- [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)

## Passaggi successivi

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Sep16_HO3-->


