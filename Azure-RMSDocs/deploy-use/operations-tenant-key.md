---
title: Operazioni relative alla chiave del tenant di Azure Information Protection
description: "Identificare i diversi livelli di controllo e responsabilità per la chiave del tenant di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/19/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 52e9b4694eaafe5dbba1af04fb53dd6b1b627d23
ms.sourcegitcommit: 64ba794e7844a74b1e25db0d44b90060e3ae1468
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2017
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Operazioni relative alla chiave del tenant di Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

A seconda della topologia di chiave del tenant (gestita da Microsoft o dal cliente), i livelli di controllo e di responsabilità per la chiave del tenant di Azure Information Protection dopo l'implementazione sono diversi.

Uno scenario in cui l'utente gestisce la propria chiave del tenant in Insieme di credenziali delle chiavi di Azure è denominato scenario BYOK (Bring Your Own Key). Per altre informazioni su questo scenario e su come scegliere tra le due topologie di chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

Nella tabella seguente vengono indicate le operazioni che è possibile eseguire a seconda della topologia di chiave del tenant di Azure Information Protection scelta.

|Operazione del ciclo di vita|Gestione di Microsoft (impostazione predefinita)|Gestione del cliente (scenario BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocare la chiave del tenant|No (automatica)|Sì|
|Reimpostare la chiave del tenant|sì|sì|
|Eseguire il backup e il ripristino della chiave del tenant|No|sì|
|Esportare la chiave del tenant|sì|No|
|Rispondere a una violazione di sicurezza|sì|sì|

Dopo aver identificato la topologia implementata, selezionare una delle sezioni seguenti per ottenere altre informazioni su queste operazioni per la chiave del tenant di Azure Information Protection:

- [Chiave del tenant gestita da Microsoft](operations-microsoft-managed-tenant-key.md)
- [Chiave del tenant gestita dal cliente](operations-customer-managed-tenant-key.md)

Se tuttavia si vuole creare una chiave del tenant di Azure Information Protection importando un dominio di pubblicazione trusted (TPD) da AD RMS, l'operazione di importazione fa parte della [migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
