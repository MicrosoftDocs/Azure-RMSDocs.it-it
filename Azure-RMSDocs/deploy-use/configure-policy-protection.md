---
title: Configurare un&quot;etichetta di Azure Information Protection per la protezione
description: "È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili configurando un&quot;etichetta per l&quot;uso della protezione di Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 5bc117cbff3226a2ee0ff375f0aa02fc3232a183
ms.openlocfilehash: ed6bd63a945b73b792bcafcdc0d07e08e83fc344
ms.lasthandoff: 02/27/2017


---

# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Come configurare un'etichetta per la protezione di Rights Management

>*Si applica a: Azure Information Protection*

È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili tramite il servizio Rights Management, che usa criteri di crittografia, identità e autorizzazione per prevenire la perdita di dati. Questa protezione viene applicata quando si configura un'etichetta per l'uso di un modello di Rights Management per documenti e messaggi di posta elettronica o l'opzione **Non inoltrare** per i messaggi di posta elettronica di Outlook. 

Il modello può essere uno di quelli predefiniti che vengono creati automaticamente quando si attiva Azure Rights Management o un modello personalizzato. I modelli di reparto di Azure Rights Management sono supportati ma applicano la protezione solo quando l'autore del documento o del messaggio di posta elettronica si trova all'interno dell'ambito configurato del modello. Se l'utente è all'esterno dell'ambito, viene visualizzato un messaggio che indica che Azure Information Protection non può applicare l'etichetta.

## <a name="how-the-protection-works"></a>Come funziona la protezione

Quando un documento o un messaggio di posta elettronica è protetto da Rights Management, viene crittografato quando i dati sono inattivi e in transito e può essere decrittografato solo dagli utenti autorizzati. Questa crittografia rimane associata al documento o messaggio di posta elettronica, anche se viene rinominato. È anche possibile configurare diritti di utilizzo e restrizioni, come negli esempi seguenti:

- Solo gli utenti all'interno dell'organizzazione possono aprire il documento o il messaggio di posta elettronica riservato dell'azienda.

- Solo gli utenti del reparto marketing possono modificare e stampare il documento o messaggio di posta elettronica relativo all'annuncio di promozione, mentre tutti gli altri utenti nell'organizzazione possono solo visualizzarlo.

- Gli utenti non possono inoltrare un messaggio di posta elettronica che contiene informazioni su una riorganizzazione interna.

- Il listino prezzi aggiornato inviato ai partner commerciali non può essere aperto dopo una certa data.

Per altre informazioni sui modelli di Azure Rights Management e sulla configurazione di questi diritti di utilizzo e restrizioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

Per altre informazioni su Azure Rights Management e sul relativo funzionamento, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Per configurare un'etichetta per applicare la protezione di Azure Rights Management, è necessario che sia attivo il servizio Azure Rights Management per l'organizzazione. Se non è ancora stato fatto, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

Non è necessario configurare Exchange per Information Rights Management (IRM) affinché gli utenti possano applicare etichette in Outlook per proteggere le loro email. Tuttavia, fino a quando Exchange non sarà configurato per IRM, non si potrà usufruire della funzionalità completa della protezione di Rights Management di Azure con Exchange. Ad esempio, gli utenti non potranno visualizzare messaggi di posta elettronica protetti nei telefoni cellulari o con Outlook Web Access, i messaggi di posta elettronica protetti non potranno essere indicizzati per la ricerca e non sarà possibile configurare Exchange Online DLP per la protezione di Rights Management. Per configurare Exchange in modo da supportare questi scenari aggiuntivi, vedere le risorse seguenti:

