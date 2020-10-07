---
title: Panoramica - Microsoft Information Protection SDK.
description: Microsoft Information Protection (MIP) riunisce i servizi di classificazione, etichettatura e protezione di Microsoft in una singola esperienza di amministrazione e in un singolo Software Development Kit (SDK).
author: msmbaldwin
ms.service: information-protection
ms.topic: overview
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 32f2895d8b52a5fd63d5c764eebb78736b1917a9
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2020
ms.locfileid: "91588326"
---
# <a name="overview"></a>Panoramica

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) riunisce i servizi di classificazione, etichettatura e protezione di Microsoft:

- L'amministrazione unificata è disponibile per Microsoft 365, Azure Information Protection, Windows Information Protection e altri servizi Microsoft. 
- Il SDK MIP può essere usato da terze parti per integrare le applicazioni, tramite uno schema di etichettatura dei dati e un servizio di protezione standard e coerenti.

* [Che cos'è il Centro conformità e sicurezza di Office 365?](/office365/securitycompliance/)
* [Che cos'è Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
* [Come funziona la protezione in Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK

Il SDK MIP espone i servizi di etichettatura e protezione dal Centro conformità e sicurezza di Office 365 ad applicazioni e servizi di terze parti. Gli sviluppatori possono usare l'SDK per creare il supporto nativo per l'applicazione di etichette e della protezione ai file. Gli sviluppatori possono prendere decisioni programmatiche sulle azioni da eseguire quando vengono rilevate etichette specifiche e sulle informazioni crittografate con MIP. 

Le etichette e la protezione applicate alle informazioni per la gamma di servizi di Microsoft sono **coerenti**. La coerenza consente alle applicazioni e ai servizi che supportano MIP di leggere e scrivere le etichette in un modo comune e prevedibile.

I casi d'uso generali per MIP SDK includono:

* Un'applicazione line-of-business che applica etichette di classificazione ai file durante l'esportazione.
* Un'applicazione di progettazione CAD/CAM che fornisce il supporto nativo per l'etichettatura di Microsoft Information Protection.
* Un CASB (Cloud Access Security Broker) o una soluzione di prevenzione della perdita dei dati che prende decisioni programmatiche per i dati crittografati con Azure Information Protection.

Per un elenco più esaustivo, vedere i [concetti relativi alle API](concept-apis-use-cases.md).

MIP SDK è supportato nelle piattaforme seguenti:

[!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

## <a name="next-steps"></a>Passaggi successivi

A questo punto è possibile iniziare a esplorare l'SDK. In primo luogo è necessario [completare le procedure di installazione e configurazione del SDK MIP](setup-configure-mip.md). Queste procedure garantiscono la configurazione corretta della sottoscrizione di Microsoft 365 e del computer client.