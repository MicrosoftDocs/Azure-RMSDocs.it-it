---
title: Istruzioni per sviluppatori per Azure Information Protection SDK 4.2 | Documentazione Microsoft
description: Scopri in che modo Microsoft Rights Management SDK 4,2 ti aiuta a creare applicazioni abilitate per AD RMS che sfruttano Active Directory Right Management Services (AD RMS).
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 01/23/2017
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae67523a-c094-44da-86b8-739bedba7111
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 957f347381b4de8abe4f828d4fd7903c0a0e62f3
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2020
ms.locfileid: "95567495"
---
# <a name="rights-management-sdk42-developer-guidance"></a>Guida per gli sviluppatori di Rights Management SDK 4,2

L'obiettivo di Microsoft Rights Management SDK 4.2 è consentire la creazione di applicazioni abilitate per AD RMS che sfruttano Active Directory Right Management Services (AD RMS) nel modo più semplice possibile.

Gli argomenti seguenti forniscono supporto durante il processo di progettazione per lo sviluppo di applicazioni abilitate per RMS.

- [Come registrare l'app e abilitarla per RMS con Azure AD](authentication-integration.md): descrive i concetti fondamentali dell'autenticazione utente per l'app abilitata per RMS.
- [Come abilitare la registrazione delle prestazioni e degli errori](enabling-logging.md): RMS SDK 4.2 gestisce il caricamento dei log delle diagnosi e delle prestazioni tramite una proprietà a dispositivo singolo.
- [Come usare i diritti predefiniti](built-in-rights-usage-restriction-reference.md): descrive i diritti predefiniti disponibili in RMS SDK 4.2 e le restrizioni di utilizzo che un'app deve applicare in conformità a tali diritti.
- [Come usare il rilevamento dei documenti](how-to-use-document-tracking.md): per usare la funzionalità di rilevamento dei documenti è necessario comprendere alcuni concetti semplici relativi alla gestione dei metadati associati e alla registrazione con il servizio.