- Per Exchange Online: vedere le istruzioni per [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Per Exchange locale, è necessario distribuire il [connettore RMS e configurare i server Exchange](../deploy-use/deploy-rms-connector.md). 


## <a name="to-configure-a-label-for-rights-management-protection"></a>Per configurare un'etichetta per la protezione di Rights Management

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale, quindi passare al pannello **Azure Information Protection**. 

    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se l'etichetta da configurare verrà applicata a tutti gli utenti, selezionare **Globale** nel pannello **Azure Information Protection**. Se l'etichetta da configurare si trova in un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata solo agli utenti selezionati, selezionare invece tale criterio con ambito.

3. Nel pannello **Criteri** selezionare l'etichetta da configurare. Verrà aperto il pannello **Etichetta**. 

4. Nel pannello **Etichetta** individuare la sezione **Set permissions for documents and emails containing this label** (Impostare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta) e selezionare una delle opzioni seguenti.
    
    - **Non configurata**: selezionare questa opzione se l'etichetta è attualmente configurata in modo da applicare la protezione e non si vuole più che l'etichetta selezionata applichi la protezione. Procedere quindi con il passaggio 10.
    
    - **Proteggi**: selezionare questa opzione per applicare la protezione e quindi procedere con il passaggio 5.
    
    - **Rimuovi la protezione**: selezionare questa opzione per rimuovere la protezione se questa è configurata per un documento o un messaggio di posta elettronica. Procedere quindi con il passaggio 10.
        
        Si noti che, per applicare un'etichetta con questa opzione, gli utenti devono avere le autorizzazioni per rimuovere la protezione di Rights Management. Per usare questa opzione, gli utenti devono avere i [diritti di utilizzo](../deploy-use/configure-usage-rights.md) **Esporta** o **Controllo completo**, essere proprietari di Rights Management (che implica automaticamente il diritto di utilizzo Controllo completo) oppure essere [utenti con privilegi avanzati per Azure Rights Management](../deploy-use/configure-super-users.md). I modelli predefiniti di Azure Rights Management non includono i diritti di utilizzo che consentono agli utenti di rimuovere la protezione. 
        
        Se gli utenti non hanno le autorizzazioni per rimuovere la protezione di Rights Management e selezionano un'etichetta configurata con l'opzione **Rimuovi protezione**, viene visualizzato il messaggio seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore.**

5. Se si è selezionata l'opzione **Proteggi**, selezionare ora **Protezione** per aprire il pannello **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-bar.png)

6. Nel pannello **Protezione** selezionare **Azure RMS** o **HYOK (AD RMS)**. 
    
    Nella maggior parte dei casi sarà necessario selezionare **Azure RMS** per le impostazioni delle autorizzazioni. Non selezionare **HYOK (AD RMS)** a meno che non siano stati letti e compresi i prerequisiti e le restrizioni relativi a questa configurazione *HYOK* (Hold Your Own Key). Per altre informazioni, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md). Per continuare la configurazione per HYOK (AD RMS), procedere con il passaggio 9.
    
7. Selezionare **Non inoltrare** se si vuole impostare questa opzione di Outlook per i messaggi di posta elettronica oppure **Seleziona modello**. 
    
8. Se si seleziona **Seleziona modello** per **Azure RMS**, fare clic sulla casella di riepilogo a discesa e selezionare il [modello](../deploy-use/configure-custom-templates.md) da usare per proteggere i documenti e i messaggi di posta elettronica con questa etichetta.
    
    Se si seleziona un **modello di reparto** oppure se sono stati configurati [controlli di selezione](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
    - Gli utenti che non rientrano nell'ambito del modello configurato o che sono esclusi dall'applicazione della protezione di Azure Rights Management visualizzeranno comunque l'etichetta ma non potranno applicarla. Se si seleziona l'etichetta, viene visualizzato un messaggio che indica che **Azure Information Protection non può applicare l'etichetta. Se il problema persiste, contattare l'amministratore.**
    
        Si noti che vengono visualizzati sempre tutti i modelli, anche se si sta configurando un criterio con ambito. Si supponga ad esempio di configurare un criterio con ambito per il gruppo Marketing. I modelli di Azure RMS che è possibile selezionare non saranno limitati ai modelli che fanno parte dell'ambito del gruppo Marketing ed è possibile selezionare un modello di reparto che non può essere usato dagli utenti selezionati. Per semplificare la configurazione e per ridurre al minimo la risoluzione dei problemi, provare a ridenominare il modello di reparto in modo da corrispondere all'etichetta nel criterio con ambito. 
            
9. Se si seleziona **Seleziona modello** per **HYOK (AD RMS)**: fornire il GUID del modello e l'URL di gestione licenze del cluster AD RMS. [Altre informazioni](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

10. Fare clic su **OK** per chiudere il pannello **Protezione** e visualizzare la scelta di **Non inoltrare** o il modello selezionato per l'opzione **Protezione** nel pannello **Etichetta**.

10. Nel pannello **Etichetta** fare clic su **Salva**.

11. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
