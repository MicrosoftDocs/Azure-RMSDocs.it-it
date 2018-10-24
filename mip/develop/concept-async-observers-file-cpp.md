---
title: Concetti - Osservatori dell'API File in MIP SDK.
description: MIP SDK è progettato per essere quasi interamente asincrono. Questo articolo aiuterà a comprendere come gli osservatori dell'API File vengono implementati e usati per l'asincronicità.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: d150e59c98300bfe20ced0b1a453a899558d1f27
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446261"
---
# <a name="microsoft-information-protection-sdk---file-api-observers"></a>Microsoft Information Protection SDK - Osservatori dell'API File

L'API File contiene due classi osservatore. I membri della classe osservatore sono virtuali e possono essere sottoposti a override per gestire i callback degli eventi.

- [`mip::FileProfile::Observer`](reference/class_mip_fileprofile_observer.md)
- [`mip::FileHandler::Observer`](reference/class_mip_filehandler_observer.md)

Al termine di un'operazione asincrona, viene chiamata la funzione membro `OnXxx()` corrispondente al risultato. Sono esempi `OnLoadSuccess()`, `OnLoadFailure()` e `OnAddEngineSuccess()` per `mip::FileProfile::Observer`.

Gli esempi seguenti illustrano il modello promise/future, usato anche dagli esempi dell'SDK, e possono essere estesi per implementare il comportamento di callback desiderato. 

## <a name="file-profile-observer-implementation"></a>Implementazione dell'osservatore del profilo File

Nell'esempio seguente è stata creata una classe `ProfileObserver` derivata da `mip::FileProfile::Observer`. Le funzioni membro sono state sottoposte a override per sfruttare il modello promise/future usato in tutti gli esempi.

**Nota**: gli esempi di seguito sono implementati solo parzialmente e non includono gli override per gli osservatori correlati `mip::FileEngine`.

### <a name="profileobserverh"></a>profile_observer.h

Nell'intestazione si definisce `ProfileObserver`, che deriva da `mip::FileProfile::Observer`, quindi si esegue l'override di tutte le funzioni membro.

```cpp
class ProfileObserver final : public mip::FileProfile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement mip::FileEngine related observers.
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

Nell'implementazione stessa si definisce un'azione da eseguire per ogni funzione membro dell'osservatore.

Ogni membro accetta due parametri. Il primo è un puntatore condiviso alla classe gestita nella funzione. `ProfileObserver::OnLoadSuccess` si aspetta di ricevere un `mip::FileProfile`. `ProfileObserver::OnAddEngineSuccess` si aspetta `mip::FileEngine`.

Il secondo è un puntatore condiviso al *contesto*. In questa implementazione il contesto è un riferimento a `std::promise`, passato per riferimento come `std::shared_ptr<void>`. La prima riga della funzione esegue il cast su `std::promise`, che viene poi archiviato in un oggetto denominato `promise`.

Infine, l'elemento future viene preparato impostando `promise->set_value()` e passando l'oggetto `mip::FileProfile`.

```cpp
#include "profile_observer.h"
#include <future>

//Called when FileProfile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = 
  std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when FileProfile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement mip::FileEngine related observers.
```

Quando si crea un'istanza di qualsiasi classe dell'SDK o si usa una funzione che esegue operazioni asincrone, l'implementazione dell'osservatore verrà passata al costruttore delle impostazioni o alla funzione asincrona stessa. Quando si creano istanze dell'oggetto `mip::FileProfile::Settings`, il costruttore accetta `mip::FileProfile::Observer` come uno dei parametri. L'esempio seguente mostra l'implementazione personalizzata `ProfileObserver`, usata in un costruttore `mip::FileProfile::Settings`.

## <a name="filehandler-observer-implementation"></a>Implementazione dell'osservatore FileHandler

In modo analogo all'osservatore del profilo, `mip::FileHandler` implementa una classe `mip::FileHandler::Observers` per la gestione delle notifiche degli eventi asincroni durante le operazioni sui file. L'implementazione è simile a quella descritta in dettaglio in precedenza. L'implementazione `FileHandlerObserver` è definita parzialmente di seguito. 

### <a name="filehandlerobserverh"></a>file_handler_observer.h

```cpp
#include "mip/file/file_handler.h"

class FileHandlerObserver final : public mip::FileHandler::Observer {
public:
  void OnCreateFileHandlerSuccess(
      const std::shared_ptr<mip::FileHandler>& fileHandler,
      const std::shared_ptr<void>& context) override;

  void OnCreateFileHandlerFailure(
      const std::exception_ptr& error,
      const std::shared_ptr<void>& context) override;

  //TODO: override remaining member functions inherited from mip::FileHandler::Observer
};
```

### <a name="filehandlerobservercpp"></a>file_handler_observer.cpp

Questo esempio riguarda solo le prime due funzioni, ma le funzioni rimanenti usano un modello simile per queste implementazioni e per `ProfileObserver`.

```cpp
#include "file_handler_observer.h"

void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_value(fileHandler);
}

void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_exception(error);
}

//TODO: override remaining member functions inherited from mip::FileHandler::Observer
```

