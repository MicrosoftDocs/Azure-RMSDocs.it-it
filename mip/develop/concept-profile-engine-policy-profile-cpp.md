---
title: Concetti - Oggetto profilo dell'API Criteri
description: Questo articolo aiuterà a comprendere i concetti relativi all'oggetto profilo dell'API Criteri, che viene creato durante l'inizializzazione dell'applicazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b229148c3028f4478f83cbbc928e19666c2f44b5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445428"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Microsoft Information Protection SDK - Concetti relativi al profilo dell'API Criteri

`mip::Profile` deve essere caricato prima di poter eseguire qualsiasi operazione dell'API Criteri.

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

## <a name="load-a-profile"></a>Caricare un profilo

Dopo aver definito `ProfileObserver` e `AuthDelegateImpl`, verranno usati per creare un'istanza di `mip::PolicyProfile`. Per la creazione dell'oggetto `mip::PolicyProfile` è richiesto [`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md).

### <a name="profilesettings-parameters"></a>Parametri di Profile::Settings

- `std::string path`: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
- `bool useInMemoryStorage`: definisce se tutti gli stati devono essere archiviati o meno in memoria invece che su disco.
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: puntatore condiviso della classe `mip::AuthDelegate`. 
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`: puntatore condiviso all'implementazione `PolicyProfile::Observer`.
- `mip::ApplicationInfo applicationInfo`: oggetto. Usato per definire informazioni relative all'applicazione che sta utilizzando l'SDK.

I due esempi seguenti mostrano come creare l'oggetto profileSettings usando l'archiviazione locale o solo in memoria per l'archiviazione degli stati. Entrambi gli esempi partono dal presupposto che l'oggetto `authDelegateImpl` sia già stato creato.

#### <a name="store-state-in-memory-only"></a>Archiviare lo stato solo in memoria

```cpp
Profile::Settings profileSettings("",
    true,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Leggere/scrivere le impostazioni del profilo dal percorso di archiviazione su disco

```cpp
Profile::Settings profileSettings("./mip_app_data",
    false,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
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
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    Profile::Settings profileSettings("", false, authDelegateImpl, std::make_shared<ProfileObserver>(), mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<Profile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Il risultato finale è il caricamento corretto del profilo e l'archiviazione nell'oggetto denominato `profile`.

## <a name="next-steps"></a>Passaggi successivi

Ora che il profilo è stato aggiunto, il passaggio successivo consiste nell'aggiungere un motore al profilo.

[Concetti relativi al motore dei criteri](concept-profile-engine-policy-engine-cpp.md)