---
title: Concetti-delega
description: Questo articolo consente di comprendere i concetti relativi alla delega in MIP SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 848b0752f6158ade4fd61b562163e2e641454773
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225022"
---
# <a name="concept---delegation-in-the-mip-sdk"></a>Concetto-delega nell'SDK MIP

Microsoft Information Protection SDK fornisce due percorsi per le applicazioni basate su servizi per agire per conto di un altro utente. La delega può essere necessaria quando i file devono essere etichettati, protetti o utilizzati nel contesto di un'identità utente diversa dall'identità del servizio. Questa identità delegata può essere impostata a livello di **motore** o di **gestore** e la posizione in cui viene impostata dipenderà dal caso di utilizzo.

## <a name="engine-settings-based-delegation"></a>Delega basata sulle impostazioni del motore

L'SDK MIP supporta la fornitura di un indirizzo di posta elettronica dell'utente delegato nell'oggetto impostazioni per tutti gli SDK. File, protezione e criteri. Questa operazione viene eseguita impostando la `DelegatedUserEmail` proprietà sull'oggetto Settings. Il risultato è che il motore inizializzato con l'oggetto impostazioni eseguirà **tutte le operazioni MIP** come se l'utente fosse stato fornito alla `DelegatedUserEmail` Proprietà. Verranno recuperati i criteri per l'utente specifico e tutte le operazioni di protezione verranno eseguite come tale utente, incluso il proprietario dei file protetti.

Questo modello è utile quando l'applicazione basata su servizi deve funzionare completamente come l'utente; il criterio deve essere recuperato solo per l'utente specificato ed è necessario eseguire tutte le operazioni di decrittografia nel contesto dell'identità utente. Quando si crea questo motore, è importante che l'applicazione specifichi un ID di motore univoco per tale utente, spesso l'indirizzo di posta elettronica. In questo modo si garantisce che vengano realizzati i vantaggi della memorizzazione nella cache. Se non viene specificato un ID di motore univoco, è possibile che si verifichino scarse prestazioni dell'applicazione.

### <a name="file-sdk"></a>SDK file

Nell'esempio seguente viene illustrato come impostare l'identità delegata per un'applicazione di file SDK in C++ e C#. Lo stesso modello può essere usato per l'SDK dei criteri.

Questo esempio illustra come creare un **motore di delegati** in file SDK in .NET.

```csharp
// C# Example for creating a delegated file engine
string delegatedUserEmail = "alice@contoso.com";
var engineSettings = new PolicyEngineSettings(delegatedUserEmail, authDelegate, "", "en-US")
{
    // Provide the identity for service discovery.
    Identity = identity,
    // Set the identity for which all MIP operations will be performed.
    DelegatedUserEmail = delegatedUserEmail
};

var engine = Task.Run(async () => await profile.AddEngineAsync(engineSettings)).Result;
```

Questo esempio illustra come creare un **motore di delegati** in file SDK in C++.

```c++
// C++ Example for creating a delegated file engine
std::string delegatedUserEmail = "alice@contoso.com";
FileEngine::Settings engineSettings(delegatedUserEmail, mAuthDelegate, "", "en-US", false);
// Set the identity for which all MIP operations will be performed. 
engineSettings.SetDelegatedUserEmail(delegatedUserEmail);

auto enginePromise = std::make_shared<std::promise<std::shared_ptr<FileEngine>>>();
auto engineFuture = enginePromise->get_future();

mProfile->AddEngineAsync(engineSettings, enginePromise);
mEngine = engineFuture.get();
```

Il risultato è che tutti i motori di file verranno creati per conto dell'utente specificato.


## <a name="handler-based-delegation"></a>Delega basata sul gestore

Negli scenari in cui è necessario solo **proteggere** i file nel contesto di un'identità utente specifica, `FileHandler` fornisce un metodo per passare l'identità utente tramite un `ProtectionSettings` oggetto. Il criterio e le eventuali operazioni di decrittografia verranno eseguite come identità del **servizio** autenticato. L'azione di protezione verrà eseguita per conto dell'utente specificato. tale utente sarà il **proprietario** della protezione MIP nel documento.

### <a name="file-sdk"></a>SDK file

Solo l'operazione di applicazione della protezione diretta o tramite etichetta verrà eseguita come l'utente fornito all' `ProtectionSettings` oggetto. Questo oggetto viene passato alle `SetLabel()` `SetProtection()` funzioni o in file SDK.

Questo esempio illustra come eseguire un' **operazione di protezione del delegato** in file SDK in .NET.

```csharp
string delegatedUserEmail = "bob@contoso.com";
ProtectionSettings protectionSettings = new ProtectionSettings()
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, protectionSettings);
// Similar pattern for SetProtection()
// handler.SetProtection(protectionDescriptor, protectionSettings);
```

Questo esempio illustra come eseguire un' **operazione di protezione del delegato** in file SDK in C++.

```c++
mip::ProtectionSettings protectionSettings;
// Set the delegated mail address 
protectionSettings.SetDelegatedUserEmail(delegatedUserEmail);
handler->SetLabel(mEngine->GetLabelById(labelId), labelingOptions, protectionSettings);
```

Il risultato è che tutte le operazioni di **scrittura** del gestore in cui viene applicata la protezione verranno eseguite come utente delegato. 

### <a name="protection-sdk"></a>SDK di protezione

L'SDK di protezione funziona in modo diverso rispetto a file SDK. Esistono **due tipi di gestori** che è possibile creare, uno per la pubblicazione e uno per l'utilizzo. Analogamente a file SDK, l'indirizzo di posta delegata viene impostato tramite l'oggetto Settings per ogni tipo di gestore.

#### <a name="net"></a>.NET

In questo esempio viene illustrato come eseguire la **pubblicazione delegata**.

```csharp
string delegatedUserEmail = "bob@contoso.com";
PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor)
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};          
var protectionHandler = engine.CreateProtectionHandlerForPublishing(publishingSettings);
```

In questo esempio viene illustrato come eseguire l' **utilizzo delegato**.

```csharp
string delegatedUserEmail = "bob@contoso.com";
ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo)
{                
    ContentName = "A few bytes.",
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
var protectionHandler = engine.CreateProtectionHandlerForConsumption(consumptionSettings);
```

#### <a name="c"></a>C++

In questo esempio viene illustrato come eseguire l' **utilizzo delegato**.

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);
// Set the delegated mail address 
publishingSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

In questo esempio viene illustrato come eseguire la **pubblicazione delegata**.

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
// Set the delegated mail address 
consumptionSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

## <a name="required-permissions"></a>Autorizzazioni necessarie

Ogni scenario precedente richiede un set di autorizzazioni diverso. 

| Scenario                             | Autorizzazione necessaria                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| Motore delegato di file SDK            | UnifiedPolicy. tenant. Read<br>Content. DelegatedReader<br>Content. DelegatedWriter |
| Motore delegato di policy SDK          | UnifiedPolicy. tenant. Read                                                       |
| Gestore delegato di file SDK           | Content. DelegatedWriter                                                         |
| Pubblicazione delegata di Protection SDK     | Content. DelegatedWriter                                                         |
| Utilizzo delegato di Protection SDK | Content. DelegatedReader                                                         |

Per una verifica completa delle autorizzazioni e per dove impostarle, esaminare [le autorizzazioni API per Microsoft Information Protection SDK](concept-api-permissions.md) .

## <a name="next-steps"></a>Passaggi successivi

- Esaminare le [autorizzazioni API per Microsoft Information Protection SDK](concept-api-permissions.md)
- Esaminare il <TODO> ref aggiungere un'entità servizio per l'autenticazione.