---
title: Avvio rapido - Protezione del server AD RMS
description: Argomento di avvio rapido che illustra come configurare MIP SDK per usare il server AD RMS (Active Directory Rights Management Server)
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/17/2019
ms.author: tommos
ms.openlocfilehash: eafcf65b9478cc8a2d2c104c3e98194c40e9c941
ms.sourcegitcommit: 80d7c1a1afb3e54fac434f10a7dca4f8076384a8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82255606"
---
# <a name="quickstart-active-directory-rights-management-server-ad-rms-protection"></a>Guida introduttiva: Protezione del server AD RMS (Active Directory Rights Management Server)

Questo argomento di avvio rapido illustra come implementare il supporto per il server AD RMS (Active Directory Rights Management Server) usando MIP SDK.

> [!NOTE]
> I passaggi descritti in questo argomento di avvio rapido si applicano solo all'API File per C# o C++ e all'API di protezione solo per C++.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, assicurarsi di:

- In primo luogo completare [Avvio rapido: Inizializzazione delle applicazioni client (C++)](quick-app-initialization-cpp.md) per creare una soluzione Visual Studio iniziale.
- In primo luogo completare [Avvio rapido: Elencare le etichette di riservatezza (C++)](quick-file-list-labels-cpp.md) o [Avvio rapido: Elencare le etichette di riservatezza (C#)](quick-file-list-labels-csharp.md)
- Distribuire AD RMS con l'[estensione per dispositivi mobili](https://docs.microsoft.com/en-us/azure/information-protection/active-directory-rights-manage-mobile-device).
- Facoltativamente, assicurarsi che il [record SRV DNS per l'estensione per dispositivi mobili di AD RMS](https://docs.microsoft.com/en-us/azure/information-protection/active-directory-rights-manage-mobile-device#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension) sia pubblicato.

## <a name="service-discovery"></a>Individuazione dei servizi

L'SDK esegue l'individuazione dei servizi in base all'elemento `mip::Identity` fornito tramite `FileEngineSettings` o `ProtectionEngineSettings` usando il suffisso UPN o dell'indirizzo di posta. Prima di tutto cerca nella gerarchia di domini il record *_rmsdisco* per l'estensione per dispositivi mobili. Per altri dettagli su tale processo, vedere [Specifica del record SRV DNS per l'estensione per dispositivi mobili di AD RMS](https://docs.microsoft.com/en-us/azure/information-protection/active-directory-rights-manage-mobile-device#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension). Se tale record SRV DNS non viene trovato, per impostazione predefinita usa il servizio Azure Information Protection come posizione del servizio.

Se un'identità non è disponibile o se il record SRV DNS per l'estensione per dispositivi mobili non è stato pubblicato, è possibile eseguire l'override del processo di individuazione dei servizi impostando in modo esplicito l'[URL dell'endpoint cloud](https://docs.microsoft.com/information-protection/develop/reference/class_mip_fileengine_settings#setpolicycloudendpointbaseurl-function).

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>Configurazione dell'API File in C# per usare AD RMS

Sono necessarie due modifiche secondarie se l'applicazione usa Active Directory Authentication Library (ADAL) e l'API File in C#. L'oggetto `FileEngineSettings` e il costruttore `AuthenticationContext` devono essere aggiornati per funzionare con AD RMS e Active Directory Federations Services (ADFS).

Se è stato distribuito il record SRV DNS per l'estensione per dispositivi mobili e si prevede di passare un indirizzo di posta elettronica o un nome dell'entità utente, [seguire le istruzioni per usare un'identità](#update-the-file-engine-settings-to-use-ad-rms-with-an-identity).

Se il record SRV DNS per l'estensione per dispositivi mobili non è disponibile o non sarà disponibile un'identità in fase di esecuzione, [seguire le istruzioni per l'endpoint esplicito](#update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint).

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-identity"></a>Aggiornare le impostazioni del motore di file per usare AD RMS con un'identità

Se il record SRV DNS per l'estensione per dispositivi mobili è stato pubblicato e `Microsoft.InformationProtection.Identity` è stato fornito come parte delle impostazioni del motore, la sola modifica necessaria nel codice consiste nell'impostare `FileEngineSettings.ProtectionOnlyEngine = true`. È necessario impostare questa proprietà perché le operazioni di assegnazione di etichette (criteri) non sono supportate per gli endpoint di protezione di AD RMS.

```csharp
// Configure FileEngineSettings as protection only engine.
var engineSettings = new FileEngineSettings("", authDelegate, "", "en-US")
{
     // Provide the identity for service discovery.
     Identity = identity,
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true
};
```

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint"></a>Aggiornare le impostazioni del motore di file per usare AD RMS con un endpoint esplicito

Se il record SRV DNS per l'estensione per dispositivi mobili non è stato pubblicato o `Microsoft.InformationProtection.Identity` non è disponibile per il passaggio quando si crea `FileEngine`, è necessario apportare due modifiche al codice. Una consiste nell'impostare `FileEngineSettings.ProtectionOnlyEngine = true`. Questa proprietà deve essere impostata perché le operazioni di assegnazione di etichette (criteri) non sono supportate per gli endpoint di protezione di AD RMS.

```csharp
// Configure FileEngineSettings as protection only engine and generate a unique engine id.
var engineSettings = new FileEngineSettings("", authDelegate, "", "en-US")
{
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true,
     // Provide the explicit AD RMS endpoint
     ProtectionCloudEndpointBaseUrl = "https://rms.contoso.com"
};
```

### <a name="update-the-authentication-delegate"></a>Aggiornare il delegato di autenticazione

Se si usa ADAL nell'applicazione .NET, sarà necessario apportare una modifica all'implementazione `Microsoft.InformationProtection.AuthDelegate` per disabilitare la convalida dell'autorità. Disabilitare la convalida dell'autorità impostando `validateAuthority` nel costruttore `AuthenticationContext` su **false**.

   ```csharp
   AuthenticationContext authContext = new AuthenticationContext(authority, false, tokenCache);
   ```

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>Configurazione dell'API File in C++ per usare AD RMS

Se è stato distribuito il record SRV DNS per l'estensione per dispositivi mobili e si prevede di passare un indirizzo di posta elettronica o un nome dell'entità utente, [seguire le istruzioni per usare un'identità](#update-the-fileenginesettings-to-use-ad-rms-with-an-identity).

Se il record SRV DNS per l'estensione per dispositivi mobili non è disponibile o non sarà disponibile un'identità in fase di esecuzione, [seguire le istruzioni per l'endpoint esplicito](#update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint).

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-identity"></a>Aggiornare FileEngine::Settings per usare AD RMS con un'identità

Se il record SRV DNS per l'estensione per dispositivi mobili è stato pubblicato e `mip::Identity` viene fornito in `FileEngine::Settings`, l'unica azione consiste nell'impostare il motore su un motore di sola protezione.

```cpp
FileEngine::Settings engineSettings(mip::Identity(mUsername), "");
engineSettings.SetProtectionOnlyEngine = true;
```

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>Aggiornare FileEngine::Settings per usare AD RMS con un endpoint esplicito

Se il record SRV DNS per l'estensione per dispositivi mobili non è stato pubblicato o non è disponibile un'identità per l'individuazione dei servizi, il motore deve essere impostato solo sulla protezione e l'URL dell'endpoint cloud esplicito deve essere fornito tramite `SetProtectionCloudEndpointBaseUrl()`.

```cpp
FileEngine::Settings engineSettings("", authDelegate, "");
engineSettings.SetProtectionOnlyEngine = true;
engineSettings.SetProtectionCloudEndpointBaseUrl("https://rms.contoso.com");
```

## <a name="configuring-protection-api-in-c-to-use-ad-rms"></a>Configurazione dell'API di protezione in C++ per usare AD RMS

Se è stato distribuito il record SRV DNS per l'estensione per dispositivi mobili e si prevede di passare un indirizzo di posta elettronica o un nome dell'entità utente, [seguire le istruzioni per usare un'identità](#set-the-protectionenginesettings-to-use-ad-rms-with-an-identity).

Se il record SRV DNS per l'estensione per dispositivi mobili non è disponibile o non sarà disponibile un'identità in fase di esecuzione, [seguire le istruzioni per l'endpoint esplicito](#set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint).

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-identity"></a>Impostare ProtectionEngine::Settings per usare AD RMS con un'identità

Se il record SRV DNS per l'estensione per dispositivi mobili è stato pubblicato e un'identità è stata fornita in `ProtectionEngine::Settings`, non sono necessarie altre modifiche al codice per usare AD RMS. L'individuazione dei servizi troverà l'endpoint AD RMS e lo userà per le operazioni di protezione.

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity(mUsername), authDelegate, "");
```

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>Impostare ProtectionEngine::Settings per usare AD RMS con un endpoint esplicito

Se il record SRV DNS non è stato pubblicato o un'identità non è stata fornita in `ProtectionEngine::Settings`, l'URL dell'endpoint di protezione deve essere impostato in modo esplicito tramite `SetProtectionCloudEndpointBaseUrl()`.

```cpp
ProtectionEngine::Settings engineSettings("", authDelegate, "");
engineSettings.SetProtectionCloudEndpointBaseUrl("https://RMS.CONTOSO.COM");
```

## <a name="remove-or-comment-label-references"></a>Rimuovere o impostare come commento i riferimenti alle etichette

Se si compila l'applicazione da una delle guide di avvio rapido, si noterà che l'applicazione ha riferimenti alle etichette nel formato `fileEngine.SensitivityLabels` o `engine->ListSensitivityLabels();`. Poiché l'applicazione è stata impostata solo sulla protezione, questi blocchi di codice devono essere impostati come commento o rimossi perché l'esecuzione di tali blocchi genererà un'eccezione.

## <a name="next-steps"></a>Passaggi successivi

Ora che sono state apportate le modifiche per supportare AD RMS, l'applicazione può eseguire qualsiasi operazione di sola protezione usando il servizio AD RMS come provider di protezione.
