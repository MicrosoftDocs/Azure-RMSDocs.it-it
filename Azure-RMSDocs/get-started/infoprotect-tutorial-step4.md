---
title: Esercitazione per l'avvio rapido - Passaggio 4 - AIP
description: 'Passaggio 4 di un''esercitazione introduttiva per provare rapidamente a usare Azure Information Protection: vedere in azione le funzioni di aggiunta di etichette e protezione.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/14/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: d397ed8290d8b792b55ee78865cdbd41e330f8a9
ms.sourcegitcommit: d42c6bb914563ae798d4171bb017c85b7077abfb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2017
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>Passaggio 4: Funzioni di classificazione, aggiunta di etichette e protezione in azione 

>*Si applica a: Azure Information Protection*

Con un documento di Word aperto e il client di Azure Information Protection installato è possibile rendersi conto di quanto sia facile aggiungere etichette e proteggere il documento usando il criterio configurato.

La classificazione e la protezione hanno effetto quando si salva il documento. Prima del salvataggio, tuttavia, il documento verrà usato per dimostrare con quale facilità è possibile applicare e modificare le etichette.

## <a name="to-manually-change-our-default-label"></a>Per modificare manualmente l'etichetta predefinita

Sulla barra di Information Protection selezionare l'ultima etichetta e osservare come vengono visualizzate le etichette secondarie:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: scegliere un'etichetta secondaria](../media/info-protect-sub-labelsv2.png)

Selezionare una delle etichette secondarie e osservare come le altre etichette non vengono più visualizzate sulla barra ora che si è selezionata un'etichetta per il documento. Il valore **Sensitivity** (Riservatezza) cambia per visualizzare il nome dell'etichetta principale e secondaria con una corrispondente variazione del colore dell'etichetta. Ad esempio:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: etichetta secondaria selezionata](../media/info-protect-sub-label-selectedv2.png)

Sulla barra di Information Protection fare clic sull'icona **Edit Label** (Modifica l'etichetta) che si trova accanto al valore dell'etichetta selezionata:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: icona Modifica l'etichetta](../media/info-protect-edit-label-selectedv2.png)

Verranno visualizzate le etichette disponibili.

Selezionare la prima etichetta, **Personal**. Poiché è stata selezionata un'etichetta classificata a un livello inferiore rispetto a quella selezionata in precedenza per questo documento, viene chiesto di giustificare il motivo per cui si sta abbassando il livello di classificazione:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Richiesta di giustificazione dell'abbassamento](../media/info-protect-lower-justification.png)

Selezionare **L'etichetta precedente non è più applicabile** e fare clic su **Conferma**. Il valore **Sensitivity** (Riservatezza) diventa **Personale** e le altre etichette vengono nuovamente nascoste.

## <a name="to-remove-the-classification-completely"></a>Per rimuovere completamente la classificazione

Sulla barra di Information Protection, fare nuovamente clic sull'icona **Modifica l'etichetta**. Tuttavia, anziché scegliere una delle etichette, fare clic sull'icona **Elimina l'etichetta**:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: icona Elimina l'etichetta](../media/delete-icon-from-personalv2.png)

Questa volta, quando richiesto, digitare "Il documento non richiede la classificazione" e fare clic su **Conferma**.  

Per il valore **Sensitivity** (Riservatezza) viene visualizzato **Non impostato**, come avviene inizialmente se non si imposta un'etichetta predefinita:

![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Rimuovere la classificazione](../media/sensitivity-not-setv2.png)


## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Per visualizzare un messaggio di azione consigliata per l'assegnazione di etichette e la protezione automatica

1. Nel documento di Word, digitare un numero di carta di credito valido, ad esempio: **4242-4242-4242-4242**. 

2. Salvare il documento con qualsiasi nome file e qualsiasi percorso. 

3. Viene visualizzata ora un prompt per applicare l'etichetta configurata per la protezione quando vengono rilevati numeri di carta di credito. Se non si è d'accordo con il suggerimento, l'impostazione dei criteri consente di rifiutarlo, selezionando **Dismiss** (Ignora). La disponibilità di un suggerimento con la possibilità di ignorarlo consente agli utenti di ridurre i falsi positivi quando si usa una classificazione automatica. Per questa esercitazione, fare clic su **Change now** (Modifica ora).

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Messaggio di azione consigliata](../media/change-nowv2.png)

    Oltre al documento che indica ora che l'etichetta configurata è applicata, ad esempio **Confidential \ All Employees** (Riservato \ Tutti i dipendenti), verrà immediatamente visualizzata la filigrana del nome dell'organizzazione sulla pagina e viene anche applicato il piè di pagina **Classificato come Riservato**. 

    Il documento è protetto anche dal modello di Azure Rights Management specificato, che è possibile confermare quando si fa clic sulla scheda **File** e si visualizzano le informazioni in **Proteggi documento**. Se si usa il modello Confidential (Riservato), verrà visualizzata l'informazione che il documento è riservato agli utenti interni. Gli utenti esterni all'organizzazione non potranno aprire il documento e il suo contenuto non potrà essere copiato o stampato. Il proprietario del documento può copiarne il contenuto e stamparlo, ma se lo invia tramite posta elettronica a un altro utente dell'organizzazione, quest'ultimo non sarà in grado di eseguire queste azioni.

4. È ora possibile chiudere il documento.

I passaggi eseguiti fino a ora hanno consentito di vedere in azione la classificazione, l'assegnazione di etichette e la protezione. Nei passaggi successivi verrà mostrato come proteggere i documenti anche quando vengono condivisi con altri utenti dell'organizzazione. Verrà inoltre mostrato come è possibile tenere traccia del modo in cui tali documenti vengono usati e verrà spiegato come revocarne l'accesso.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Istruzioni complete per l'assegnazione di etichette e la protezione dei file |[Classificare e proteggere un file o un messaggio di posta elettronica](../rms-client/client-classify-protect.md)|





>[!div class="step-by-step"]
[&#171; Passaggio 3](infoprotect-tutorial-step3.md)
[Passaggio 5 &#187;](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]