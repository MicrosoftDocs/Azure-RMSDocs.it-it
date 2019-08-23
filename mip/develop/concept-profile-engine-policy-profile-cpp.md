---
title: Concetti - Oggetto profilo dell'API Criteri
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto profilo dell'API Criteri, che viene creato durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 9b3b32464cae35560c74a05b28506ca60dc963d2
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886044"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al profilo dell'API Criteri

`mip::Profile` deve essere caricato prima di poter eseguire qualsiasi operazione dell'API Criteri.

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

## <a name="load-a-profile"></a>Caricare un profilo

Ora che gli `MipContext`elementi `ProfileObserver`, e `AuthDelegateImpl` sono definiti, verranno usati per creare un'istanza `mip::PolicyProfile`. Per creare `mip::PolicyProfile` l'oggetto [`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md) sono `mip::MipContext`necessari e.

### <a name="profilesettings-parameters"></a>Parametri di Profile::Settings

Il `PolicyProfile::Settings` costruttore accetta quattro parametri, elencati di seguito:

- `const std::shared_ptr<MipContext>`: Oggetto `mip::MipContext` inizializzato per archiviare le informazioni sull'applicazione, il percorso di stato e così via.
- `mip::CacheStorageType`: Definisce come archiviare lo stato: In memoria, su disco o su disco e crittografato. Per informazioni dettagliate, vedere [concetti relativi all'archiviazione della cache](concept-cache-storage.md).
- `std::shared_ptr<mip::AuthDelegate>`: Puntatore condiviso della classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`: Puntatore condiviso all'implementazione del profilo `Observer` (in [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)e [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

#### <a name="store-state-in-memory-only"></a>Archiviare lo stato solo in memoria

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Leggere/scrivere le impostazioni del profilo dal percorso di archiviazione su disco

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer
```

Usare poi il modello promise/future per caricare il `Profile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<Profile>>>();
auto profileFuture = profilePromise->get_future();
Profile::LoadAsync(profileSettings, profilePromise);
```

Se un profilo è caricato correttamente, `ProfileObserver::OnLoadSuccess`, l'implementazione di `mip::Profile::Observer::OnLoadSuccess` riceve una notifica. L'oggetto risultante, in questo caso `mip::Profile`, nonché il contesto, vengono passati come parametri alla funzione dell'osservatore.

Il *contesto* è un puntatore a `std::promise` creato per gestire l'operazione asincrona. La funzione imposta semplicemente il valore della promessa sull'oggetto profilo passato per il primo parametro. Quando la funzione main usa `Future.get()`, il risultato può essere archiviato in un nuovo oggetto nel thread chiamante.

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

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    PolicyProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer

    auto profilePromise = std::make_shared<promise<shared_ptr<PolicyProfile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Il risultato finale è il caricamento corretto del profilo e l'archiviazione nell'oggetto denominato `profile`.

## <a name="next-steps"></a>Fasi successive

Ora che il profilo è stato aggiunto, il passaggio successivo consiste nell'aggiungere un motore al profilo.

[Concetti relativi al motore dei criteri](concept-profile-engine-policy-engine-cpp.md)
