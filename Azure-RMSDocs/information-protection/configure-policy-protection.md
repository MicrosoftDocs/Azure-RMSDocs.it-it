---
title: Come configurare un'etichetta per applicare la protezione di Rights Management | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# Come configurare un'etichetta per applicare la protezione di Rights Management

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili tramite Azure Rights Management, che usa criteri di crittografia, identità e autorizzazione per prevenire la perdita di dati. Questa protezione viene applicata quando si configura un'etichetta per usare un modello di Rights Management. 

Questo modello può essere uno dei modelli predefiniti che vengono creati automaticamente quando si attiva Azure Rights Management oppure un modello personalizzato. I modelli di reparto sono supportati ma applicano la protezione solo quando l'autore del documento o del messaggio di posta elettronica si trova all'interno dell'ambito configurato del modello. Se l'utente è all'esterno dell'ambito, viene visualizzato un messaggio che indica che Azure Information Protection non può applicare l'etichetta.

## Come funziona la protezione

Quando un documento o un messaggio di posta elettronica è protetto da Azure Rights Management, viene crittografato quando i dati sono inattivi e in transito e può essere decrittografato solo dagli utenti autorizzati. Questa crittografia rimane associata al documento o messaggio di posta elettronica, anche se viene rinominato. È anche possibile configurare diritti di utilizzo e restrizioni, come negli esempi seguenti:

- Solo gli utenti all'interno dell'organizzazione possono aprire il documento o messaggio di posta elettronica.

- Solo gli utenti del reparto marketing possono modificare e stampare il documento o messaggio di posta elettronica, mentre tutti gli altri utenti nell'organizzazione possono solo visualizzarlo.

- Gli utenti non possono inoltrare un messaggio di posta elettronica.

- I documenti o messaggi di posta elettronica inviati ai partner commerciali possono essere aperti solo dopo una certa data.

Per altre informazioni sui modelli e sulla configurazione di questi diritti di utilizzo e restrizioni, vedere [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

Per altre informazioni su Azure Rights Management e sul relativo funzionamento, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Per configurare un'etichetta per applicare la protezione di Rights Management, è necessario che sia attivo il servizio Azure Rights Management per l'organizzazione. Se non è ancora stato fatto, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).


## Per configurare un'etichetta per applicare la protezione di Rights Management

1. Accedere al [portale di Azure](https://portal.azure.com).
 
2. Nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

3. Nel pannello **Azure Information Protection** selezionare l'etichetta da configurare per applicare la protezione di Rights Management.

4. Nel pannello **Label** (Etichetta), nella sezione **Set RMS template for protecting documents and emails containing this label** (Imposta il modello RMS per la protezione dei documenti e messaggi di posta elettronica che contengono questa etichetta), configurare quanto segue:

    - Se viene visualizzato **Select RMS template from** (Selezionare modello RMS da), selezionare **Azure RMS**. 
    
        Non selezionare **AD RMS** e le opzioni di configurazione associate senza l'assistenza di Microsoft. Se si vuole testare Azure Information Protection con Active Directory Rights Management Services, inviare un messaggio di posta elettronica all'indirizzo askipteam@microsoft.com. 
    
    - Per **Select RMS template** (Selezionare il modello RMS), fare clic sulla casella a discesa e selezionare il modello da usare per proteggere i documenti e i messaggi di posta elettronica con questa etichetta.

        > [!NOTE] Se si crea un nuovo modello dopo aver aperto il pannello **Label** (Etichetta), chiudere il pannello e tornare al passaggio 3, per fare in modo che Azure recuperi il modello appena creato e ne consenta la selezione.

5. Fare clic su **Save**.

6. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  



<!--HONumber=Jul16_HO5-->


