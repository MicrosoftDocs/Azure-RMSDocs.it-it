---
title: Concetti - Osservatori in MIP SDK.
description: MIP SDK è progettato per essere quasi interamente asincrono. Questo articolo aiuterà a comprendere come gli osservatori vengono implementati e usati per l'asincronicità.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e42b9996d737ace5b25988eb72fa02aa87230f13
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "60175140"
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

Dato che vengono implementate due funzioni `Observer` per ogni operazione asincrona, si può presupporre che esistano **quattro** metodi `Observer` associati a `FileProfile`: 

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
