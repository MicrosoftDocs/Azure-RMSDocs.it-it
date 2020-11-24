---
title: Panoramica di Microsoft Information Protection SDK per il wrapper C#
description: Una rapida panoramica su come iniziare a usare il wrapper .NET di MIP SDK e le differenze tra .NET wrapper e C++ SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: da563bc385658d716d6813710495d91b42bbcc83
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567836"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Introduzione con il wrapper Microsoft Information Protection .NET

Il wrapper .NET di Microsoft Information Protection SDK consente agli sviluppatori di integrare l'esperienza Microsoft Information Protection in nelle proprie applicazioni e servizi. Le funzionalità di classificazione, assegnazione di etichette e protezione dell'SDK consentono di garantire che le informazioni vengano classificate, etichettate e protette indipendentemente dalla loro posizione. 

Il wrapper gestito e tutte le dipendenze possono essere installate tramite NuGet in Visual Studio.

## <a name="supported-platforms"></a>Piattaforme supportate

Il wrapper Microsoft Information Protection .NET è supportato nelle piattaforme .NET seguenti:

* .NET Standard 2.0
* .NET 4,0

## <a name="installing-the-package"></a>Installazione del pacchetto

Dalla console di gestione pacchetti in Visual Studio 2017 installare il pacchetto eseguendo:

`install-package Microsoft.InformationProtection.File`

Non sono necessari pacchetti aggiuntivi. Tutte le librerie di terze parti sono incluse e verranno copiate nella cartella di output durante la compilazione.

## <a name="wrapper-details"></a>Dettagli wrapper

Il wrapper .NET è un wrapper gestito generato da un [sorso](https://swig.org/) . Il wrapper usa le librerie C++ compilate da Microsoft Information Protection SDK. Queste dll sono le stesse dll incluse con la versione C++ dell'SDK.

## <a name="concept-overlap"></a>Sovrapposizione di concetti

Esistono alcune differenze fondamentali tra la versione C++ dell'SDK e il wrapper gestito.

* Il wrapper .NET non richiede l'uso di osservatori per le operazioni asincrone. Tutte le operazioni asincrone vengono implementate tramite il [modello asincrono basato su attività](/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap).
* Il wrapper .NET richiede i delegati che fanno parte di C++ SDK: AuthDelegate e ConsentDelegate. Questi delegati vengono implementati tramite le interfacce `IAuthDelegate` e `IConsentDelegate`

## <a name="next-steps"></a>Passaggi successivi

Esaminare quindi la [Guida introduttiva-inizializzazione per Microsoft Information Protection (MIP) SDK C#](quick-app-initialization-csharp.md) per iniziare a creare un'applicazione console abilitata per MIP di base.