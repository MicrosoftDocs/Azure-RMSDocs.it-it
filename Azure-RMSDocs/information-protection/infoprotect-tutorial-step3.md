---
title: Esercitazione introduttiva di Azure Information Protection, passaggio 3 | Azure Information Protection
description: "Passaggio 3 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in meno di 15 minuti."
author: cabailey
manager: mbaldwin
ms.date: 09/06/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: f5e15870a3a67f67261db9c3d1d735c126f48ee2


---

# Passaggio 3: Installare il client di Azure Information Protection 

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

In questo passaggio verrà installato il client di Azure Information Protection in modo che i criteri appena configurati vengano scaricati in un PC Windows e le etichette vengano visualizzate nelle applicazioni di Office. 

1. In un PC con Office installato ma in cui Word non sia aperto [scaricare il client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) dall'Area download Microsoft. 

2. Eseguire **AzInfoProtection.exe** e seguire le istruzioni per l'installazione del client.

    Per questa esercitazione non è importante selezionare l'opzione relativa all'installazione di criteri demo. Azure infatti scaricherà il criterio appena configurato, che sostituirà i criteri demo. È tuttavia possibile usare l'opzione relativa ai criteri demo se si vogliono solo provare le etichette predefinite senza connettersi ad Azure Information Protection. 

3. Verificare che il client sia stato installato aprendo Word e un nuovo documento vuoto. Non salvare ancora il documento. Se viene richiesto di immettere il nome utente e la password, immettere i dettagli relativi all'account amministratore globale. Quando il documento viene caricato, vengono visualizzati due nuovi elementi:

    - Nella scheda **Home** un nuovo gruppo **Protezione** con il pulsante **Proteggi**.

        Fare clic su **Proteggi** > **Guida e commenti e suggerimenti** e nella finestra di dialogo **Microsoft Azure Information Protection** verificare lo stato del client. Deve essere visualizzato il messaggio **Information Protection policy is installed** (Criteri di Information Protection installati) insieme a una data e a un'ora di connessione recenti. Verificare che il nome utente visualizzato sia corretto per il tenant.

    - Sotto la barra multifunzione viene visualizzata una nuova barra, la barra Information Protection. Questa barra visualizza il titolo **Sensitivity** (Riservatezza) e l'etichetta predefinita configurata in precedenza, **Internal** (Interno). 
    
        ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Client installato](../media/word2013-callouts2.png)

È il momento del passaggio finale, in cui è possibile vedere in azione le funzioni di classificazione, aggiunta di etichette e protezione.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'installazione del client|[Installazione del client di Azure Information Protection](info-protect-client.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 2](infoprotect-tutorial-step2.md)
[Passaggio 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Sep16_HO1-->


