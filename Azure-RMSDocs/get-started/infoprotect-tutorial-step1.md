---
title: Esercitazione per l'avvio rapido - Passaggio 1 - AIP
description: 'Passaggio 1 di un''esercitazione introduttiva per provare rapidamente a usare Azure Information Protection: attivare il servizio Azure Rights Management.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 1779eb6f2bcf31ce3515b58b6ed955208fafb237
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2017
---
# <a name="step-1-activate-the-rights-management-service"></a>Passaggio 1: Attivare il servizio Rights Management
 
>*Si applica a: Azure Information Protection*

> [!NOTE]
>Se il servizio Azure Rights Management per il tenant è già stato attivato, andare direttamente al [passaggio successivo](infoprotect-tutorial-step2.md). 
>
>Se non si è sicuri se il servizio è stato attivato, usare le istruzioni incluse in questo passaggio per verificarlo.

Quando il servizio Azure Rights Management è attivato, è possibile proteggere i messaggi di posta elettronica e i documenti più sensibili dell'organizzazione e tenere traccia del modo in cui i documenti protetti vengono usati quando vengono condivisi con altri utenti. È possibile attivare questo servizio in vari modi, inclusi l'uso di Windows PowerShell e i portali di amministrazione.

Per questa esercitazione, si passerà direttamente alla pagina di attivazione del portale per gli amministratori di Office 365. Se invece si preferisce non passare direttamente a questa pagina, ma usare il portale di amministrazione di Office 365, vedere le istruzioni complete riportate nell'articolo [Attivazione di Azure Rights Management](../deploy-use/activate-service.md). Seguire queste istruzioni anche se si ha accesso al portale di Azure ma non al portale di amministrazione di Office 365.

## <a name="to-activate-the-rights-management-service"></a>Per attivare il servizio Rights Management

1. Aprire una nuova finestra del browser e passare direttamente alla [pagina di attivazione di Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per gli amministratori di Office 365.
    
    Se viene chiesto di effettuare l'accesso, usare un account di amministratore globale di Office 365.

2. Nella pagina **Rights Management** fare clic su **attiva**. Se questo pulsante visualizza il testo **deactivate** (disattiva), vuol dire che il servizio è già attivato ed è possibile passare direttamente al [passaggio successivo](infoprotect-tutorial-step2.md). 

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 1: attivare il servizio](../media/info-protect-activate.png)

3. Quando viene visualizzata la richiesta **Do you want to activate Rights Management?** (Attivare Rights Management?), fare clic su **activate** (attiva) per confermare l'attivazione.

    Verranno visualizzati il messaggio **Rights Management è attivato** e l'opzione di disattivazione. Potrebbe essere necessario aggiornare manualmente la pagina.

    A questo punto, non scegliere **funzionalità avanzate**. È invece possibile chiudere questa pagina.

Quelle sopra indicate sono tutte le operazioni da eseguire per il primo passaggio dell'esercitazione. È ora possibile andare al Passaggio 2.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'attivazione di Rights Management|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introduzione](infoprotect-quick-start-tutorial.md)
[Passaggio 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
