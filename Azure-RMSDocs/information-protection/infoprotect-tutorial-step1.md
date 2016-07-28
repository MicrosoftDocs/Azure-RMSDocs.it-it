---
title: Esercitazione introduttiva di Azure Information Protection, passaggio 1 | Azure Rights Management
description: "Passaggio 1 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in circa 10 minuti."
author: cabailey
manager: mbaldwin
ms.date: 07/11/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 78f0f07271414fb646f996e7273343f2abf8852b
ms.openlocfilehash: 633b24d0c23cbbee88a2647aaa9defe376ccb40e


---

# Passaggio 1: Attivare il servizio Rights Management
 
*Si applica a: Azure Information Protection (anteprima)*

> [!NOTE]
>Se si vogliono solo classificare i dati, senza proteggerli con Azure Rights Management, o se Azure Rights Management è già attivato per il tenant, andare direttamente al [passaggio successivo](infoprotect-tutorial-step2.md). 

Quando Azure Rights Management è attivato, è possibile proteggere i documenti e i file più sensibili dopo che sono stati classificati. Per attivare Azure Rights Management, è possibile usare l'interfaccia di amministrazione di Office 365 o il portale di Azure classico:

-   Se è disponibile una sottoscrizione di Office 365 che include Azure Rights Management o una sottoscrizione di Office 365 che esclude Azure Rights Management, ma è disponibile una sottoscrizione di Azure RMS Premium: **usare l'interfaccia di amministrazione di Office 365**.

-   Se non si ha una sottoscrizione di Office 365: **usare il portale di Azure classico**.

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

A questo punto, non scegliere **funzionalità avanzate**. Con questa operazione viene visualizzato il portale di Azure classico in cui è possibile configurare i modelli personalizzati, che non sono necessari per questa esercitazione. Chiudere invece l’interfaccia di amministrazione di Office 365.

### Per attivare Rights Management dal portale di Azure classico

1.  Passare al [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081) e accedere con l'account di amministratore globale di Azure Active Directory.

2.  Nel riquadro sinistro fare clic su **ACTIVE DIRECTORY**.

3.  Nella pagina **active directory** fare clic su **RIGHTS MANAGEMENT**.

4.  Selezionare la directory da gestire per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], fare clic su **ATTIVA** e quindi confermare l'azione.

Come **STATO RIGHTS MANAGEMENT** ora verrà visualizzato **Attivo** e l'opzione **ATTIVA** verrà sostituita da **DISATTIVA**.

Sebbene nel portale sia possibile configurare anche altre opzioni relative a Rights Management, queste non sono necessarie ai fini dell'esercitazione ed è pertanto possibile chiudere il portale di Azure classico.

Quelle sopra indicate sono tutte le operazioni da eseguire per il primo passaggio. Il servizio Azure Rights Management è attivato. Più avanti nell'esercitazione sarà possibile selezionare uno dei modelli predefiniti di Azure Rights Management per proteggere documenti e messaggi di posta elettronica classificati come riservati.

Per una distribuzione di produzione è probabilmente consigliabile configurare modelli personalizzati in aggiunta ai due modelli predefiniti di Azure Rights Management o in sostituzione di questi. I modelli personalizzati, tuttavia, non sono necessari per questa esercitazione ed è pertanto possibile procedere con il passaggio 2.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sull'attivazione di Rights Management|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|
|Informazioni sui modelli predefiniti e su come creare nuovi modelli personalizzati|[Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; Introduzione](infoprotect-quick-start-tutorial.md)
[Passaggio 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Jul16_HO3-->

