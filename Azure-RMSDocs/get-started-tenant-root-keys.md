---
title: Introduzione all'uso e alla gestione della chiave radice del tenant
description: Informazioni sui passaggi successivi dopo la pianificazione della gestione delle chiavi radice del tenant, inclusa la chiave predefinita generata da Microsoft e BYOK Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9756710e29c82ef953633697cb989942d1844496
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382242"
---
# <a name="getting-started-with-tenant-root-keys"></a>Introduzione alle chiavi radice del tenant

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Dopo aver [pianificato, creato e configurato la chiave del tenant](plan-implement-tenant-key.md) in base alle esigenze, continuare con i passaggi seguenti:

- [Iniziare a usare la chiave del tenant](#start-using-your-tenant-key)
- [Considerare la registrazione dell'utilizzo](#consider-usage-logging)

Per altre informazioni sulle operazioni del ciclo di vita supportate per la chiave del tenant, vedere [operazioni per la chiave del tenant Azure Information Protection](./operations-tenant-key.md).

Se l'organizzazione richiede la protezione locale per contenuti estremamente sensibili, configurare la [protezione DKE](plan-implement-tenant-key.md#double-key-encryption-dke) (solo per client con etichetta unificata).

Se è necessaria la protezione locale e si usa il client classico, configurare invece la [protezione HYOK](configure-adrms-restrictions.md) .
 

## <a name="start-using-your-tenant-key"></a>Iniziare a usare la chiave del tenant

Attivare il servizio Rights Management se non è ancora attivato, per consentire all'organizzazione di iniziare a usare Azure Information Protection. Gli utenti iniziano immediatamente a usare la chiave del tenant.

Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](./activate-service.md).

> [!NOTE]
> Se si è deciso di gestire la propria chiave del tenant dopo l'attivazione del servizio Rights Management, gli utenti passano gradualmente dalla chiave precedente alla nuova chiave nel corso di alcune settimane.
>
>Durante questa transizione, i documenti e i file protetti con la chiave del tenant precedente rimangono accessibili agli utenti autorizzati.

## <a name="consider-usage-logging"></a>Considerare la registrazione dell'utilizzo

La registrazione dell'utilizzo registra ogni transazione eseguita dal servizio Rights Management di Azure.

A seconda del metodo di gestione delle chiavi, le informazioni di registrazione possono includere dettagli sulla chiave del tenant. Nell'immagine seguente viene illustrato un esempio di un file di log visualizzato in Excel, in cui i tipi di richiesta **i** e **KeyVaultSignRequest** indicano che è in uso la chiave del tenant.
    
![file di log visualizzato in Excel in cui è attualmente usata la chiave del tenant](./media/RMS_Logging.png)
    
Per ulteriori informazioni sulla registrazione dell'utilizzo, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).
