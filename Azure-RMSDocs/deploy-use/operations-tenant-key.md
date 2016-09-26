---
title: Operazioni relative alla chiave del tenant di Azure Rights Management | Azure RMS
description: "Identificare i diversi livelli di controllo e responsabilità per la chiave del tenant di Azure Rights Management (Azure RMS)."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: d496a99c4b05e0cf0ba5929f44cdbd1906d31341


---

# Operazioni relative alla chiave del tenant di Azure Rights Management

>*Si applica a: Azure Rights Management, Office 365*

A seconda della topologia di chiave del tenant (gestita da Microsoft o dal cliente), i livelli di controllo e di responsabilità per la chiave del tenant di Rights Management di Microsoft Azure (Azure RMS) dopo l'implementazione sono diversi.

Uno scenario in cui l'utente gestisce la propria chiave del tenant in Insieme di credenziali delle chiavi di Azure è denominato scenario BYOK (Bring Your Own Key). Per altre informazioni su questo scenario e su come scegliere tra le due topologie di chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

Nella tabella seguente vengono indicate le operazioni che è possibile eseguire a seconda della topologia di chiave del tenant di Azure RMS scelta.

|Operazione del ciclo di vita|Gestione di Microsoft (impostazione predefinita)|Gestione del cliente (scenario BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocare la chiave del tenant|No (automatica)|sì|
|Ridistribuire la chiave del tenant|sì|sì|
|Eseguire il backup e il ripristino della chiave del tenant|No|sì|
|Esportare la chiave del tenant|sì|No|
|Rispondere a una violazione di sicurezza|sì|sì|

Dopo aver identificato la topologia implementata, selezionare una delle sezioni seguenti per ottenere altre informazioni su queste operazioni per la chiave del tenant di Azure RMS:


- [Chiave del tenant gestita da Microsoft](operations-microsoft-managed-tenant-key.md)
- [Chiave del tenant gestita dal cliente](operations-customer-managed-tenant-key.md)







<!--HONumber=Aug16_HO4-->

