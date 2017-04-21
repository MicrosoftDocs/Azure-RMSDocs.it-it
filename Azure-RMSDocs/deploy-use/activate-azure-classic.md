---
title: Attivare Azure RMS con il portale di Azure classico - AIP
description: Istruzioni di attivazione per il servizio Azure Rights Management quando si accede al portale di Azure. Ad esempio, se si ha una sottoscrizione per Enterprise Mobility Suite o la sottoscrizione Premium di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7400cb489d3930ef1436bb3b08def5bf673c2bbf
ms.sourcegitcommit: 7b773ca5bf1abf30e527c34717ecb2dc96f88033
translationtype: HT
---
# <a name="how-to-activate-azure-rights-management-from-the-azure-classic-portal"></a>Come attivare Azure Rights Management dal portale di Azure classico

>*Si applica a: Azure Information Protection*


Usare queste istruzioni se si ha accesso al portale di Azure. Ad esempio, se si ha una sottoscrizione per Enterprise Mobility Suite o la sottoscrizione Premium di Azure Information Protection.

> [!TIP]
> Guardare un video di due minuti: [Come attivare Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Dopo aver creato un account Azure, [accedere al portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081). Usare un account di amministratore globale, ad esempio l'account usato per ottenere la sottoscrizione che include Azure Rights Management.

2.  Nel riquadro sinistro fare clic su **ACTIVE DIRECTORY**.

3.  Nella pagina **active directory** fare clic su **RIGHTS MANAGEMENT**.

4.  Selezionare la directory da gestire per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], fare clic su **ATTIVA** e quindi confermare l'azione.

    > [!NOTE]
    >Se viene visualizzato un errore di attivazione, è possibile che il piano del servizio o la versione del prodotto non includa il servizio Azure Rights Management per Azure Information Protection.
    >
    >Per attivare il servizio Azure Rights Management, è necessario un [piano Azure Information Protection Premium](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) o un [piano di Office 365 che include Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Per avere assistenza relativamente a tale problema, inviare un messaggio di posta elettronica ad [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


Come **STATO RIGHTS MANAGEMENT** ora verrà visualizzato **Attivo** e l'opzione **ATTIVA** verrà sostituita da **DISATTIVA**.

## <a name="rights-management-status-values-and-descriptions-in-the-azure-classic-portal"></a>Valori di stato e descrizioni di Rights Management nel portale di Azure classico
Oltre allo stato **Attivo** , che indica che il servizio Rights Management è abilitato e pronto all'uso, è possibile che siano visualizzati anche gli stati **Inattivo**, **Non disponibile**o **Non autorizzato**.

|Valore dello stato|Descrizione|
|----------------|---------------|
|**Attivo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è abilitato e pronto all'uso.|
|**Inattivo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è disabilitato e deve essere attivato affinché l'organizzazione possa proteggere i file.|
|**Non disponibile**|Il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è inattivo. Riprovare.|
|**Non autorizzato**|Non si dispone delle autorizzazioni necessarie a visualizzare lo stato del servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Ad esempio, l'account è bloccato oppure l'utente non è l'amministratore globale del tenant selezionato.|

## <a name="next-steps"></a>Passaggi successivi
Tornare ad [Attivazione di Azure Rights Management](activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]