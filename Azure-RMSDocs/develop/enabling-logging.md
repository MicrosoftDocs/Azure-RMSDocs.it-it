---
title: Procedura&#58; Abilitare la registrazione delle prestazioni e dell'errore | Azure RMS
description: Microsoft Rights Management SDK 4.2 gestisce i log delle diagnosi e delle prestazioni caricati tramite una proprietà a dispositivo singolo.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 23f4eda077a4f3749097e0f34013d5a831e6cb2f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255377"
---
# <a name="how-to-enable-error-and-performance-logging"></a>Come fare per: Abilitare la registrazione delle prestazioni e degli errori
Microsoft Rights Management SDK 4.2 gestisce i log delle diagnosi e delle prestazioni caricati tramite una proprietà a dispositivo singolo.

## <a name="overview"></a>Panoramica ##
È possibile migliorare l'esperienza degli utenti e la risoluzione dei problemi abilitando il caricamento automatico dei dati delle registrazioni della diagnostica, delle prestazioni e della telemetria in Microsoft. 

> [!IMPORTANT] 
> Per rispettare la privacy degli utenti, lo sviluppatore dell'app deve chiedere il consenso all'utente prima di abilitare la registrazione automatica.

> [!NOTE]
> Come esempio, ecco un messaggio standard usato da Microsoft per la notifica di registrazione: 
>
> *Attivando la registrazione degli errori e delle prestazioni, l’utente accetta l'invio di tali dati a Microsoft.  Microsoft raccoglie i dati sugli errori e sulle prestazioni tramite Internet ("Dati").  Microsoft usa questi dati per offrire e migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi Microsoft.  Vengono analizzate, ad esempio, prestazioni e affidabilità quali le funzionalità usate dagli utenti, la velocità di risposta delle funzionalità, le prestazioni del dispositivo, le interazioni con l'interfaccia utente e tutti i problemi che possono verificarsi durante l'uso del prodotto.  I Dati includono anche informazioni sulla configurazione del software, ad esempio la versione in esecuzione e l'indirizzo IP.*  

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

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Ottenere l'impostazione del flag di controllo della registrazione corrente

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## <a name="ios"></a>iOS ##
Abilitare la registrazione automatica

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

Ottenere l'impostazione del flag di controllo della registrazione corrente

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

Impostare il controllo a livello di log

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

Ottenere l'impostazione del controllo a livello di log

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## <a name="windows"></a>Windows ##
Abilitare la registrazione automatica

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Per altre informazioni sulle impostazioni facoltative, vedere [CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx).

Ottenere l'impostazione del flag di controllo della registrazione corrente

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Nota**: i frammenti di codice Windows precedenti sono in C++. Per C\#, aggiornare la sintassi con '.' al posto di '::'.

**Linux/C++**: questo SDK include alcune registrazioni di base meno ampie di quelle delle altre piattaforme. Per altre informazioni, vedere la sezione **Risoluzione dei problemi** del file "README.md" in [RMS SDK per C++ portabile](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).
