---
title: Esercitazione per l'avvio rapido - Passaggio 1 - AIP
description: Attivare il servizio di protezione. Passaggio 1 di un'esercitazione introduttiva che consente di provare rapidamente a usare Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 952431771e89e934be4a725ece4f3d9cd47165fe
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2018
---
# <a name="step-1-activate-protection"></a>Passaggio 1: Attivare la protezione
 
>*Si applica a: Azure Information Protection*

> [!NOTE]
>Anche se il servizio Azure Rights Management è già attivato per il tenant, completare questo passaggio per confermare lo stato di attivazione. Le istruzioni includono l'accesso al portale di Azure e la creazione del pannello Azure Information Protection per prepararsi al passaggio 2.

Quando il servizio Azure Rights Management è attivato, è possibile proteggere i messaggi di posta elettronica e i documenti più sensibili dell'organizzazione e controllare come vengono usati quando sono condivisi con altri utenti. 

Esistono diversi modi per attivare la protezione. È possibile usare PowerShell e i portali di amministrazione. In questa esercitazione si usa il portale di Azure, dove vengono anche configurate le etichette per gli utenti. 

## <a name="to-activate-the-azure-rights-management-service"></a>Per attivare il servizio Azure Rights Management

1. Accedere al [portale di Azure](https://portal.azure.com) usando l'account di amministratore globale per il tenant. 
    
    Se non si è l'amministratore globale, è possibile usare uno dei [ruoli amministrativi](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti: **Amministratore di Information Protection** o **Amministratore della sicurezza**.

2. Nel menu hub fare clic su **Crea una risorsa**, quindi nell'elenco **Marketplace** selezionare **Sicurezza e identità**. 
    
3.  Nell'elenco **App in primo piano** del pannello **Sicurezza e identità** selezionare **Azure Information Protection**. Quindi fare clic su **Crea** nel pannello **Azure Information Protection**.
    
    Questa azione consente di creare il pannello **Azure Information Protection** in modo che al successivo accesso al portale sia possibile selezionare il servizio dall'elenco **Tutti i servizi** dell'hub. 
    
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
