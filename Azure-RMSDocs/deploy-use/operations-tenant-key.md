---
# required metadata

title: Operazioni relative alla chiave del tenant di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Operazioni relative alla chiave del tenant di Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

A seconda della topologia di chiave del tenant (gestita da Microsoft o dal cliente), i livelli di controllo e di responsabilità per la chiave del tenant di Rights Management di Microsoft Azure (Azure RMS) dopo l'implementazione sono diversi.

Uno scenario in cui l'utente gestisce la propria chiave è denominato scenario BYOK (Bring Your Own Key). Per altre informazioni su questo scenario e sulla scelta tra le due topologie di chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

Nella tabella seguente vengono indicate le operazioni che è possibile eseguire a seconda della topologia di chiave del tenant di Azure RMS scelta.

|Operazione del ciclo di vita|Gestione di Microsoft (impostazione predefinita)|Gestione del cliente (scenario BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocare la chiave del tenant|No (automatica)|No (automatica)|
|Ridistribuire la chiave del tenant|Sì|Sì|
|Eseguire il backup e il ripristino della chiave del tenant|No|Sì|
|Esportare la chiave del tenant|Sì|No|
|Rispondere a una violazione di sicurezza|Sì|Sì|

Dopo aver identificato la topologia implementata, selezionare una delle sezioni seguenti per ottenere altre informazioni su queste operazioni per la chiave del tenant di Azure RMS:


- [Chiave del tenant gestita da Microsoft](operations-microsoft-managed-tenant-key.md)
- [Chiave del tenant gestita dal cliente](operations-customer-managed-tenant-key.md)






<!--HONumber=Apr16_HO4-->


