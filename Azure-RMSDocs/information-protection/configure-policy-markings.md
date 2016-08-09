---
title: Come configurare un'etichetta per i contrassegni visivi per Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 9f2d28e4f162891497a7b0518322338628118b9d


---

# Come configurare un'etichetta per i contrassegni visivi per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Quando si assegna un'etichetta a un documento o a un messaggio di posta elettronica, è possibile selezionare diverse opzioni per rendere facilmente visibile la classificazione scelta. Questi contrassegni visivi sono un'intestazione, un piè di pagina e una filigrana:

I contrassegni visivi vengono applicati ai documenti di Word, Excel e PowerPoint quando viene applicata l'etichetta e quando viene salvato il documento. Per i messaggi di posta elettronica, i contrassegni visivi vengono applicati all'invio del messaggio.

Altre informazioni su questi contrassegni visivi:

- Intestazioni e piè di pagina si applicano a Word, Excel, PowerPoint e Outlook.

- Le filigrane si applicano a Word, Excel e PowerPoint:

    - Excel: le filigrane sono visibili solo nelle modalità Layout di pagina e Anteprima di stampa, oltre che sulla stampa.

    - PowerPoint: le filigrane vengono applicate alla diapositiva master, come immagine di sfondo.

Seguire le istruzioni seguenti per configurare i contrassegni visivi per un'etichetta.

1. Accedere al [portale di Azure](https://portal.azure.com).
 
2. Nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

3. Nel pannello **Azure Information Protection** selezionare l'etichetta da configurare per i contrassegni visivi.

4. Nel pannello **Label** (Etichetta), nella sezione **Set visual marking (such as header or footer)** (Imposta contrassegno visivo, ad esempio intestazione o piè di pagina), configurare le impostazioni per i contrassegni visivi desiderati e quindi fare clic su **Save** (Salva):

    - Per configurare un'intestazione: per **Documents with this label have a header** (I documenti con questa etichetta hanno un'intestazione) selezionare **Sì** se si vuole usare un'intestazione, altrimenti **No**. Se si seleziona **Sì**, specificare il testo, le dimensioni, il colore e l'allineamento per l'intestazione.

    - Per configurare un piè di pagina: per **Documents with this label have a footer** (I documenti con questa etichetta hanno un piè di pagina) selezionare **Sì** se si vuole usare un piè di pagina, altrimenti **No**. Se si seleziona **Sì**, specificare il testo, le dimensioni, il colore e l'allineamento per il piè di pagina.

    - Per configurare una filigrana: per **Documents with this label have a watermark** (I documenti con questa etichetta hanno una filigrana) selezionare **Sì** se si vuole usare una filigrana, altrimenti **No**. Se si seleziona **Sì**, specificare il testo, le dimensioni, il colore e il layout per la filigrana.

5. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Jul16_HO5-->


