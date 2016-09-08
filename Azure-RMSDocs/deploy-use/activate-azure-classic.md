---
title: Come attivare Azure Rights Management dal portale di Azure classico | Azure RMS
description: Usare queste istruzioni se si ha accesso al portale di Azure. Ad esempio, se si ha una sottoscrizione per Enterprise Mobility Suite o la sottoscrizione di Azure Rights Management Premium.
author: cabailey
manager: mbaldwin
ms.date: 06/27/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 573aa437d8449212bd2f22b532342e4c7e3a1be6


---

# Come attivare Azure Rights Management dal portale di Azure classico

>*Si applica a: Azure Rights Management*


Usare queste istruzioni se si ha accesso al portale di Azure. Ad esempio, se si ha una sottoscrizione per Enterprise Mobility Suite o la sottoscrizione di Azure Rights Management Premium.

> [!TIP]
> Guardare un video di due minuti: [Come attivare Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Dopo aver creato un account Azure, [accedere al portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081). Usare un account di amministratore globale, ad esempio l'account usato per ottenere la sottoscrizione che include Azure Rights Management.

2.  Nel riquadro sinistro fare clic su **ACTIVE DIRECTORY**.

3.  Nella pagina **active directory** fare clic su **RIGHTS MANAGEMENT**.

4.  Selezionare la directory da gestire per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], fare clic su **ATTIVA** e quindi confermare l'azione.

    > [!NOTE]
    >Se viene visualizzato un errore di attivazione, è possibile che il piano del servizio o la versione del prodotto non includano [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].
    >
    >Usare le informazioni disponibili nell'articolo relativo alle [sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md) per confermare il supporto per RMS. Per avere assistenza relativamente a tale problema, inviare un messaggio di posta elettronica ad [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


Come **STATO RIGHTS MANAGEMENT** ora verrà visualizzato **Attivo** e l'opzione **ATTIVA** verrà sostituita da **DISATTIVA**.

## Valori di stato e descrizioni di Rights Management nel portale di Azure classico
Oltre allo stato **Attivo** , che indica che il servizio Rights Management è abilitato e pronto all'uso, è possibile che siano visualizzati anche gli stati **Inattivo**, **Non disponibile**o **Non autorizzato**.

|Valore dello stato|Descrizione|
|----------------|---------------|
|**Attivo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è abilitato e pronto all'uso.|
|**Inattivo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è disabilitato e deve essere attivato affinché l'organizzazione possa proteggere i file.|
|**Non disponibile**|Il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è inattivo. Riprovare.|
|**Non autorizzato**|Non si dispone delle autorizzazioni necessarie a visualizzare lo stato del servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Ad esempio, l'account è bloccato oppure l'utente non è l'amministratore globale del tenant selezionato.|

## Passaggi successivi
Tornare ad [Attivazione di Azure Rights Management](activate-service.md).


<!--HONumber=Aug16_HO4-->


