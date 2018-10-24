---
title: Concetti - Oggetto profilo dell'API File
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto profilo dell'API File, che viene creato durante l'inizializzazione dell'applicazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 33ec266068d15e827267b7d518344aebd0f8f072
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445904"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al profilo dell'API File

Il profilo è la classe radice per tutte le operazioni in MIP SDK. Prima di usare qualsiasi funzionalità dell'API File, è necessario creare un `FileProfile` e tutte le operazioni future verranno eseguite dal profilo o da altri oggetti *aggiunti* al profilo.

Esistono alcuni prerequisiti per il codice che devono essere soddisfatti prima di tentare di creare un'istanza di un profilo:

- Implementazione di `AuthDelegateImpl` per estendere `mip::AuthDelegate`.
- Implementazione di `ConsentDelegateImpl` per estendere `mip::ConsentDelegate`.
- [Registrazione dell'applicazione in Azure Active Directory](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) e ID client hardcoded nei file di configurazione o dell'applicazione. 
- Implementazione appropriata di una classe che eredita `mip::FileProfile::Observer`.

## <a name="load-a-profile"></a>Caricare un profilo

Dopo aver definito `ProfileObserver`, `ConsentDelegateImpl` e `AuthDelegateImpl`, è ora possibile creare un'istanza di `mip::FileProfile`. La creazione dell'oggetto `mip::FileProfile` richiede [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) per l'archiviazione di tutte le informazioni sulle impostazioni per `FileProfile`.

### <a name="fileprofilesettings-parameters"></a>Parametri di FileProfile::Settings

Il costruttore `FileProfile::Settings` accetta cinque parametri, elencati di seguito:

- `std::string path`: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
- `bool useInMemoryStorage`: definisce se tutti gli stati devono essere archiviati o meno in memoria invece che su disco.
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: puntatore condiviso della classe `mip::AuthDelegate`. 
- `std::shared_ptr<mip::ConsentDelegate>`: 
- `std::shared_ptr<mip::FileProfile::Observer> observer`: puntatore condiviso all'implementazione `FileProfile::Observer`.
- `mip::ApplicationInfo applicationInfo`: oggetto. Usato per definire informazioni relative all'applicazione che sta utilizzando l'SDK.

Gli esempi seguenti mostrano come creare l'oggetto `profileSettings` usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

#### <a name="store-state-in-memory-only"></a>Archiviare lo stato solo in memoria

```cpp
FileProfile::Settings profileSettings(
    "",                                          //path to store settings
    true,                                        //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Leggere/scrivere le impostazioni del profilo dal percorso di archiviazione su disco

Il frammento di codice seguente indicherà a `FileProfile` di archiviare tutti i dati sullo stato dell'app in `./mip_app_data`.

```cpp
FileProfile::Settings profileSettings(
    "./mip_app_data",                            //path to store settings
    false,                                       //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="load-the-profile"></a>Caricare il profilo

Usando i dettagli di uno degli approcci sopra indicati, usare ora il modello promise/future per caricare il `FileProfile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<FileProfile>>>();
auto profileFuture = profilePromise->get_future();
FileProfile::LoadAsync(profileSettings, profilePromise);
```

Se fosse stato caricato un profilo e tale operazione fosse stata completata correttamente (`ProfileObserver::OnLoadSuccess`), verrebbe chiamata l'implementazione di `mip::FileProfile::Observer::OnLoadSuccess`. L'oggetto risultante o il puntatore dell'eccezione, nonché il contesto, vengono passati come parametri alla funzione. Il contesto è un puntatore a `std::promise` creato per gestire l'operazione asincrona. La funzione imposta semplicemente il valore della promessa sull'oggetto FileProfile passato per il primo parametro. Quando la funzione main usa `Future.get()`, il risultato può essere archiviato in un nuovo oggetto.

```cpp
//get the future value and store in profile. 
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>Riepilogo

Dopo aver completato l'implementazione degli osservatori e del delegato di autenticazione, è ora possibile caricare completamente un profilo. Il frammento di codice riportato di seguito presuppone che tutte le intestazioni necessarie siano già incluse.

```cpp
int main()
{
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    FileProfile::Settings profileSettings("",
            false,
            authDelegateImpl,
            std::make_shared<ConsentDelegateImpl>(),
            std::make_shared<ProfileObserver>(),
            mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<FileProfile>>>();
    auto profileFuture = profilePromise->get_future();
    FileProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Il risultato finale è il caricamento corretto del profilo e l'archiviazione nell'oggetto denominato `profile`.

## <a name="next-steps"></a>Passaggi successivi

Ora che il profilo è stato aggiunto, il passaggio successivo consiste nell'aggiungere un motore al profilo. 

- [Concetti relativi al motore di file](concept-profile-engine-file-engine-cpp.md)