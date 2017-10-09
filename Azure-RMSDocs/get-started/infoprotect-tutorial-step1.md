---
title: Esercitazione per l'avvio rapido - Passaggio 1 - AIP
description: Attivare il servizio di protezione. Passaggio 1 di un'esercitazione introduttiva che consente di provare rapidamente a usare Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 91eb9ec61f4fa1ebd7aac3cf0c244878ef450bb9
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2017
---
# <a name="step-1-activate-protection"></a>Passaggio 1: Attivare la protezione
 
>*Si applica a: Azure Information Protection*

> [!NOTE]
>Anche se è già stato attivato il servizio Azure Rights Management per il tenant, completare questo passaggio per confermare lo stato di attivazione. Le istruzioni includono l'accesso al portale di Azure e la creazione del pannello Azure Information Protection, in modo da essere pronti per il passaggio 2. 

Quando il servizio Azure Rights Management è attivato, è possibile proteggere i messaggi di posta elettronica e i documenti più sensibili dell'organizzazione e tenere traccia del modo in cui i documenti protetti vengono usati quando vengono condivisi con altri utenti. È possibile attivare la protezione in modi diversi, usando ad esempio Windows PowerShell e i portali di amministrazione.

Per questa esercitazione si userà il portale di Azure, dove vengono anche configurate le etichette per gli utenti. 

## <a name="to-activate-the-azure-rights-management-service"></a>Per attivare il servizio Azure Rights Management

1. Accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza per il tenant.

2. Nel menu hub fare clic su **Nuovo** e quindi, nell'elenco **Marketplace**, selezionare **Sicurezza e identità**. 
    
3.  Nell'elenco **App in primo piano** del pannello **Sicurezza e identità** selezionare **Azure Information Protection**. Quindi fare clic su **Crea** nel pannello **Azure Information Protection**.
    
    Questa azione consente di creare il pannello **Azure Information Protection** in modo che al successivo accesso al portale sarà possibile selezionare il servizio dall'elenco **Altri servizi** dell'hub. 
    
    > [!TIP] 
    > Selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.

4. Leggere le informazioni disponibili nella pagina **Avvio rapido** che si apre automaticamente quando ci si connette al servizio per la prima volta. È possibile tornare a questa pagina in un secondo momento. Per questa esercitazione, selezionare **Protection activation** (Attivazione protezione). 

5. Ora è possibile vedere se il servizio Azure Rights Management è attivato per il tenant. 
    
    - Se il servizio è attivato, viene visualizzato il messaggio di conferma seguente:
        
        ![Stato di Azure Information Protection per Azure RMS](../media/info-protect-azurerms-activated.png)
        
    - Se il servizio non è attivato, le informazioni sullo stato indicano questa condizione e viene visualizzata l'opzione per l'attivazione:
        
        ![Stato di Azure Information Protection per Azure RMS](../media/info-protect-azurerms-deactivated.png)

6. Se il servizio non è attivato, selezionare **Attiva**. 

    Una volta completata l'attivazione, sulla barra delle informazioni verrà visualizzato il messaggio **Activation finished successfully** (Attivazione completata).

Quelle sopra indicate sono tutte le operazioni da eseguire per il primo passaggio dell'esercitazione. È ora possibile andare al Passaggio 2.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'attivazione di Rights Management|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introduzione](infoprotect-quick-start-tutorial.md)
[Passaggio 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
