---
title: Esercitazione per l'avvio rapido di Azure RMS - Passaggio 1 | Azure RMS
description: "Il primo passaggio di questa esercitazione consente di provare rapidamente Microsoft Azure Rights Management per l'organizzazione. L'esercitazione è articolata in 5 passaggi, eseguibili in meno di 15 minuti."
keywords: 
author: Cabailey
manager: mbaldwin
ms.date: 06/29/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fab51fefed8d3a347a52ab7c118bb40b3cc23b37
ms.openlocfilehash: 80f2742bbaab9d3252cec6f6c709012ca81218d5


---



# Passaggio 1 dell'esercitazione per l'avvio rapido di Azure RMS: Attivare il servizio Rights Management

*Si applica a: Azure Rights Management, Office 365*


Passare a: 
> [!div class="op_single_selector"]
- [Introduzione](quick-start-tutorial.md)
- [Passaggio 1: Attivare Azure RMS](tutorial-step1.md)
- [Passaggio 2: Installare l'app RMS sharing](tutorial-step2.md)
- [Passaggio 3: Inviare il documento riservato tramite posta elettronica](tutorial-step3.md)
- [Passaggio 4: Leggere il documento](tutorial-step4.md)
- [Passaggio 5: Tenere traccia del documento](tutorial-step5.md)


![Esercitazione per l'avvio rapido di Azure RMS - Passaggio 1](../media/AzRMS_QuickStartSteps1.PNG)

Anche se si dispone di una sottoscrizione che supporta Azure Rights Management, il servizio è disabilitato per impostazione predefinita. Per attivarlo, usare l'interfaccia di amministrazione di Office 365 o il portale di Azure classico:

-   Se è disponibile una sottoscrizione di Office 365 che include Azure Rights Management o una sottoscrizione di Office 365 che esclude Azure Rights Management, ma è disponibile una sottoscrizione di Azure RMS Premium: **usare l'interfaccia di amministrazione di Office 365**.

-   Se non si ha una sottoscrizione di Office 365: **usare il portale di Azure classico**.

![Schermate del passaggio 1 dell'esercitazione](../media/AzRMS_Tutorial_1_Screenshots.png)

### Per attivare Rights Management dall'interfaccia di amministrazione classica di Office 365

> [!NOTE]
> Se si usa l'**anteprima dell'interfaccia di amministrazione di Office 365** anziché l'interfaccia di amministrazione classica di Office 365, è possibile usare le istruzioni da [Come attivare Azure Rights Management dall'anteprima dell'interfaccia di amministrazione di Office 365](../deploy-use/activate-office365-preview.md), o passare alla versione classica per usare queste istruzioni. Per passare alla versione classica, fare clic su **Torna all'interfaccia di amministrazione precedente** sulla **Home page**, dopo aver effettuato l'accesso.

1.  Passare al [portale di Office 365](https://portal.office.com/) e accedere con l'account di amministratore globale di Office 365.

2.  Se l'interfaccia di amministrazione di Office 365 non viene visualizzata automaticamente, selezionare l'icona di avvio delle app in alto a sinistra e scegliere **Amministratore**. Il riquadro **Amministratore** viene visualizzato solo dagli amministratori di Office 365.

    > [!TIP]
    > Per la guida all'interfaccia di amministrazione, vedere [Informazioni sull'interfaccia di amministrazione di Office 365 - Guida per gli amministratori](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  Nel riquadro sinistro fare clic su **IMPOSTAZIONI SERVIZIO**.

4.  Fare clic su **Rights Management**.

5.  Nella pagina **RIGHTS MANAGEMENT** fare clic su **Gestione**.

6.  Nella pagina **Rights Management** fare clic su **attiva**.

7.  Quando viene chiesto **se si desidera attivare Rights Management**, fare clic **attiva**.

Viene visualizzato il messaggio di avvenuta attivazione di Rights management e l'opzione di disattivazione (potrebbe essere necessario aggiornare manualmente la pagina) **** .

A questo punto, non scegliere **funzionalità avanzate**. Con questa operazione viene infatti visualizzato il portale di Azure classico in cui è possibile configurare i modelli, che non sono necessari per questa esercitazione. Chiudere invece l’interfaccia di amministrazione di Office 365.

### Per attivare Rights Management dal portale di Azure classico

1.  Passare al [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081) e accedere con l'account di amministratore globale di Azure Active Directory.

2.  Nel riquadro sinistro fare clic su **ACTIVE DIRECTORY**.

3.  Nella pagina **active directory** fare clic su **RIGHTS MANAGEMENT**.

4.  Selezionare la directory da gestire per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], fare clic su **ATTIVA** e quindi confermare l'azione.

Come **STATO RIGHTS MANAGEMENT** ora verrà visualizzato **Attivo** e l'opzione **ATTIVA** verrà sostituita da **DISATTIVA**.

Sebbene nel portale sia possibile configurare anche altre opzioni relative a Rights Management, queste non sono necessarie ai fini dell'esercitazione ed è pertanto possibile chiudere il portale di Azure classico.

Quelle sopra indicate sono tutte le operazioni da eseguire per il primo passaggio. Il servizio viene attivato in modo che a questo punto tutti gli utenti dell'organizzazione possano iniziare a proteggere i documenti riservati e importanti. In un ambiente di produzione è possibile limitare inizialmente gli utenti che possono effettuare questa operazione, in modo da eseguire un'implementazione graduale. Questo tuttavia non è necessario ai fini dell'esercitazione.

Anche se la procedura corrispondente non è inclusa in questa esercitazione, è probabile che per una distribuzione di produzione si desideri configurare modelli personalizzati. I modelli consentono agli utenti di applicare rapidamente le impostazioni corrette quando ne hanno bisogno per proteggere i file. Quando si attiva Rights Management, si ottengono automaticamente 2 modelli predefiniti ed è probabile che, in un ambiente di produzione, si desideri integrare tali modelli con modelli personalizzati. I modelli, tuttavia, non sono necessari per questa esercitazione ed è pertanto possibile procedere con il passaggio successivo.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'attivazione di Rights Management e sul controllo di chi può proteggere file e messaggi di posta elettronica quando il servizio è attivato|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|
|Informazioni sui modelli predefiniti e su come creare nuovi modelli personalizzati|[Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[«Introduzione](quick-start-tutorial.md)
[Passaggio 2»](tutorial-step2.md)


<!--HONumber=Jul16_HO3-->


