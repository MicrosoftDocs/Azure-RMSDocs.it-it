---
# required metadata

title: Procedura&#58; Abilitare la registrazione delle prestazioni e dell'errore | Azure RMS
description: Microsoft Rights Management SDK 4.2 gestisce i log delle diagnosi e delle prestazioni caricati tramite una proprietà a dispositivo singolo.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedura: Abilitare la registrazione delle prestazioni e dell'errore
Microsoft Rights Management SDK 4.2 gestisce i log delle diagnosi e delle prestazioni caricati tramite una proprietà a dispositivo singolo.

## Panoramica ##
È possibile migliorare l'esperienza degli utenti e la risoluzione dei problemi, consentendo il caricamento automatico delle registrazioni di diagnostica e delle prestazioni in Microsoft. Per rispettare la privacy degli utenti, lo sviluppatore dell'app deve chiedere il consenso all'utente prima di abilitare la registrazione automatica.

Il controllo della registrazione viene gestito tramite due proprietà.

-   Abilitare la registrazione tramite la proprietà **IpcCustomerExperienceDataCollectionEnabled**. L'impostazione viene mantenuta anche in seguito alla reimpostazione dei dispositivi.
-   Controllare il livello di registrazione tramite la proprietà **IpcLogLevel** usando le impostazioni seguenti.

    * 1 - Dettagli
    * 2 - Informazioni
    * 3 - Avviso
    * 4 - Errore
    * 5 - Critico

In ognuno dei frammenti di codice di esempio seguenti, l'applicazione chiamante può impostare o eseguire una query sulla proprietà.

### Android ###
Abilitare la registrazione automatica

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Ottenere l'impostazione del flag di controllo della registrazione corrente

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
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
 

## Windows ##
Abilitare la registrazione automatica

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Per altre informazioni sulle impostazioni facoltative, vedere [CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions).

Ottenere l'impostazione del flag di controllo della registrazione corrente

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Nota**: i frammenti di codice Windows precedenti sono in C++. Per C\#, aggiornare la sintassi con '.' al posto di '::'.

**Linux/C++**: questo SDK include alcune registrazioni di base meno ampie di quelle delle altre piattaforme. Per altre informazioni, vedere la sezione **Risoluzione dei problemi** del file "README.md" in [RMS SDK per C++ portabile](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

 

 


<!--HONumber=Apr16_HO4-->


