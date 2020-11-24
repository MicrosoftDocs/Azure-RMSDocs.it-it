---
title: Procedura&#58; Abilitare la registrazione delle prestazioni e dell'errore | Azure RMS
description: Microsoft Rights Management SDK 4.2 gestisce i log delle diagnosi e delle prestazioni caricati tramite una proprietà a dispositivo singolo.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 4a9a0029cbf9d3d171b24fc7a20a146a4646f799
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95567956"
---
# <a name="how-to-enable-error-and-performance-logging"></a>Procedura: Abilitare la registrazione delle prestazioni e dell'errore
Microsoft Rights Management SDK 4.2 gestisce i log delle diagnosi e delle prestazioni caricati tramite una proprietà a dispositivo singolo.

## <a name="overview"></a>Panoramica ##
È possibile migliorare l'esperienza degli utenti e la risoluzione dei problemi abilitando il caricamento automatico dei dati delle registrazioni della diagnostica, delle prestazioni e della telemetria in Microsoft. 

> [!IMPORTANT] 
> Per rispettare la privacy degli utenti, lo sviluppatore dell'app deve chiedere il consenso all'utente prima di abilitare la registrazione automatica.

> [!NOTE]
> Come esempio, ecco un messaggio standard usato da Microsoft per la notifica di registrazione: 
>
> *Attivando la registrazione degli errori e delle prestazioni, si accetta di inviare i dati relativi a errori e prestazioni a Microsoft.  Microsoft raccoglierà i dati relativi a errori e prestazioni tramite Internet ("dati").  Microsoft usa questi dati per fornire e migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi Microsoft.  Si analizzino, ad esempio, le prestazioni e l'affidabilità, ad esempio le funzionalità usate, la velocità di risposta delle funzionalità, le prestazioni del dispositivo, le interazioni con l'interfaccia utente e tutti i problemi che si verificano con il prodotto.  I dati includono anche informazioni sulla configurazione del software, ad esempio il software attualmente in esecuzione e l'indirizzo IP.*  

Il controllo della registrazione viene gestito tramite due proprietà.

-   Abilitare la registrazione tramite la proprietà **IpcCustomerExperienceDataCollectionEnabled**. L'impostazione viene mantenuta anche in seguito alla reimpostazione dei dispositivi.
-   Controllare il livello di registrazione tramite la proprietà **IpcLogLevel** usando le impostazioni seguenti.

    * 1 - Dettagli
    * 2 - Informazioni
    * 3 - Avviso
    * 4 - Errore
    * 5 - Critico

In ognuno dei frammenti di codice di esempio seguenti, l'applicazione chiamante può impostare o eseguire una query sulla proprietà.

### <a name="android"></a>Android ###
Abilitare la registrazione automatica

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
SharedPreferences.Editor editor = preferences.edit();
editor.putBoolean("IpcCustomerExperienceDataCollectionEnabled", true);
editor.commit();
```

Ottenere l'impostazione del flag di controllo della registrazione corrente

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);
```

## <a name="ios"></a>iOS ##
Abilitare la registrazione automatica

```objectivec
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setBool:FALSE forKey:@"IpcCustomerExperienceDataCollectionEnabled"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

Ottenere l'impostazione del flag di controllo della registrazione corrente

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcCustomerExperienceDataCollectionEnabled"];
```

Impostare il controllo a livello di log

```java
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setInteger:1 forKey:@"IpcLogLevel"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

Ottenere l'impostazione del controllo a livello di log

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcLogLevel"];
```

## <a name="windows"></a>Windows ##
Abilitare la registrazione automatica

```cpp
CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;
```

Per altre informazioni sulle impostazioni facoltative, vedere [CustomerExperienceOptions](/previous-versions/windows/desktop/msipcthin2/customerexperienceoptions).

Ottenere l'impostazione del flag di controllo della registrazione corrente

```cpp
CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;
```

**Nota**: i frammenti di codice Windows precedenti sono in C++. Per C\#, aggiornare la sintassi con '.' al posto di '::'.

**Linux/C++**: questo SDK include alcune registrazioni di base meno ampie di quelle delle altre piattaforme. Per altre informazioni, vedere la sezione **Risoluzione dei problemi** del file "README.md" in [RMS SDK per C++ portabile](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).