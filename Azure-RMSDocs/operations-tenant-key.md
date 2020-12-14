---
title: Operazioni relative alla chiave del tenant di Azure Information Protection
description: Identificare i diversi livelli di controllo e responsabilità per la chiave del tenant di Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7d6cf57f75cdb3e60371dfae26509bd7f2e847c5
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386475"
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Operazioni relative alla chiave del tenant di Azure Information Protection

>**Si applica a*: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

In base alla topologia di chiave del tenant per Azure Information Protection, esistono diversi livelli di controllo e di responsabilità per la chiave del tenant di Azure Information Protection. Le due topologie di chiave sono **gestita da Microsoft** e **gestita dal cliente**.

Uno scenario in cui l'utente gestisce la propria chiave del tenant in Insieme di credenziali delle chiavi di Azure è denominato scenario BYOK (Bring Your Own Key). Per altre informazioni su questo scenario e su come scegliere tra le due topologie di chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

Nella tabella seguente vengono indicate le operazioni che è possibile eseguire in base alla topologia scelta per la chiave del tenant di Azure Information Protection.

|Operazione del ciclo di vita|Gestione di Microsoft (impostazione predefinita)|Gestione del cliente (scenario BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocare la chiave del tenant|No (automatica)|Sì|
|Reimpostare la chiave del tenant|Sì|Sì|
|Eseguire il backup e il ripristino della chiave del tenant|No|Sì|
|Esportare la chiave del tenant|Sì|No|
|Rispondere a una violazione di sicurezza|Sì|Sì|

Dopo aver identificato la topologia implementata, selezionare uno dei collegamenti seguenti per ottenere altre informazioni su queste operazioni per la chiave del tenant di Azure Information Protection:

- [Chiave del tenant gestita da Microsoft](operations-microsoft-managed-tenant-key.md)
- [Chiave del tenant gestita dal cliente](operations-customer-managed-tenant-key.md)

Se tuttavia si vuole creare una chiave del tenant di Azure Information Protection importando un dominio di pubblicazione trusted (TPD) da AD RMS, l'operazione di importazione fa parte della [migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).  

