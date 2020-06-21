---
title: RMS SDK 4,2-avviso di deprecazione
description: RMS SDK 4,2-avviso di deprecazione
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
ms.date: 03/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 14ea411732b38883d278d4df22700b8503224be0
ms.sourcegitcommit: 307258ff0a8a7a3f607c8f47f38a9801d0e06ba1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/21/2020
ms.locfileid: "85126646"
---
# <a name="rms-sdk-42-deprecation-notice"></a>RMS SDK 4,2-avviso di deprecazione 

*Applicabile a tutte le versioni di RMS SDK 4,2 versione precedente al 2020 marzo*

Il 3 marzo 2020, un aggiornamento alla RMS SDK 4,2 per Android, iOS e OSX è stato rilasciato tramite l'area download Microsoft. Questo aggiornamento è obbligatorio per tutte le applicazioni che usano attualmente le piattaforme RMS SDK.  

Il martedì 15 settembre 2020 le versioni del RMS SDK rilasciate prima del marzo 2020 non riusciranno a connettersi all'endpoint del servizio Rights Management di Azure. Le applicazioni che utilizzano RMS SDK 4,2 devono essere aggiornate prima di questa data. 

## <a name="reason-for-change"></a>Motivo della modifica 

Le versioni precedenti del RMS SDK usano l'aggiunta di certificati per garantire che il client abilitato per RMS comunichi con il servizio RMS, ricevendo un certificato concatenato a una CA radice prevista specifica.  

I browser moderni usano i registri di trasparenza dei certificati per verificare che i certificati siano stati rilasciati ai proprietari di dominio legittimi e che i certificati vengano emessi da autorità di certificazione radice attendibili.  

Per supportare al meglio i browser moderni, il 15 settembre 2020, Microsoft aggiornerà il certificato per `https://api.aadrm.com` a un nuovo certificato emesso da una CA radice attendibile a livello globale che segnala i certificati emessi ai log di trasparenza certificati attendibili dai browser moderni. Al termine di questa modifica, le versioni legacy di RMS SDK il tentativo di eseguire l'aggiunta del certificato al certificato radice previsto non riuscirà a trovare il certificato e non riuscirà a connettersi.  

## <a name="client-impact"></a>Effetto client 

Le applicazioni Microsoft seguenti usano attualmente gli SDK RMS. Gli aggiornamenti saranno resi disponibili per queste piattaforme e i dispositivi devono essere aggiornati prima della scadenza di settembre. 

- Office 2019 per Mac 
- Office 2016 per Mac 
- Word, Excel e PowerPoint per iOS 
- Word, Excel e PowerPoint per Android 

Risorse 

- Android: https://www.microsoft.com/download/details.aspx?id=43673
- iOShttps://www.microsoft.com/download/details.aspx?id=43674 
- macOS: https://www.microsoft.com/download/details.aspx?id=43675 
- Linux: https://azuread.github.io/rms-sdk-for-cpp/annotated.html