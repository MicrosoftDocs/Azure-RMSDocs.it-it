---
title: Concetti - Oggetto profilo dell'API File
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto profilo dell'API File, che viene creato durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: f174225ee7399480c610b491819c434400548e22
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555297"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al profilo dell'API File

Il profilo è la classe radice per tutte le operazioni in MIP SDK. Prima di usare qualsiasi funzionalità dell'API File, è necessario creare un `FileProfile` e tutte le operazioni future verranno eseguite dal profilo o da altri oggetti *aggiunti* al profilo.

Esistono alcuni prerequisiti per il codice che devono essere soddisfatti prima di tentare di creare un'istanza di un profilo:

- `MipContext` è stato creato e archiviato in un oggetto accessibile all'oggetto `mip::FileProfile`.
- `AuthDelegateImpl` implementa `mip::AuthDelegate`.
- `ConsentDelegateImpl` implementa `mip::ConsentDelegate`.
- [Registrazione dell'applicazione in Azure Active Directory](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) e ID client hardcoded nei file di configurazione o dell'applicazione.
- Implementazione appropriata di una classe che eredita `mip::FileProfile::Observer`.

## <a name="load-a-profile"></a>Caricare un profilo

Dopo aver definito `ProfileObserver`, `ConsentDelegateImpl` e `AuthDelegateImpl`, è ora possibile creare un'istanza di `mip::FileProfile`. Per creare l'oggetto `mip::FileProfile` è necessario che [`mip::MipContext`] disponga di e [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) per archiviare tutte le informazioni sulle impostazioni relative al `FileProfile`.

### <a name="fileprofilesettings-parameters"></a>Parametri di FileProfile::Settings

Il costruttore `FileProfile::Settings` accetta cinque parametri, elencati di seguito:

- `std::shared_ptr<MipContext>`: oggetto `mip::MipContext` inizializzato per archiviare le informazioni sull'applicazione, il percorso di stato e così via.
- `mip::CacheStorageType`: definisce come archiviare lo stato: in memoria, su disco o su disco e crittografato.
- `std::shared_ptr<mip::AuthDelegate>`: puntatore condiviso della classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::ConsentDelegate>`: puntatore condiviso della classe [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md).
- `std::shared_ptr<mip::FileProfile::Observer> observer`: un puntatore condiviso all'implementazione del `Observer` del profilo (in [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)e [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

Gli esempi seguenti mostrano come creare l'oggetto `profileSettings` usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

#### <a name="store-state-in-memory-only"></a>Archiviare lo stato solo in memoria

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

FileProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),      // new consent delegate
    std::make_shared<FileProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Leggere/scrivere le impostazioni del profilo dal percorso di archiviazione su disco

Il frammento di codice seguente indicherà a `FileProfile` di archiviare tutti i dati sullo stato dell'app in `./mip_app_data`.

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

FileProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
    std::make_shared<FileProfileObserverImpl>());  // new protection profile observer
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
    const string userName = "MyTestUser@contoso.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    FileProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
        std::make_shared<FileProfileObserverImpl>());  // new file profile observer

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
