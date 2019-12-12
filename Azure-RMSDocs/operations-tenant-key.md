---
title: Operazioni relative alla chiave del tenant di Azure Information Protection
description: Identificare i diversi livelli di controllo e responsabilità per la chiave del tenant di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7de597c2ebe50aa2309e3c6cce1b4b7b8523a994
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2019
ms.locfileid: "74934637"
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Operazioni relative alla chiave del tenant di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

In base alla topologia di chiave del tenant per Azure Information Protection, esistono diversi livelli di controllo e di responsabilità per la chiave del tenant di Azure Information Protection. Le due topologie di chiave sono **gestita da Microsoft** e **gestita dal cliente**.

Uno scenario in cui l'utente gestisce la propria chiave del tenant in Insieme di credenziali delle chiavi di Azure è denominato scenario BYOK (Bring Your Own Key). Per altre informazioni su questo scenario e su come scegliere tra le due topologie di chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

Nella tabella seguente vengono indicate le operazioni che è possibile eseguire in base alla topologia scelta per la chiave del tenant di Azure Information Protection.

|Operazione del ciclo di vita|Gestione di Microsoft (impostazione predefinita)|Gestione del cliente (scenario BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocare la chiave del tenant|No (automatica)|Yes|
|Reimpostare la chiave del tenant|Yes|Yes|
|Eseguire il backup e il ripristino della chiave del tenant|No|Yes|
|Esportare la chiave del tenant|Yes|No|
|Rispondere a una violazione di sicurezza|Yes|Yes|

Dopo aver identificato la topologia implementata, selezionare uno dei collegamenti seguenti per ottenere altre informazioni su queste operazioni per la chiave del tenant di Azure Information Protection:

- [Chiave del tenant gestita da Microsoft](operations-microsoft-managed-tenant-key.md)
- [Chiave del tenant gestita dal cliente](operations-customer-managed-tenant-key.md)

Se tuttavia si vuole creare una chiave del tenant di Azure Information Protection importando un dominio di pubblicazione trusted (TPD) da AD RMS, l'operazione di importazione fa parte della [migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).  

