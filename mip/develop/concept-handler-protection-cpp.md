---
title: Concetti - Gestori protezione nel SDK MIP.
description: Questo articolo illustra le modalità di creazione e uso dei gestori dell'API per la chiamata di operazioni.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: b00078ba82d22ce37263162b3d7bb3d1f7d3a903
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886159"
---
# <a name="microsoft-information-protection-sdk---protection-handler-concepts"></a>Microsoft Information Protection SDK - Concetti del gestore di protezione

Nell'API di protezione del SDK MIP `mip::ProtectionHandler` espone funzioni per crittografare e decrittografare flussi protetti e buffer, eseguire controlli di accesso, ottenere la licenza di pubblicazione e recuperare attributi dalle informazioni protette.

## <a name="requirements"></a>Requisiti

Per creare un `ProtectionHandler` per lavorare con un file specifico esistono questi requisiti:

- Un elemento `mip::MipContext`
- Un elemento `mip::ProtectionProfile`
- Un elemento `mip::ProtectionEngine` aggiunto a `ProtectionProfile`
- Classe che eredita `mip::ProtectionHandler::Observer`.
- Un elemento `mip::ProtectionDescriptor` o una licenza di pubblicazione

## <a name="create-a-protection-handler"></a>Creare un gestore protezione dati

Gli oggetti `mip::ProtectionHandler` vengono costruiti fornendo un elemento `ProtectionDescriptor` o una licenza di pubblicazione serializzata a una di due funzioni `ProtectionEngine`. Il descrittore di protezione deve essere generato per la protezione delle informazioni in testo normale che non hanno ancora una licenza di pubblicazione. La **licenza di pubblicazione** viene usata durante la decrittografia di contenuto già protetto o per la protezione di contenuto in cui la licenza è già stata inclusa. Il contenuto protetto non può essere decrittografato senza la licenza di pubblicazione associata.

`mip::ProtectionEngine` espone due funzioni per la creazione di `ProtectionHandler`. I parametri sono gli stessi, fatta eccezione per il gestore o la licenza di pubblicazione come primo parametro.

- `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync`
  - Richiede come primo parametro un elemento `ProtectionDescriptor`.
- `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync`
  - Richiede come primo parametro una licenza di pubblicazione serializzata, archiviata in `std::vector<unint8_t>`.

### <a name="create-from-descriptor"></a>Creare dal descrittore

Quando si protegge contenuto che non è ancora stato protetto o quando si applica di nuovo la protezione al contenuto (il che implica che è stato decrittografato), è necessario creare un `mip::ProtectionDescriptor`. Dopo la creazione questo viene passato a `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync()` e il risultato viene restituito tramite `mip::ProtectionHandler::Observer`.

```cpp
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();
auto observer = std::make_shared<ProtectionHandlerObserverImpl>();

//Refer to ProtectionDescriptor docs for details on creating the descriptor
auto descriptor = CreateProtectionDescriptor(); //Stub function

mEngine->CreateProtectionHandlerFromDescriptorAsync(
    descriptor,
    mip::ProtectionHandlerCreationOptions::None,
    observer,
    handlerPromise);

auto handler = handlerFuture.get();
```

Dopo la creazione corretta dell'oggetto `ProtectionHandler` è possibile eseguire operazioni di file (get/set/delete/commit).

### <a name="create-from-publishing-license"></a>Creare dalla licenza di pubblicazione

Questo esempio presuppone che la licenza di pubblicazione sia già stata letta da un'origine e archiviata in `std::vector<uint8_t> serializedPublishingLicense`.

```cpp

//TODO: Implement GetPublishingLicense()
//Snip implies that function reads PL from source file, database, stream, etc.
std::vector<uint8_t> serializedPublishingLicense = GetPublishingLicense(filePath);

auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();

shared_ptr<ProtectionHandlerObserverImpl> handleObserver =
    std::make_shared<ProtectionHandlerObserverImpl>();

mEngine->CreateProtectionHandlerFromPublishingLicenseAsync(
    serializedPublishingLicense,
    mip::ProtectionHandlerCreationOptions::None,
    handleObserver,
    handlerPromise);

auto handler = handlerFuture.get();
```

