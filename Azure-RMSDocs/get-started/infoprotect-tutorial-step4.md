---
title: Esercitazione introduttiva, passaggio 4 | Azure Rights Management
description: Passaggio 3 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esecuzione dell'esercitazione richiede circa 30 minuti.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: ce1d0a700e0b69d71f5cb2e93f406124bc0ca581
ms.openlocfilehash: c9ed50317e18e86438b4393ce629d23d433c99fe


---

# Passaggio 4: Funzioni di classificazione, aggiunta di etichette e protezione in azione 

>*Si applica a: Azure Information Protection*

Con un documento di Word aperto e il client di Azure Information Protection installato è possibile rendersi conto di quanto sia facile aggiungere etichette e proteggere il documento usando il criterio configurato.

La classificazione e la protezione hanno effetto quando si salva il documento. Prima del salvataggio, tuttavia, il documento verrà usato per dimostrare con quale facilità è possibile aggiungere e modificare etichette.

## Per modificare manualmente l'etichetta predefinita

Sulla barra di Information Protection scegliere l'etichetta **Personal** (Personale). Verrà richiesto di giustificare l'abbassamento del livello di classificazione:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Richiesta di giustificazione dell'abbassamento](../media/info-protect-lower-justification.png)

Selezionare **The previous label no longer applies** (L'etichetta precedente non viene più applicata) e fare clic su **Confirm** (Conferma). Il valore **Sensitivity** (Riservatezza) cambierà in **Personal** (Personale).

## Per rimuovere completamente la classificazione

Sulla barra di Information Protection fare clic sull'icona **Modifica etichetta** accanto a **Personal** (Personale). Verranno visualizzate le etichette disponibili. Ma questa volta, anziché scegliere una delle etichette, fare clic sull'icona **Rimuovi etichetta**. Fare clic su **OK** per confermare e quindi fornire la giustificazione per questa azione.  

Per il valore **Sensitivity** (Riservatezza) verrà visualizzato **Not set** (Non impostato), come avviene inizialmente se non si imposta un'etichetta predefinita:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Rimuovere la classificazione](../media/sensitivity-not-set.png)


## Per visualizzare un messaggio di azione consigliata per l'assegnazione di etichette e la protezione automatica

1. Nel documento di Word, digitare un numero di carta di credito valido, ad esempio: **4242-4242-4242-4242**. 

2. Salvare il documento con qualsiasi nome file e qualsiasi percorso. 

3. È ora visualizzato il messaggio: **It is recommended to label this file as Confidential** (È consigliabile etichettare il file come Riservato). Fare clic su **Change now** (Cambia adesso).

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Messaggio di azione consigliata](../media/change-now.png)

    Oltre al documento con l'etichetta impostata su Confidential (Riservato), verrà immediatamente visualizzata la filigrana dell'organizzazione. Verrà inoltre inserito il piè di pagina **Sensitivity: Confidential** (Riservatezza: Riservato). 

    Il documento è protetto anche dal modello di Azure Rights Management specificato, che è possibile confermare quando si fa clic sulla scheda **File** e si visualizzano le informazioni in **Proteggi documento**. Se si usa il modello Confidential (Riservato), verrà visualizzata l'informazione che il documento è riservato agli utenti interni. Gli utenti esterni all'organizzazione non potranno aprire il documento e il suo contenuto non potrà essere copiato o stampato. Il proprietario del documento può copiarne il contenuto e stamparlo, ma se lo invia tramite posta elettronica a un altro utente dell'organizzazione, quest'ultimo non sarà in grado di eseguire queste azioni.

I passaggi eseguiti fino a ora hanno consentito di vedere in azione la classificazione, l'assegnazione di etichette e la protezione. Nei passaggi successivi verrà mostrato come proteggere i documenti anche quando vengono condivisi con altri utenti dell'organizzazione. Verrà inoltre mostrato come è possibile tenere traccia del modo in cui tali documenti vengono usati e verrà spiegato come revocarne l'accesso.

>[!div class="step-by-step"]
[&#171; Passaggio 3](infoprotect-tutorial-step3.md)
[Passaggio 5 &#187;](infoprotect-tutorial-step5.md)



<!--HONumber=Sep16_HO4-->


