---
title: Esercitazione introduttiva, passaggio 1 | Azure Information Protection
description: Passaggio 1 dell&quot;esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell&quot;organizzazione. L&quot;esecuzione dell&quot;esercitazione richiede circa 30 minuti.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 1b9a65619e2cbe9def71379dffc6c1df1729cdfa


---

# <a name="step-1-activate-the-rights-management-service"></a>Passaggio 1: Attivare il servizio Rights Management
 
>*Si applica a: Azure Information Protection*

> [!NOTE]
>Se il servizio Azure Rights Management è già stato attivato per il tenant, proseguire con il [passaggio successivo](infoprotect-tutorial-step2.md). 

Quando il servizio Azure Rights Management è attivato, è possibile proteggere i messaggi di posta elettronica e i documenti più sensibili dell'organizzazione e tenere traccia del modo in cui sono usati quando vengono condivisi con altri utenti. È possibile attivare questo servizio in diversi modi, inclusi l'uso di Windows PowerShell e lo spostamento tra i portali di amministrazione.

Ai fini di questa esercitazione, si passerà direttamente alla pagina di attivazione per gli amministratori di Office 365, che è la stessa per il portale di Office 365 classico e l'anteprima dell'interfaccia di amministrazione di Office 365. 

Se si preferisce non passare direttamente a questa pagina ma usare il portale di amministrazione di Office 365, vedere le istruzioni complete riportate nell'articolo [Attivazione di Azure Rights Management](../deploy-use/activate-service.md). Seguire queste istruzioni anche se si ha accesso al portale di Azure ma non al portale di amministrazione di Office 365.

## <a name="to-activate-the-rights-management-service"></a>Per attivare il servizio Rights Management

1. Aprire una nuova finestra del browser e passare direttamente alla [pagina di attivazione di Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per gli amministratori di Office 365.
    
    Se viene chiesto di effettuare l'accesso, usare un account di amministratore globale di Office 365.

2. Nella pagina **Rights Management** fare clic su **attiva**.

3. Quando viene chiesto **se si desidera attivare Rights Management**, fare clic **attiva**.

    Verranno visualizzati il messaggio **Rights Management è attivato** e l'opzione di disattivazione. Potrebbe essere necessario aggiornare manualmente la pagina.

    A questo punto, non scegliere **funzionalità avanzate**. Con questa operazione viene visualizzato il portale di Azure classico in cui è possibile configurare i modelli personalizzati, che non sono necessari per questa esercitazione. È invece possibile chiudere questa pagina.

Quelle sopra indicate sono tutte le operazioni da eseguire per il primo passaggio dell'esercitazione. Per una distribuzione di produzione è probabilmente consigliabile configurare modelli personalizzati in aggiunta ai due modelli predefiniti di Azure Rights Management o in sostituzione di questi. I modelli personalizzati, tuttavia, non sono necessari per questa esercitazione ed è pertanto possibile procedere con il passaggio 2.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'attivazione di Rights Management|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|
|Informazioni sui modelli predefiniti e su come creare nuovi modelli personalizzati|[Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; Introduzione](infoprotect-quick-start-tutorial.md)
[Passaggio 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


