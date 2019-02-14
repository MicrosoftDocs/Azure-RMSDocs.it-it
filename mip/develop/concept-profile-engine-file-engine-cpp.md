---
title: Concetti - Oggetto motore dell'API File
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto motore dell'API File, che viene creato durante l'inizializzazione dell'applicazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 09b4db10523539f093a54c54d1fc6b7de8f7ddb0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259287"
---
# <a name="microsoft-information-protection-sdk---file-api-engine-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al motore dell'API File

`mip::FileEngine` nell'API File di MIP SDK offre un'interfaccia per tutte le operazioni eseguite per conto di un'identità specificata. Verrà aggiunto un motore per ogni utente che accede all'applicazione e tutte le operazioni del motore verranno eseguite nel contesto di tale identità.

Il `FileEngine` ha due responsabilità principali: Elenca le etichette per un utente autenticato e creazione di gestori di file per eseguire operazioni di file per conto dell'utente. 

- [`mip::FileEngine`](reference/class_mip_fileengine.md)
- `ListSensitivityLabels()`: Ottiene l'elenco di etichette per il motore caricato.
- `CreateFileHandler()`: Crea un `mip::FileHandler` per un flusso o file specifici.

## <a name="add-a-file-engine"></a>Aggiungere un motore di file

Come descritto in [Oggetti profilo e motore](concept-profile-engine-cpp.md), un motore può avere due stati: `CREATED` o `LOADED`. Se non è in uno di questi due stati, non esiste. Per creare e caricare uno stato, è necessario eseguire una singola chiamata a `FileProfile::LoadAsync`. Se il motore esiste già nello stato memorizzato nella cache, sarà `LOADED`. Se non esiste, sarà `CREATED` e `LOADED`. `CREATED` implica che l'applicazione ha tutte le informazioni dal servizio necessarie per caricare il motore. `LOADED` implica che tutte le strutture di dati necessarie per sfruttare il motore sono state create in memoria.

### <a name="create-file-engine-settings"></a>Creare le impostazioni del motore di file

Analogamente a un profilo, anche per il motore è necessario un oggetto impostazioni, `mip::FileEngine::Settings`. Questo oggetto archivia l'identificatore univoco del motore, i dati client personalizzabili che possono essere usati per il debug o la telemetria e, facoltativamente, le impostazioni locali.

Viene qui creato un oggetto `FileEngine::Settings` chiamato *engineSettings*. 

```cpp
FileEngine::Settings engineSettings("UniqueID", "");
```

Come procedura consigliata, il primo parametro, `id`, deve essere tale da consentire di collegare il motore con facilità all'utente associato. Elementi come l'indirizzo di posta elettronica, il nome dell'entità utente o un GUID dell'oggetto AAD potrebbero garantire che l'ID sia univoco e possa essere caricato dallo stato locale senza chiamare il servizio.

### <a name="add-the-file-engine"></a>Aggiungere il motore di file

Per aggiungere il motore, si tornerà al modello promise/future usato per caricare il profilo. Invece di creare la promessa per `mip::FileProfile`, questa viene creata con `mip::FileEngine`.

```cpp
  //auto profile will be std::shared_ptr<mip::FileProfile>
  auto profile = profileFuture.get();

  //Create the FileEngine::Settings object
  FileEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::FileEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::FileEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::FileEngine>
  auto engine = engineFuture.get();
```

Il risultato finale del codice precedente è l'aggiunta al profilo del motore per l'utente autenticato.

## <a name="list-sensitivity-labels"></a>Elencare le etichette di riservatezza

Tramite il motore aggiunto è ora possibile elencare tutte le etichette di riservatezza disponibili per l'utente autenticato chiamando `engine->ListSensitivityLabels()`.

`ListSensitivityLabels()` recupererà l'elenco di etichette e degli attributi di tali etichette per un utente specifico dal servizio. Il risultato viene archiviato in un vettore di `std::shared_ptr<mip::Label>`.

[Qui]() sono disponibili altre informazioni su `mip::Label`.

### <a name="listsensitivitylabels"></a>ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

Oppure, in forma semplificata:

```cpp
auto labels = engine->ListSensitivityLabels();
```

### <a name="print-the-labels-and-ids"></a>Stampare le etichette e gli ID

La stampa dei nomi è un modo semplice per mostrare che è stato eseguito correttamente il pull dei criteri dal servizio e si è riusciti a ottenere le etichette. Per applicare l'etichetta, è necessario l'identificatore dell'etichetta. Il codice seguente esegue l'iterazione di tutte le etichette, visualizzando `name` e `id` per ogni etichetta padre e figlio.

```cpp
//Iterate through all labels in the vector
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

## <a name="next-steps"></a>Passaggi successivi

Ora che il profilo è caricato, il motore è stato aggiunto e sono disponibili etichette, è possibile aggiungere un gestore per iniziare a leggere, scrivere o rimuovere le etichette dai file. Vedere [Gestori di file in MIP SDK](concept-handler-file-cpp.md).

