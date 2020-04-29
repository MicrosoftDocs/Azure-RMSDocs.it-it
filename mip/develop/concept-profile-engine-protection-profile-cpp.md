---
title: Concetti - Oggetto profilo dell'API Protezione
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto profilo dell'API Protezione, che viene creato durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 7d6dded96c3d87cdbf925f85c675c10a68f182fb
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764039"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al profilo dell'API Protezione

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. 

## <a name="load-a-profile"></a>Caricare un profilo

Ora che `ProtectionProfileObserverImpl` è definito, verrà usato per creare un'istanza `mip::ProtectionProfile`. Per creare `mip::ProtectionProfile` l'oggetto [`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md)è necessario.

### <a name="protectionprofilesettings-parameters"></a>Parametri ProtectionProfile::Settings

- `std::shared_ptr<MipContext>`: Oggetto `mip::MipContext` inizializzato per archiviare le informazioni sull'applicazione, il percorso di stato e così via.
- `mip::CacheStorageType`: Definisce come archiviare lo stato: in memoria, su disco o su disco e crittografato.
- `std::shared_ptr<mip::ConsentDelegate>`: Puntatore condiviso della classe [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md).
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer`: Puntatore condiviso all'implementazione del profilo `Observer` (in [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)e [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. 

#### <a name="store-state-in-memory-only"></a>Archiviare lo stato solo in memoria

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

ProtectionProfile::Settings profileSettings(
    mipContext,                                        // mipContext object
    mip::CacheStorageType::InMemory,                   // use in memory storage    
    std::make_shared<ConsentDelegateImpl>(),           // new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Leggere/scrivere le impostazioni del profilo dal percorso di archiviazione su disco

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

ProtectionProfile::Settings profileSettings(
    mipContext,                                         // mipContext object
    mip::CacheStorageType::OnDisk,                      // use on disk storage    
    std::make_shared<ConsentDelegateImpl>(),            // new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>()); // new protection profile
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

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    ProtectionProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage        
        std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
        std::make_shared<ProfileObserver>());          // new protection profile observer

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
