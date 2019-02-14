---
title: Microsoft Information Protection SDK C# Cenni preliminari sul Wrapper
description: Una rapida panoramica su come iniziare a usare il wrapper MIP SDK .NET e le differenze tra il wrapper .NET e C++ SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 6b2f26a61cd491574fd9f4a1e74fbfab4752257a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252317"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Guida introduttiva con il Wrapper .NET di Microsoft Information Protection

Il Wrapper di .NET SDK di Microsoft informazioni protezione dati consente agli sviluppatori di integrare l'esperienza di Microsoft Information Protection in per le proprie applicazioni e servizi. il SDK la classificazione, etichettatura e protezione della Guida di funzionalità per garantire che le informazioni sono classificate, etichettati e protetti indipendentemente da dove viaggia. 

Il wrapper gestito e tutte le dipendenze possono essere installate tramite NuGet in Visual Studio.

## <a name="supported-platforms"></a>Piattaforme supportate

Il Wrapper .NET di Microsoft informazioni Protection è supportato nelle piattaforme .NET seguenti:

* .NET Standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>Installazione del pacchetto

Dalla Console di gestione pacchetti in Visual Studio 2017, installare il pacchetto eseguendo:

`install-package Microsoft.InformationProtection.File`

Nessun pacchetti aggiuntivi sono necessari. Tutte le librerie di terze parti sono incluse e verranno copiati nella cartella di output in fase di compilazione.

## <a name="wrapper-details"></a>Dettagli di wrapper

Il wrapper .NET è un [SWIG](https://swig.org/) wrapper gestito generato. Il wrapper utilizza librerie C++ compilate dal SDK di Microsoft Information Protection. Queste DLL sono le stesse DLL inclusi con la versione di C++ del SDK.

## <a name="concept-overlap"></a>Concetto sovrapposizione

Esistono alcune differenze fondamentali tra la versione di C++ del SDK e il wrapper gestito.

* Il wrapper .NET non richiede l'uso di osservatori di operazioni asincrone. Tutte le operazioni asincrone vengono implementate usando il [Task-based Asynchronous Pattern](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap).
* Il wrapper .NET richiedono i delegati che fanno parte di C++ SDK: AuthDelegate e ConsentDelegate. Questi delegati vengono implementati tramite le interfacce `IAuthDelegate` e `IConsentDelegate`

## <a name="next-steps"></a>Passaggi successivi

Successivamente, esaminare [Guida introduttiva - inizializzazione per Microsoft Information Protection (MIP) SDK C# ](quick-app-initialization-csharp.md) informazioni introduttive sulla creazione di un'applicazione console abilitato MIP di base.
