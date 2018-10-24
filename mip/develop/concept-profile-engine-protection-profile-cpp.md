---
title: Concetti - Oggetto profilo dell'API Protezione
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto profilo dell'API Protezione, che viene creato durante l'inizializzazione dell'applicazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ae6699212d45a6c8a2fa95f648e7f5a2be3de93e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445309"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al profilo dell'API Protezione

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

## <a name="load-a-profile"></a>Caricare un profilo

Dopo aver definito `ProtectionProfileObserverImpl` e `AuthDelegateImpl`, verranno usati per creare un'istanza di `mip::ProtectionProfile`. Per la creazione dell'oggetto `mip::ProtectionProfile` è richiesto [`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md).

### <a name="protectionprofilesettings-parameters"></a>Parametri ProtectionProfile::Settings

- `std::string path`: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
- `bool useInMemoryStorage`: definisce se tutti gli stati devono essere archiviati o meno in memoria invece che su disco.
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: puntatore condiviso della classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer`: puntatore condiviso all'implementazione `ProtectionProfile::Observer`.
- `mip::ApplicationInfo applicationInfo`: oggetto. Usato per definire informazioni relative all'applicazione che sta utilizzando l'SDK.

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

#### <a name="store-state-in-memory-only"></a>Archiviare lo stato solo in memoria

```cpp
ProtectionProfile::Settings profileSettings(
    "",                                     //path to store settings
    true,                                   //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Leggere/scrivere le impostazioni del profilo dal percorso di archiviazione su disco

```cpp
ProtectionProfile::Settings profileSettings(
    "./mip_app_data",                       //path to store settings
    false,                                  //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

Usare poi il modello promise/future per caricare il `ProtectionProfile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<ProtectionProfile>>>();
auto profileFuture = profilePromise->get_future();
ProtectionProfile::LoadAsync(profileSettings, profilePromise);
```

Se fosse stato caricato un profilo e tale operazione fosse stata completata correttamente (`ProtectionProfileObserverImpl::OnLoadSuccess`), verrebbe chiamata l'implementazione di `mip::ProtectionProfile::Observer::OnLoadSuccess`. L'oggetto risultante o il puntatore dell'eccezione, nonché il contesto, vengono passati come parametri alla funzione. Il contesto è un puntatore a `std::promise` creato per gestire l'operazione asincrona. La funzione imposta semplicemente il valore della promessa sull'oggetto ProtectionProfile (contesto). Quando la funzione main usa `Future.get()`, il risultato può essere archiviato in un nuovo oggetto.

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>Riepilogo

Dopo aver completato l'implementazione degli osservatori e del delegato di autenticazione, è ora possibile caricare completamente un profilo. Il frammento di codice riportato di seguito presuppone che tutte le intestazioni necessarie siano già incluse.

```cpp
int main()
{
    const string userName = "MyTestUser@contoso.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    ProtectionProfile::Settings profileSettings("",
        false,
        authDelegateImpl,
        std::make_shared<ConsentDelegateImpl>(),
        std::make_shared<ProfileObserver>(),
        mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Il risultato finale è il caricamento corretto del profilo e l'archiviazione nell'oggetto denominato `profile`.

## <a name="next-steps"></a>Passaggi successivi

Ora che il profilo è stato aggiunto, il passaggio successivo consiste nell'aggiungere un motore al profilo.

[Concetti relativi al motore di protezione](concept-profile-engine-protection-engine-cpp.md)