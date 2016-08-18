---
title: Esercitazione introduttiva di Azure Information Protection, passaggio 4 | Azure Rights Management
description: "Passaggio 4 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in meno di 15 minuti."
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: d17bacf8e148622db0e2393f40d3fd37c8f086eb
ms.openlocfilehash: a36433167462275e91059f9eb3a2141ffa2797d5


---

# Passaggio 4: Funzioni di classificazione, aggiunta di etichette e protezione in azione 

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Con un documento di Word aperto e il client di Azure Information Protection installato è possibile rendersi conto di quanto sia facile aggiungere etichette e proteggere il documento usando il criterio configurato.

La classificazione e la protezione hanno effetto quando si salva il documento. Prima del salvataggio, tuttavia, il documento verrà usato per dimostrare con quale facilità è possibile aggiungere e modificare etichette.

### Per modificare manualmente l'etichetta predefinita:

- Sulla barra di Information Protection scegliere l'etichetta **Personal** (Personale). Verrà richiesto di giustificare l'abbassamento del livello di classificazione. Selezionare **This file no longer requires that classification** (Il file non richiede più questa classificazione) e fare clic su **Conferma**.  

    Il valore **Sensitivity** (Riservatezza) cambierà in **Personal** (Personale).

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Richiesta di giustificazione dell'abbassamento](../media/confirm-lowering.png)

### Per rimuovere completamente la classificazione:

- Sulla barra di Information Protection fare clic sull'icona **Modifica etichetta** accanto a **Personal** (Personale). Verranno visualizzate le etichette disponibili. Ma questa volta, anziché scegliere una delle etichette, fare clic sull'icona **Rimuovi etichetta**. Fare clic su **OK** per confermare e quindi fornire la giustificazione per questa azione.  

    Per il valore **Sensitivity** (Riservatezza) verrà visualizzato **Non impostato**, come avviene inizialmente se non si imposta un'etichetta predefinita.

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Rimuovere la classificazione](../media/sensitivity-not-set.png)


### Per visualizzare un messaggio di azione consigliata per l'aggiunta di etichette e la protezione automatica:

1. Nel documento di Word, digitare un numero di carta di credito valido, ad esempio: **4242-4242-4242-4242**. 

2. Salvare il documento con qualsiasi nome file e qualsiasi percorso. 

3. È ora visualizzato il messaggio: **It is recommended to label this file as Confidential** (È consigliabile etichettare il file come Riservato). Fare clic su **Change now** (Cambia adesso).

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 4: Messaggio di azione consigliata](../media/change-now.png)

    Attraverso la pagina verrà immediatamente visualizzata la filigrana dell'organizzazione, oltre al piè di pagina **Sensitivity: Confidential** (Riservatezza: Riservato). 

    Se si è scelto di applicare un modello RMS, il documento è protetto anche dal modello di Azure Rights Management specificato, che è possibile confermare quando si fa clic sulla scheda **File** e si visualizzano le informazioni in **Proteggi documento**. Se si usa il modello Confidential (Riservato), verrà visualizzata l'informazione che il documento è riservato agli utenti interni. Gli utenti esterni all'organizzazione non potranno aprire il documento e il suo contenuto non potrà essere copiato o stampato. Il proprietario del documento può copiarne il contenuto e stamparlo, ma se lo invia tramite posta elettronica a un altro utente dell'organizzazione, quest'ultimo non sarà in grado di eseguire queste azioni.

> [!NOTE]
>In caso di problemi durante l'esecuzione di questi passaggi, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi fare clic su **Guida e commenti**. 
>
>Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **Invia commenti e suggerimenti**. Verrà inviato un messaggio di posta elettronica al team di Information Protection. Al messaggio verranno allegati automaticamente i file di log del PC per consentire la diagnosi di eventuali problemi.

##  Passaggi successivi

Dopo aver esaminato il criterio predefinito di Azure Information Protection e dopo aver scoperto come personalizzarlo, oltre ad aver appreso come funziona l'aggiunta di etichette per un documento di Word, è consigliabile provare qualcuna delle altre impostazioni e verificarne il funzionamento in altre applicazioni di Office che supportano Azure Information Protection: Excel, PowerPoint, Outlook. Se al momento dell'installazione del client di Azure Information Protection queste applicazioni erano aperte, chiuderle e riaprirle prima di provare a usarle con Azure Information Protection.

Ad esempio, è possibile sostituire il titolo predefinito **Sensitivity** (Riservatezza) sulla barra di Information Protection con un titolo a scelta. È possibile modificare le descrizioni, i colori, l'ordine e il nome delle etichette. È possibile creare nuove etichette e definire regole automatiche personalizzate. È possibile ritoccare le filigrane configurandone le dimensioni e il colore e modificarle da diagonali a orizzontali.

Si noti che in Excel le filigrane sono visibili solo nelle modalità Layout di pagina e Anteprima di stampa, oltre che sulla stampa.

Ogni volta che si modifica una qualsiasi impostazione nel portale di Azure per i criteri di Information Protection, ricordarsi di **salvare** il criterio e quindi di **pubblicarlo**. Poiché è possibile apportare modifiche in più pannelli, è consigliabile verificare che in tutti i pannelli il pulsante **Save** (Salva) sia disabilitato. In caso contrario, sono presenti modifiche non salvate. Se al momento della pubblicazione di nuove modifiche l'applicazione di Office era aperta, chiuderla e riaprirla per scaricare i criteri più recenti.

Dopo aver eseguito un test per proprio conto, può essere utile vedere le [domande frequenti per Azure Information Protection](faq.md).




<!--HONumber=Aug16_HO2-->


