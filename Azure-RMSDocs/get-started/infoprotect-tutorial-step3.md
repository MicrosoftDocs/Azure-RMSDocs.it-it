---
title: Esercitazione per l'avvio rapido - Passaggio 3 - AIP
description: 'Passaggio 3 di un''esercitazione introduttiva per provare rapidamente a usare Azure Information Protection: installare il client.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
ms.openlocfilehash: ccc52f1fca6e968ac1794d7bad437c271f4bd485
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2017
---
# <a name="step-3-install-the-client"></a>Passaggio 3: Installare il client

>*Si applica a: Azure Information Protection*

In questo passaggio verrà installato il client di Azure Information Protection in modo che i criteri appena configurati vengano scaricati in un PC Windows e le etichette vengano visualizzate nelle applicazioni di Office.


## <a name="install-the-azure-information-protection-client"></a>Installare il client di Azure Information Protection

1. In un PC con Office installato ma in cui Word non sia aperto accedere all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection.exe**. Si tratta della versione con disponibilità generale del client supportata nelle reti di produzione. Tuttavia, se si vuole provare la versione di anteprima corrente che dispone di tutte le funzionalità e correzioni più recenti, scaricare **AzInfoProtection_PREVIEW_1.10.52.0.exe**.
    
2. Eseguire il file eseguibile appena scaricato e seguire le istruzioni per installare il client.
    
    Per questa esercitazione non è importante selezionare l'opzione relativa all'installazione di criteri demo. Azure infatti scaricherà il criterio appena configurato, che sostituirà i criteri demo. È tuttavia possibile usare l'opzione relativa ai criteri demo se si vogliono solo provare le etichette predefinite senza connettersi ad Azure Information Protection. 

## <a name="verify-the-installation"></a>Verificare l'installazione

Verificare che l'installazione sia stata completata correttamente aprendo Word e un nuovo documento vuoto. Non salvare ancora il documento. Se viene richiesto di immettere il nome utente e la password, immettere i dettagli relativi all'account amministratore globale. 

Se si installa il client per la prima volta, verrà visualizzata una pagina **iniziale** con istruzioni di base. Dopo aver letto le informazioni, fare clic su **Chiudi**.

Quando il documento viene caricato, vengono visualizzati due nuovi elementi:

![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Client installato](../media/word2016-calloutsv2.png)

- Un nuovo gruppo **Protection** (Protezione) nella scheda **Home** con un pulsante denominato **Protect** (Proteggi).
    
    Fare clic su **Proteggi** > **Guida e commenti e suggerimenti** e nella finestra di dialogo **Microsoft Azure Information Protection** verificare lo stato del client. Dovrebbe venire visualizzata l'indicazione **Connesso come** seguita dal nome dell'utente. Dovrebbe inoltre venire visualizzata un'indicazione di data e ora per l'ultima connessione e per l'installazione dei criteri di Information Protection. Verificare che il nome utente visualizzato sia corretto per il tenant.

- La nuova barra di Information Protection sotto la barra multifunzione. Visualizza il titolo **Sensibilità** e le etichette illustrate nel portale di Azure. 

A questo punto è possibile vedere Azure Information Protection in azione.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'installazione del client di Azure Information Protection|[Scaricare e installare il client di Azure Information Protection](../rms-client/install-client-app.md)|
|Istruzioni per gli amministratori del client Azure Information Protection|[Guida per l'amministratore del client di Azure Information Protection](../rms-client/client-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 2](infoprotect-tutorial-step2.md)
[Passaggio 4 &#187;](infoprotect-tutorial-step4.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]