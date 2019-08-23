---
title: Concetti - Oggetto motore dell'API Criteri
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto motore dell'API Criteri, che viene creato durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 5fac6b39cb3770748336fac7264134acf2627a02
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886075"
---
# <a name="microsoft-information-protection-sdk---policy-api-engine-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al motore dell'API Criteri

`mip::PolicyEngine` implementa tutte le operazioni che può eseguire l'API Criteri, fatta eccezione per il caricamento del profilo.

## <a name="implementation-add-a-policy-engine"></a>Implementazione Aggiungere un motore dei criteri

### <a name="implementation-create-policy-engine-settings"></a>Implementazione Creare le impostazioni del motore dei criteri

Analogamente a un profilo, anche per il motore è necessario un oggetto impostazioni, `mip::PolicyEngine::Settings`. Questo oggetto archivia l'identificatore univoco del motore, i dati client personalizzabili che possono essere usati per il debug o la telemetria e, facoltativamente, le impostazioni locali.

Qui viene creato un `FileEngine::Settings` oggetto denominato *engineSettings* usando l'identità dell'utente dell'applicazione:

```cpp
PolicyEngine::Settings engineSettings(
  mip::Identity(mUsername), // mip::Identity.
  "",                       // Client data. Customizable by developer, stored with engine.
  "en-US",                  // Locale.
  false);                   // Load sensitive information types for driving classification.
```

Valido anche per fornire un ID del motore personalizzato:

```cpp
PolicyEngine::Settings engineSettings(
  "myEngineId", // string
  "",           // Client data in string format. Customizable by developer, stored with engine.
  "en-US",      // Locale. Default is en-US
  false);       // Load sensitive information types for driving classification. Default is false.
```

Come procedura consigliata, il primo parametro, **id**, deve essere tale da consentire di collegare il motore con facilità all'utente associato, preferibilmente il nome dell'entità utente.

### <a name="implementation-add-the-policy-engine"></a>Implementazione Aggiungere il motore dei criteri

Per aggiungere il motore, si tornerà al modello promise/future usato per caricare il profilo. Invece di creare la promessa per `mip::Profile`, si userà `mip::PolicyEngine`.

```cpp

  //auto profile will be std::shared_ptr<mip::Profile>
  auto profile = profileFuture.get();

  //Create the PolicyEngine::Settings object
  PolicyEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::PolicyEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::PolicyEngine>
  auto engine = engineFuture.get();
```

Il risultato finale del codice precedente è l'aggiunta di un motore per l'utente autenticato al profilo.

## <a name="implementation-list-sensitivity-labels"></a>Implementazione Elencare le etichette di riservatezza

Tramite il motore aggiunto è ora possibile elencare tutte le etichette di riservatezza disponibili per l'utente autenticato chiamando `engine->ListSensitivityLabels()`.

`ListSensitivityLabels()` recupererà l'elenco di etichette e degli attributi di tali etichette per un utente specifico dal servizio. Il risultato viene archiviato in un vettore di `std::shared_ptr<mip::Label>`.

### <a name="implementation-listsensitivitylabels"></a>Implementazione ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

### <a name="implementation-print-the-labels"></a>Implementazione Stampare le etichette

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //print the label name
  cout << label->GetName() << endl;
  //Iterate through all child labels
  for (const auto& child : label->GetChildren()) {
    //Print the label with some formatting
    cout << "->  " << child->GetName() << endl;
  }
}
```

La stampa dei nomi è un modo semplice per mostrare che è stato eseguito correttamente il pull dei criteri dal servizio e si è riusciti a ottenere le etichette. Per applicare l'etichetta, è necessario l'identificatore dell'etichetta. Il risultato della modifica del frammento di codice precedente per restituire l'ID dell'etichetta è il seguente:

```cpp
for (const auto& label : labels) {
  //Print label name and GUID
  cout << label->GetName() << " : " << label->GetId() << endl;

  //Print child label name and GUID
  for (const auto& child : label->GetChildren()) {
    cout << "->  " << child->GetName() <<  " : " << child->GetId() << endl;
  }
}
```

La raccolta di `mip::Label` restituita da `GetSensitivityLabels()` può essere usata per visualizzare tutte le etichette disponibili per l'utente e quindi, se selezionata, per usare l'ID per applicare le etichette a un file.
