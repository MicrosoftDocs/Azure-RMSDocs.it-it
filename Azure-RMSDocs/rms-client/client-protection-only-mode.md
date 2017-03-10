---
title: "Modalità di sola protezione per Azure Information Protection"
description: "Informazioni per gli utenti che eseguono il client Azure Information Protection in modalità di sola protezione."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6d7aa4eb4a98db298f6a86b650b8c91a79bdc9b3
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="protection-only-mode-for-the-azure-information-protection-client"></a>Modalità di sola protezione per il client Azure Information Protection

Quando si esegue il client Azure Information Protection senza criteri, viene visualizzato in modalità di **sola protezione**. Ad esempio, quando si usa Esplora file, fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**:

![Modalità di sola protezione](../media/protection-only-mode.png)

 Questa modalità viene eseguita negli scenari seguenti:

- L'organizzazione non ha una sottoscrizione per Azure Information Protection (per la classificazione e la protezione dei dati), ma ha una sottoscrizione per il servizio Azure Rights Management (per la protezione dei dati con Office 365). 
    - Si tratta di uno scenario supportato ed è possibile usare il client Azure Information Protection per proteggere i file e visualizzare i file protetti.

- L'organizzazione ha una sottoscrizione per Azure Information Protection, ma non è possibile scaricare i relativi criteri. 
    - Ciò può accadere a causa di un errore di configurazione o di accesso. Contattare l'help desk o l'amministratore. Nel frattempo potrebbe comunque essere possibile usare il client Azure Information Protection per proteggere i file e visualizzare i file protetti.

## <a name="limitations-for-protection-only-mode"></a>Limitazioni per la modalità di sola protezione

- Nelle app di Office la barra di Azure Information Protection non viene visualizzata. Quando si fa clic su **Proteggi** > **Mostra barra**, questa opzione di menu non è disponibile.

- Quando si usa la finestra di dialogo **Classifica e proteggi - Azure Information Protection** con Esplora file, non vengono visualizzate le etichette per la classificazione. Al contrario, come illustrato nell'immagine precedente, viene visualizzata un'opzione per selezionare i modelli di Rights Management (RMS). 

## <a name="supported-tasks-for-protection-only-mode"></a>Attività supportate per la modalità di sola protezione

- Proteggere documenti e messaggi di posta elettronica (e rimuovere la protezione) dalle app di Office usando la funzionalità Information Rights Management (IRM) di Office. Ad esempio: fare clic su **File** > **Info** > **Proteggi documento** > **Limita accesso**. Per altre informazioni, vedere [Uso della protezione delle informazioni con Office 365 oppure Office 2016 o Office 2013](../deploy-use/help-users.md).

- Proteggere i file (e rimuovere la protezione) usando Esplora file di Windows: fare clic con il pulsante destro del mouse su uno o più file o su una cartella > **Classifica e proteggi**. Per applicare la protezione configurata dall'amministratore, nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Seleziona modello** e scegliere uno dei modelli disponibili.

- Visualizzare i file protetti usando il visualizzatore Azure Information Protection.

- Accedere al sito di rilevamento dei documenti dalle app di Office. È tuttavia necessario avere una sottoscrizione valida per tenere traccia dei documenti e revocarli dal sito.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
