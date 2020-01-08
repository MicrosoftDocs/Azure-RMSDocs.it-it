---
title: Concetti - Oggetto motore dell'API Protezione
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto motore dell'API Protezione, che viene creato durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 116bd67298195e66de26ab278802e93644a095dd
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556096"
---
# <a name="microsoft-information-protection-sdk---protection-api-engine-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al motore dell'API Protezione

## <a name="implementation-add-a-protection-engine"></a>Implementazione: Aggiungere un motore di protezione

Nell'API Protezione, la classe `mip::ProtectionProfile` è la classe radice per tutte le operazioni dell'SDK. Avendo già creato il profilo, è ora possibile aggiungere un motore al profilo.

L'esempio seguente illustra l'uso di un solo motore per un unico utente autenticato.

### <a name="implementation-create-protection-engine-settings"></a>Implementazione: Creare le impostazioni del motore di protezione

Analogamente a un profilo, anche per il motore è necessario un oggetto impostazioni, `mip::ProtectionEngine::Settings`. Questo oggetto archivia l'identificatore univoco del motore, i dati client personalizzabili che possono essere usati per il debug o la telemetria e, facoltativamente, le impostazioni locali.

Viene qui creato un oggetto `ProtectionEngine::Settings` chiamato *engineSettings*. 

```cpp
ProtectionEngine::Settings engineSettings("UniqueID", "");
```

> [!NOTE]
> Se si utilizza questo metodo per creare l'oggetto impostazioni di protezione, è inoltre necessario impostare manualmente CloudEndpointBaseUrl su https://api.aadrm.com o TP l'URL del cluster del servizio Active Directory Rights Management.

Come procedura consigliata, il primo parametro, **id**, deve essere tale da consentire di collegare il motore con facilità all'utente associato **oppure** a un oggetto `mip::Identity`. Per inizializzare le impostazioni con `mip::Identity`:

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity("Bob@Contoso.com", "");
```

### <a name="implementation-add-the-protection-engine"></a>Implementazione: Aggiungere il motore di protezione

Per aggiungere il motore, si tornerà al modello promise/future usato per caricare il profilo. Invece di creare la promessa per `mip::ProtectionProfile`, si userà `mip::ProtectionEngine`.

```cpp

  //auto profile will be std::shared_ptr<mip::ProtectionProfile>
  auto profile = profileFuture.get();

  //Create the ProtectionEngine::Settings object
  ProtectionEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::ProtectionEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::ProtectionEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::ProtectionEngine>
  auto engine = engineFuture.get();
```

Il risultato finale del codice precedente è l'aggiunta di un motore per l'utente autenticato al profilo.

## <a name="implementation-list-templates"></a>Implementazione: Elencare i modelli

Tramite il motore aggiunto è ora possibile elencare tutti i modelli di riservatezza disponibili per l'utente autenticato chiamando `engine->GetTemplatesAsync()`. 

`GetTemplatesAsync()` recupererà l'elenco degli identificatori dei modelli. Il risultato viene archiviato in un vettore di `std::shared_ptr<std::string>`.

### <a name="implementation-listsensitivitytemplates"></a>Implementazione: ListSensitivityTemplates()

```cpp
auto loadPromise = std::make_shared<std::promise<shared_ptr<vector<string>>>>();
std::future<std::shared_ptr<std::vector<std::string>>> loadFuture = loadPromise->get_future();
mEngine->GetTemplatesAsync(engineObserver, loadPromise);
auto templates = loadFuture.get();
```

### <a name="implementation-print-the-template-ids"></a>Implementazione: Stampare gli ID dei modelli

```cpp
//Iterate through all template IDs in the vector
for (const auto& temp : *templates) {
  cout << "Template:" << "\n\tId: " << temp << endl;
}
```

La stampa dei nomi è un modo semplice per mostrare che è stato eseguito correttamente il pull dei criteri dal servizio e si è riusciti a ottenere i modelli. Per applicare il modello, è necessario l'identificatore del modello.

Il mapping dei modelli alle etichette può essere eseguito solo tramite l'API Criteri, esaminando il risultato di `ComputeActions()`.

## <a name="next-steps"></a>Passaggi successivi

Ora che il profilo è caricato, il motore è stato aggiunto e sono disponibili modelli, è possibile aggiungere un gestore per iniziare a leggere, scrivere o rimuovere i modelli dai file. Vedere i [concetti relativi al gestore della protezione](concept-handler-protection-cpp.md).
