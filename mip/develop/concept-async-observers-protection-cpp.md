---
title: Concetti - Osservatori dell'API Protezione in MIP SDK.
description: MIP SDK è progettato per essere quasi interamente asincrono. Questo articolo aiuterà a comprendere come gli osservatori dell'API Protezione vengono implementati e usati per l'asincronicità.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 2d1cf81e20a317ecb1eb9e71b5b4e0ab32482877
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175548"
---
# <a name="microsoft-information-protection-sdk---protection-api-observers"></a>Microsoft Information Protection SDK - Osservatori dell'API Protezione

L'API Protezione contiene tre classi osservatore. I membri della classe osservatore sono virtuali e possono essere sottoposti a override per gestire i callback per le operazioni asincrone.

- [Profilo di protezione: `mip::ProtectionProfile::Observer`](reference/class_mip_ProtectionProfile_observer.md)
- [Motore di protezione: `mip::ProtectionEngine::Observer`](reference/class_mip_ProtectionEngine_observer.md)
- [Gestore della protezione: `mip::ProtectionHandler::Observer`](reference/class_mip_Protectionhandler_observer.md)

Al termine di un'operazione asincrona, viene chiamata la funzione membro `OnXxx()` corrispondente al risultato. Sono esempi `OnLoadSuccess()`, `OnLoadFailure()` e `OnAddEngineSuccess()` per `mip::ProtectionProfile::Observer`.

Gli esempi seguenti illustrano il modello promise/future, usato anche dagli esempi dell'SDK, e possono essere estesi per implementare il comportamento di callback desiderato. 

## <a name="protectionprofile-observer-implementation"></a>Implementazione dell'osservatore ProtectionProfile

Nell'esempio seguente è stata creata una classe `ProtectionProfileObserverImpl` derivata da `mip::ProtectionProfile::Observer`. Le funzioni membro sono state sottoposte a override per sfruttare il modello promise/future usato in tutti gli esempi.

### <a name="protectionprofileobserverimpl-class-declaration"></a>Dichiarazione della classe ProtectionProfileObserverImpl

Nell'intestazione si definisce `ProtectionProfileObserverImpl`, che deriva da `mip::ProtectionProfile::Observer`, quindi si esegue l'override di tutte le funzioni membro.

```cpp
//ProtectionProfileObserverImpl.h
class ProtectionProfileObserverImpl final : public mip::ProtectionProfile::Observer {
public:
  ProtectionProfileObserverImpl() { }
  void OnLoadSuccess(const shared_ptr<mip::ProtectionProfile>& profile, const shared_ptr<void>& context) override;
  void OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) override;
  void OnAddEngineSuccess(const shared_ptr<mip::ProtectionEngine>& engine, const shared_ptr<void>& context) override;
  void OnAddEngineError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionprofileobserverimpl-implementation"></a>Implementazione di ProtectionProfileObserverImpl

Nell'implementazione stessa si definisce semplicemente un'azione da eseguire per ogni funzione membro dell'osservatore.

Ogni membro accetta due parametri. Il primo è un puntatore condiviso alla classe gestita nella funzione. `ProtectionObserver::OnLoadSuccess` si aspetta di ricevere un `mip::ProtectionProtection`, `ProtectionObserver::OnAddEngineSuccess` si aspetta `mip::ProtectionEngine`.

Il secondo è un puntatore condiviso al *contesto*. In questa implementazione il contesto è un riferimento a `std::promise`, passato come `shared_ptr<void>`. La prima riga della funzione esegue il cast su `std::promise`, che viene poi archiviato in un oggetto denominato `promise`.

Infine, l'elemento future viene preparato impostando `promise->set_value()` e passando l'oggetto `mip::ProtectionProtection`.

```cpp
//protection_observers.cpp

void ProtectionProfileObserverImpl::OnLoadSuccess(
  const shared_ptr<mip::ProtectionProfile>& profile,
  const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_value(profile);
};

void ProtectionProfileObserverImpl::OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_exception(error);
};

void ProtectionProfileObserverImpl::OnAddEngineSuccess(
  const shared_ptr<mip::ProtectionEngine>& engine,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_value(engine);
};

void ProtectionProfileObserverImpl::OnAddEngineError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_exception(error);
};
```

Quando si crea un'istanza di qualsiasi classe dell'SDK o si usa una funzione che esegue operazioni asincrone, l'implementazione dell'osservatore verrà passata al costruttore delle impostazioni o alla funzione asincrona stessa. Quando si creano istanze dell'oggetto `mip::ProtectionProfile::Settings`, il costruttore accetta `mip::ProtectionProfile::Observer` come uno dei parametri. L'esempio seguente mostra l'implementazione personalizzata `ProtectionProfileObserverImpl`, usata in un costruttore `mip::ProtectionProfile::Settings`.

## <a name="protectionhandler-observer-implementation"></a>Implementazione dell'osservatore ProtectionHandler

In modo analogo all'osservatore di protezione, `mip::ProtectionHandler` implementa una classe `mip::ProtectionHandler::Observer` per la gestione delle notifiche degli eventi asincroni durante le operazioni di protezione. L'implementazione è simile a quella descritta in dettaglio in precedenza. L'implementazione `ProtectionHandlerObserverImpl` è definita parzialmente di seguito. L'implementazione completa è disponibile nel [repository degli esempi su GitHub](https://azure.microsoft.com/resources/samples/?sort=0&term=mip+sdk).

### <a name="protectionhandlerobserverimpl-class-declaration"></a>Dichiarazione della classe ProtectionHandlerObserverImpl

```cpp
//protection_observers.h

class ProtectionHandlerObserverImpl final : public mip::ProtectionHandler::Observer {
public:
  ProtectionHandlerObserverImpl() { }
  void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
  void OnCreateProtectionHandlerError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionhandlerobserverimpl-partial-implementation"></a>Implementazione parziale di ProtectionHandlerObserverImpl

Questo esempio riguarda solo le prime due funzioni, ma le funzioni rimanenti usano un modello simile per queste implementazioni e per `ProtectionObserver`.

```cpp
//protection_observers.cpp

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerSuccess(
  const shared_ptr<mip::ProtectionHandler>& protectionHandler,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_value(protectionHandler);
};

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_exception(error);
};
```

