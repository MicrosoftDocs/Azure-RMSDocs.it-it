---
title: Concetti - Osservatori in MIP SDK.
description: MIP SDK è progettato per essere quasi interamente asincrono. Questo articolo aiuterà a comprendere come gli osservatori vengono implementati e usati per l'asincronicità.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: bd709b75c5b98c4241bc80f4a8542de30f48ff66
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555875"
---
# <a name="microsoft-information-protection-sdk---observer-concepts"></a>Microsoft Information Protection SDK - Concetti relativi agli osservatori

MIP SDK è progettato per essere quasi interamente asincrono. Ad esempio, qualsiasi operazione che genera I/O di rete o file viene eseguita in modo asincrono. Per gestire le notifiche degli eventi per questi eventi asincroni, l'SDK usa il [modello basato su osservatori](https://wikipedia.org/wiki/Observer_pattern). 

## <a name="implementation-overview"></a>Panoramica dell'implementazione

Quando si crea un oggetto che eseguirà un'operazione asincrona, deve essere implementata una classe `Observer`. Gli osservatori riceveranno gli eventi di notifica correlati alle diverse operazioni asincrone in MIP SDK e forniranno il risultato al chiamante.

Le funzioni in ogni classe `Observer` sono virtuali e vengono sottoposte a override per il modello asincrono preferito. L'SDK implementa il modello basato su osservatori per la notifica degli eventi tramite `std::promise` e `std::future`.

Ogni osservatore specifico della classe contiene un set di funzioni per esito positivo ed errore/esito negativo, per il risultato di un'operazione asincrona. Le funzioni per l'*esito positivo* restituiscono l'oggetto associato all'operazione. Le funzioni per *errore*/*esito negativo* restituiscono un'eccezione che contiene i dettagli sui motivi per cui l'operazione ha avuto esito negativo.

Ad esempio, `FileProfile` supporta le due operazioni seguenti: 

- Può aggiungere un nuovo motore al profilo tramite `FileProfile::AddEngineAsync`. 
- Può scaricare un motore dal profilo tramite `FileProfile::UnloadEngineAsync`.

Poiché due `Observer` funzioni vengono implementate per ogni operazione asincrona, si può presumere che ci siano **quattro** `Observer` metodi associati a `FileProfile`: 

- `FileProfileObserver::OnAddEngineSuccess()`
- `FileProfileObserver::OnAddEngineError()`
- `FileProfileObserver::OnUnloadEngineSuccess`
- `FileProfileObserver::OnUnloadEngineError()`. 

## <a name="mip-sdk-observer-classes"></a>Classi di osservatore di MIP SDK

L'API File di MIP SDK contiene due osservatori:

* `mip::FileProfile::Observer`
* `mip::FileHandler::Observer`

L'API Criteri di MIP SDK contiene un singolo osservatore:

* `mip::Profile::Observer`

L'API Protezione di MIP SDK contiene tre osservatori:

* `mip::ProtectionProfile::Observer`
* `mip::ProtectionEngine::Observer`
* `mip::ProtectionHandler::Observer`

## <a name="next-steps"></a>Passaggi successivi

Vedere altre informazioni su come gli osservatori sono implementati e usati dalle varie API:

* [Osservatori dell'API File (C++)](concept-async-observers-file-cpp.md)
* [Osservatori dell'API Criteri (C++)](concept-async-observers-policy-cpp.md)
* [Osservatori dell'API Protezione (C++)](concept-async-observers-protection-cpp.md)
