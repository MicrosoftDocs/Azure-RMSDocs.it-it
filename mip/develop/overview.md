---
title: Panoramica - Microsoft Information Protection SDK.
description: Microsoft Information Protection (MIP) riunisce i servizi di classificazione, etichettatura e protezione di Microsoft in una singola esperienza di amministrazione e in un singolo Software Development Kit (SDK).
author: msmbaldwin
ms.service: information-protection
ms.topic: overview
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: d8efb7ceef890d0c2a0ea72f64d3047e0cfb25a5
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329608"
---
# <a name="overview"></a>Panoramica

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) è l'unificazione del Microsoft classificazione, assegnazione di etichette e i servizi di protezione:

- L'amministrazione unificata è disponibile per Office 365, Azure Information Protection, Windows Information Protection e ad altri servizi Microsoft. 
- Terze parti è possibile usare il SDK di MIP per integrarsi con applicazioni, usando una data standard, coerenti con l'assegnazione di etichette dello schema e la protezione del servizio.

* [Che cos'è il Centro conformità e sicurezza di Office 365?](https://docs.microsoft.com/office365/securitycompliance/)
* [Che cos'è Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
* [Come funziona la protezione in Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK

Microsoft Information Protection SDK espone i servizi di assegnazione di etichette e protezione da Office 365 Centro sicurezza e conformità, a servizi e applicazioni di terze parti. Gli sviluppatori possono usare l'SDK per creare il supporto nativo per l'applicazione di etichette e della protezione ai file. Gli sviluppatori possono prendere decisioni programmatiche sulle azioni da eseguire quando vengono rilevate etichette specifiche e sulle informazioni crittografate con MIP. 

Le etichette e la protezione applicate alle informazioni per la gamma di servizi di Microsoft sono **coerenti**. La coerenza consente alle applicazioni e ai servizi che supportano MIP di leggere e scrivere le etichette in un modo comune e prevedibile.

I casi d'uso generali per MIP SDK includono:

* Un'applicazione line-of-business che applica etichette di classificazione ai file durante l'esportazione.
* Un'applicazione di progettazione CAD/CAM che fornisce il supporto nativo per l'etichettatura di Microsoft Information Protection.
* Un CASB (Cloud Access Security Broker) o una soluzione di prevenzione della perdita dei dati che prende decisioni programmatiche per i dati crittografati con Azure Information Protection.

Per un elenco più esaustivo, vedere i [concetti relativi alle API](concept-apis-use-cases.md).

MIP SDK è supportato nelle piattaforme seguenti:

[!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

## <a name="next-steps"></a>Passaggi successivi

A questo punto è possibile iniziare a esplorare l'SDK. Innanzitutto, occorre effettuare [completare i passaggi di installazione e configurazione di Microsoft Information Protection SDK](setup-configure-mip.md). Questi passaggi garantirà la sottoscrizione di Office 365 e computer client siano configurate correttamente.

