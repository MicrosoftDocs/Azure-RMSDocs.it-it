---
title: Come distribuire un'app - AIP
description: Questo articolo descrive il processo di distribuzione di un'applicazione di servizio in un tenant diverso da quello per cui è stata originariamente sviluppata.
keywords: ''
author: kkanakas
ms.author: kartikka
manager: barbkess
ms.date: 02/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 34dc6d6f-cfe4-4848-9b11-8d90c4b38ef7
audience: developer
ms.reviewer: kartikka
ms.suite: ems
ms.openlocfilehash: 5be6785c86cfeb104acc7f12d4cb7b830e9c9d36
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251876"
---
# <a name="deploying-a-service-application-into-a-different-tenant"></a>Distribuzione di un'applicazione di servizio a un tenant diverso

Questo articolo descrive il processo di distribuzione di un'applicazione di servizio. In questo scenario si eseguirà la transizione dell'applicazione dal tenant AD di sviluppo in cui è stata originariamente registrata al tenant AD di produzione di un'altra società.

> [!Note]
> Questo scenario è pertinente solo se l'applicazione di servizio usa l'autenticazione con chiave simmetrica.

## <a name="scenario"></a>Scenario
La società *CoolApp* ha sviluppato un'applicazione di servizio usando Azure Information Protection (AIP), che esegue la crittografia, assegna etichette e protegge i documenti quando gli utenti eseguono l'esportazione da un'applicazione aziendale come Dynamics, SAP o Salesforce. In questo scenario un'azienda di grandi dimensioni, *ABC*, acquista la nuova applicazione di *CoolApp* e pertanto il team di *CoolApp* deve distribuire la soluzione nell'ambiente di *ABC*. 

![Flusso di esempio per la creazione della chiave simmetrica in un altro tenant](../media/develop/service-app-provision.jpg)

## <a name="flow-1-coolapp-provides-a-ui-dialog-to-abc-to-implement-the-deployment"></a>Flusso 1: *CoolApp* fornisce una finestra di dialogo ad *ABC* per implementare la distribuzione

Dopo che *ABC* ha acquistato la soluzione di *CoolApp*, l'amministratore IT di *ABC* deve creare l'entità servizio *CoolApp* e registrare l'applicazione nel tenant Azure AD di *ABC*. 

I passaggi di questa procedura sono illustrati nella sezione **Creare un'entità servizio** di [Sviluppo dell'applicazione](developing-your-application.md).

![Esempio di interfaccia utente che l'amministratore IT può inserire per l'applicazione](../media/develop/how-to-deploy-app-UI.png)

> [!Note]
> Per creare l'entità servizio in un tenant è necessario disporre dei diritti di amministrazione del tenant.

L'amministratore IT di *ABC* avvia quindi l'applicazione di *CoolApp* come servizio nel proprio ambiente e incorpora i dettagli per il funzionamento dell'applicazione di *CoolApp*, ad esempio l'ID dell'applicazione, l'ID del tenant e la chiave simmetrica.

Se è stato deciso di non fornire all'amministratore IT di *ABC* una finestra di dialogo per le informazioni dell'entità servizio, seguire la procedura descritta in **Flusso 2**.

## <a name="flow-2-abc-it-administrator-provides-the-key-to-the-coolapp-team"></a>Flusso 2: l'amministratore IT di *ABC* fornisce la chiave al team di *CoolApp*

Dopo che l'amministratore IT di *ABC* ha creato l'entità servizio, come illustrato in **Figura 1**, *ABC* fornisce le informazioni al team di *CoolApp*. A sua volta, il team di *CoolApp* procede a incorporare le informazioni nell'applicazione di *CoolApp* per consentirne l'uso al tenant di *ABC*.
