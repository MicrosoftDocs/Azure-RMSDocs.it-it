---
title: Come configurare un'etichetta per applicare la protezione di Rights Management | Azure Information Protection
description: "È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili tramite il servizio Rights Management, che usa criteri di crittografia, identità e autorizzazione per prevenire la perdita di dati. Questa protezione viene applicata quando si configura un'etichetta per usare un modello di Rights Management."
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 830e982fc1f0443545942c1deb1a2fc93431be17


---

# Come configurare un'etichetta per applicare la protezione di Rights Management

>*Si applica a: Azure Information Protection*

È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili tramite il servizio Rights Management, che usa criteri di crittografia, identità e autorizzazione per prevenire la perdita di dati. Questa protezione viene applicata quando si configura un'etichetta per usare un modello di Rights Management. 

Questo modello può essere uno dei modelli predefiniti che vengono creati automaticamente quando si attiva Azure Rights Management oppure un modello personalizzato. I modelli di reparto di Azure Rights Management sono supportati ma applicano la protezione solo quando l'autore del documento o del messaggio di posta elettronica si trova all'interno dell'ambito configurato del modello. Se l'utente è all'esterno dell'ambito, viene visualizzato un messaggio che indica che Azure Information Protection non può applicare l'etichetta.

## Come funziona la protezione

Quando un documento o un messaggio di posta elettronica è protetto da Rights Management, viene crittografato quando i dati sono inattivi e in transito e può essere decrittografato solo dagli utenti autorizzati. Questa crittografia rimane associata al documento o messaggio di posta elettronica, anche se viene rinominato. È anche possibile configurare diritti di utilizzo e restrizioni, come negli esempi seguenti:

- Solo gli utenti all'interno dell'organizzazione possono aprire il documento o il messaggio di posta elettronica riservato dell'azienda.

- Solo gli utenti del reparto marketing possono modificare e stampare il documento o messaggio di posta elettronica relativo all'annuncio di promozione, mentre tutti gli altri utenti nell'organizzazione possono solo visualizzarlo.

- Gli utenti non possono inoltrare un messaggio di posta elettronica che contiene informazioni su una riorganizzazione interna.

- Il listino prezzi aggiornato inviato ai partner commerciali non può essere aperto dopo una certa data.

Per altre informazioni sui modelli di Azure Rights Management e sulla configurazione di questi diritti di utilizzo e restrizioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

Per altre informazioni su Azure Rights Management e sul relativo funzionamento, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Per configurare un'etichetta per applicare la protezione di Azure Rights Management, è necessario che sia attivo il servizio Azure Rights Management per l'organizzazione. Se non è ancora stato fatto, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).


## Per configurare un'etichetta per applicare la protezione di Rights Management

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale, quindi passare al pannello **Azure Information Protection**. 

    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** selezionare l'etichetta da configurare per applicare la protezione di Rights Management.

3. Nel pannello **Etichetta**, nella sezione **Configurare il modello RMS per la protezione di documenti e messaggi di posta elettronica contenenti questa etichetta** in **Selezionare il modello RMS da** selezionare **Azure RMS** o **AD RMS (ANTEPRIMA)**.
    
    Nella maggior parte dei casi, selezionare **Azure RMS**. Non selezionare AD RMS a meno che non siano stati letti e compresi i prerequisiti e le restrizioni relativi a questa configurazione, che viene talvolta definita "*hold your own key*" (HYOK). Per altre informazioni, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md).
    
4. Se si seleziona Azure RMS: per **Selezionare il modello RMS** fare clic sulla casella di riepilogo a discesa e selezionare il [modello](../deploy-use/configure-custom-templates.md) o l'opzione Rights Management che si vuole usare per proteggere i documenti e i messaggi di posta elettronica con questa etichetta.
    
    Altre informazioni sulle opzioni:
    
    - È stato creato un nuovo modello dopo l'apertura del pannello **Etichetta**? Chiudere il pannello e tornare al passaggio 2, per fare in modo che Azure recuperi il modello appena creato e ne consenta la selezione.
    
    - Se si seleziona un **modello di reparto** oppure se sono stati configurati [controlli di selezione](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
        - Gli utenti che non rientrano nell'ambito del modello configurato o che sono esclusi dall'applicazione della protezione di Azure Rights Management visualizzeranno comunque l'etichetta ma non potranno applicarla. Se si seleziona l'etichetta, viene visualizzato un messaggio che indica che **Azure Information Protection non può applicare l'etichetta. Se il problema persiste, contattare l'amministratore.**
        
    - Se si seleziona **Rimuovi protezione**:
        
        - Gli utenti devono avere le autorizzazioni per rimuovere la protezione di Rights Management per applicare un'etichetta con questa opzione. Questa opzione richiede che si abbiano i [diritti di utilizzo](../deploy-use/configure-usage-rights.md) **Esporta** (per i documenti di Office) o **Controllo completo** o che si sia il proprietario di Rights Management (concede automaticamente il diritto di utilizzo Controllo completo) o un [utente con privilegi avanzati per Azure Rights Management](../deploy-use/configure-super-users.md). I modelli di gestione dei diritti predefiniti non includono i diritti di utilizzo che consentono agli utenti di rimuovere la protezione. 

            Se gli utenti non hanno le autorizzazioni per rimuovere la protezione di Rights Management e selezionano questa etichetta con l'opzione **Rimuovi protezione**, viene visualizzato un messaggio simile al seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore.**

5. Se si seleziona AD RMS: fornire il GUID del modello e l'URL di gestione licenze del cluster AD RMS. [Altre informazioni](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

6. Fare clic su **Save**.

7. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  



<!--HONumber=Oct16_HO1-->

