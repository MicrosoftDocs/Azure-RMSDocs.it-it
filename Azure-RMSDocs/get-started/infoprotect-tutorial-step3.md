---
title: Esercitazione introduttiva, passaggio 3 | Azure Information Protection
description: Passaggio 3 dell&quot;esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell&quot;organizzazione. L&quot;esecuzione dell&quot;esercitazione richiede circa 30 minuti.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 496f086d4db43a69ef0acca579b290286a5b9e5b


---

# <a name="step-3-install-the-client-and-application"></a>Passaggio 3: Installare il client e l'applicazione 

>*Si applica a: Azure Information Protection*

In questo passaggio verrà innanzitutto installato il client di Azure Information Protection in modo che i criteri appena configurati vengano scaricati in un PC Windows e le etichette vengano visualizzate nelle applicazioni di Office.

Verrà quindi installata l'applicazione Rights Management sharing, affinché sia possibile condividere in modo sicuro un documento tramite posta elettronica e quindi tenere traccia di come viene usato tale documento. 

Entrambe le installazioni si integrano nelle applicazioni di Office e attualmente è necessario eseguirle separatamente.


## <a name="install-the-azure-information-protection-client"></a>Installare il client di Azure Information Protection

1. In un PC con Office installato ma in cui Word non sia aperto [scaricare il client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) dall'Area download Microsoft. 

2. Eseguire **AzInfoProtection.exe** e seguire le istruzioni per l'installazione del client.

    Per questa esercitazione non è importante selezionare l'opzione relativa all'installazione di criteri demo. Azure infatti scaricherà il criterio appena configurato, che sostituirà i criteri demo. È tuttavia possibile usare l'opzione relativa ai criteri demo se si vogliono solo provare le etichette predefinite senza connettersi ad Azure Information Protection. 

## <a name="install-the-rights-management-sharing-application"></a>Installare l'applicazione Rights Management sharing 

1. Accedere alla pagina [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) nel sito Web Microsoft.

2. Nella sezione **Computer** fare clic sull'icona relativa all'**app RMS per Windows** e salvare il file di installazione **Setup.exe** dell'applicazione Microsoft Rights Management sharing.

3. Nella pagina **Installazione di Microsoft RMS** fare clic su **Avanti**e attendere il completamento dell'installazione. Fare quindi clic su **Riavvia** per riavviare il computer o su **Chiudi** per completare l'installazione.


## <a name="verify-the-installations"></a>Verificare le installazioni

Verificare che le installazioni siano state eseguite correttamente aprendo Word e un nuovo documento vuoto. Non salvare ancora il documento. Se viene richiesto di immettere il nome utente e la password, immettere i dettagli relativi all'account amministratore globale. 

Quando il documento viene caricato, vengono visualizzati tre nuovi elementi:

- Nella scheda **Home** un nuovo gruppo **Protezione** con il pulsante **Proteggi**.

    Fare clic su **Proteggi** > **Guida e commenti e suggerimenti** e nella finestra di dialogo **Microsoft Azure Information Protection** verificare lo stato del client. Deve essere visualizzato il messaggio **Information Protection policy is installed** (Criteri di Information Protection installati) insieme a una data e a un'ora di connessione recenti. Verificare che il nome utente visualizzato sia corretto per il tenant.

- Nella scheda **Home** un nuovo gruppo **RMS** con l'etichetta **Condividi file protetto**.

- La nuova barra di Information Protection sotto la barra multifunzione. Questa barra visualizza il titolo **Sensitivity** (Riservatezza) e l'etichetta predefinita configurata in precedenza, **Interno**. 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Client installato](../media/word2013-callouts2.png)

A questo punto è possibile vedere Azure Information Protection in azione.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'installazione del client di Azure Information Protection|[Installazione del client di Azure Information Protection](../rms-client/info-protect-client.md)|
|Informazioni sull'installazione dell'applicazione Rights Management sharing e istruzioni per gli utenti|[Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md)|
|Informazioni su un'installazione tramite script dell'applicazione Rights Management sharing per Windows e altre informazioni tecniche|[Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 2](infoprotect-tutorial-step2.md)
[Passaggio 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Nov16_HO2-->


