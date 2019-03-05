---
title: Concetti - Osservatori dell'API Criteri in MIP SDK.
description: MIP SDK è progettato per essere quasi interamente asincrono. Questo articolo aiuterà a comprendere come gli osservatori dell'API Criteri vengono implementati e usati per l'asincronicità.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e8f2e2c775270f81489778ced852a7bb26b5ad1c
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330288"
---
# <a name="microsoft-information-protection-sdk---policy-api-observers"></a>Microsoft Information Protection SDK - Osservatori dell'API Criteri

L'SDK dell'API Criteri contiene una classe osservatore. I membri della classe osservatore sono virtuali e devono essere sottoposti a override per gestire i callback per le operazioni asincrone.

- [`mip::PolicyProfile::Observer`](reference/class_mip_policyprofile_observer.md)

Al termine di un'operazione asincrona, viene chiamata la funzione membro `OnXxx()` corrispondente al risultato. Sono esempi `OnLoadSuccess()`, `OnLoadFailure()` e `OnAddEngineSuccess()` per `mip::Profile::Observer`.

Gli esempi seguenti illustrano il modello promise/future, usato anche dagli esempi dell'SDK, e possono essere estesi per implementare il comportamento di callback desiderato. 

## <a name="profile-observer-implementation"></a>Implementazione dell'osservatore del profilo

Nell'esempio seguente è stata creata una classe `ProfileObserver` derivata da `mip::Profile::Observer`. Le funzioni membro sono state sottoposte a override per sfruttare il modello promise/future usato in tutti gli esempi.

**Nota**: Di seguito esempi sono implementati solo parzialmente e non includono le sostituzioni per il `mip::ProfileEngine` relativi osservatori.

### <a name="profileobserverh"></a>profile_observer.h

Nell'intestazione si definisce `ProfileObserver`, che deriva da `mip::Profile::Observer`, quindi si esegue l'override di tutte le funzioni membro.

```cpp
class ProfileObserver final : public mip::Profile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement remaining members
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

Nell'implementazione stessa si definisce un'azione da eseguire per ogni funzione membro dell'osservatore.

Ogni membro accetta due parametri. Il primo è un puntatore condiviso alla classe gestita dalla funzione. `ProfileObserver::OnLoadSuccess` si aspetta di ricevere un `mip::Profile`. `ProfileObserver::OnAddEngineSuccess` si aspetta `mip::ProfileEngine`.

Il secondo è un puntatore condiviso al *contesto*. In questa implementazione il contesto è un riferimento a `std::promise`, passato come `shared_ptr<void>`. La prima riga della funzione esegue il cast su `std::promise`, che viene poi archiviato in un oggetto denominato `promise`.

Infine, l'elemento future viene preparato impostando `promise->set_value()` e passando l'oggetto `mip::Profile`.

```cpp
#include "profile_observer.h"
#include <future>

//Called when Profile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when Profile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement remaining observer members
```

Quando si esegue qualsiasi operazione asincrona, l'implementazione dell'osservatore viene passata al costruttore delle impostazioni o alla funzione asincrona stessa. 

