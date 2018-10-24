---
title: Panoramica - Microsoft Information Protection SDK.
description: Microsoft Information Protection (MIP) riunisce i servizi di classificazione, etichettatura e protezione di Microsoft in una singola esperienza di amministrazione e in un singolo Software Development Kit (SDK).
author: BryanLa
ms.service: information-protection
ms.topic: overview
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 775ae3d524947c8300de0e011b92c2cad106905a
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251727"
---
# <a name="overview"></a>Panoramica

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) riunisce i servizi di classificazione, etichettatura e protezione di Microsoft in una singola esperienza di amministrazione e in un singolo Software Development Kit (SDK). L'amministrazione unificata è disponibile per Office 365, Azure Information Protection, Windows Information Protection e ad altri servizi Microsoft. L'SDK può essere usato da terze parti per integrare le applicazioni, usando uno schema di etichettatura dei dati e un servizio di protezione standard e coerenti.

* [Che cos'è il Centro conformità e sicurezza di Office 365?](https://docs.microsoft.com/office365/securitycompliance/)
* [Che cos'è Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
* [Come funziona la protezione in Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK

MIP SDK espone i servizi di etichettatura e protezione dal Centro conformità e sicurezza di Office 365 ad applicazioni e servizi di terze parti. Gli sviluppatori possono usare l'SDK per creare il supporto nativo per l'applicazione di etichette e della protezione ai file. Gli sviluppatori possono prendere decisioni programmatiche sulle azioni da eseguire quando vengono rilevate etichette specifiche e sulle informazioni crittografate con MIP. 

Le etichette e la protezione applicate alle informazioni per la gamma di servizi di Microsoft sono **coerenti**. La coerenza consente alle applicazioni e ai servizi che supportano MIP di leggere e scrivere le etichette in un modo comune e prevedibile.

I casi d'uso generali per MIP SDK includono:

* Un'applicazione line-of-business che applica etichette di classificazione ai file durante l'esportazione.
* Un'applicazione di progettazione CAD/CAM che fornisce il supporto nativo per l'etichettatura di Microsoft Information Protection.
* Un CASB (Cloud Access Security Broker) o una soluzione di prevenzione della perdita dei dati che prende decisioni programmatiche per i dati crittografati con Azure Information Protection.

Per un elenco più esaustivo, vedere i [concetti relativi alle API](concept-apis-use-cases.md).

## <a name="next-steps"></a>Passaggi successivi

A questo punto è possibile iniziare a esplorare l'SDK. Per prima cosa, sarà necessario [completare i passaggi di installazione e configurazione di MIP SDK](setup-configure-mip.md), per assicurarsi che l'abbonamento a Office 365 e il computer client siano configurati correttamente.

