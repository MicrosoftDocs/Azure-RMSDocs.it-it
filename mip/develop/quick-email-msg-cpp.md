---
title: API File - Elaborare file con estensione msg di posta elettronica (C++)
description: Le informazioni in questo articolo sono utili per comprendere come usare l'API File di MIP SDK per elaborare i file con estensione msg (C++).
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: b070a8ef35ff1bb71a6a87b19621f347626ef085
ms.sourcegitcommit: 437057990372948c9435b620052a7398360264b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2020
ms.locfileid: "97701612"
---
# <a name="file-api---process-email-msg-files-c"></a>API File - Elaborare file con estensione msg di posta elettronica (C++)

L'API File supporta operazioni di protezione per i file con estensione msg in modo identico a qualsiasi altro tipo di file, ad eccezione del fatto che l'SDK richiede che l'applicazione abiliti il flag di funzionalità MSG. In questo articolo verrà spiegato come impostare questo flag.

Come illustrato in precedenza, la creazione di un'istanza di `mip::FileEngine` richiede l'oggetto impostazione `mip::FileEngineSettings`. È possibile usare FileEngineSettings per passare i parametri per le impostazioni personalizzate che l'applicazione deve impostare per una particolare istanza. La proprietà `CustomSettings` di `mip::FileEngineSettings` viene usata per impostare il flag per `enable_msg_file_type` per abilitare l'elaborazione dei file con estensione msg.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Inizializzazione dell'applicazione API File (C++)](quick-app-initialization-cpp.md) per creare una soluzione Visual Studio iniziale. Questa guida di avvio rapido "Procedura - Elaborazione dei file con estensione msg dei messaggi di posta elettronica (C++)" si basa su quella precedente.
- Vedere [Avvio rapido: Elencare le etichette di riservatezza (C#)](quick-file-list-labels-cpp.md).
- Vedere [Avvio rapido: Impostare/ottenere etichette di riservatezza (C#)](quick-file-set-get-label-cpp.md).
- Vedere i concetti relativi ai [file di posta elettronica in MIP SDK](concept-email.md).
- Facoltativamente: vedere i concetti relativi ai [motori di file in MIP SDK](concept-profile-engine-file-engine-cpp.md).
- Facoltativamente: rivedere i concetti esposti in [Gestori di file in MIP SDK](concept-handler-file-cpp.md).

## <a name="prerequisite-implementation-steps"></a>Passaggi di implementazione richiesti come prerequisito

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Inizializzazione dell'applicazione client (C++)".

2. Creare uno script di PowerShell per generare token di accesso come illustrato nella guida di avvio rapido "[Elencare le etichette di riservatezza (C++)](quick-file-list-labels-cpp.md#create-a-powershell-script-to-generate-access-tokens)".

3. Implementare la classe observer per monitorare `mip::FileHandler` come illustrato nella guida di avvio rapido "[Impostare/ottenere etichette di riservatezza (C++)](quick-file-set-get-label-cpp.md#implement-an-observer-class-to-monitor-the-file-handler-object)".

## <a name="set-enable_msg_file_type-and-use-file-api-to-protect-msg-file"></a>Impostare enable_msg_file_type e usare l'API File per proteggere il file con estensione msg

Aggiungere il codice di costruzione del motore di file seguente per impostare `enable_msg_file_type flag` e usare il motore di file per proteggere un file con estensione msg.

1. Usare *Esplora soluzioni* per aprire il file con estensione cpp nel progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Aggiungere le direttive #include e using seguenti sotto le direttive esistenti corrispondenti, nella parte superiore del file:

    ```cpp
    #include "filehandler_observer.h" 
    #include "mip/file/file_handler.h" 
    #include <iostream>
    #include "mip/protection/protection_descriptor_builder.h"
    #include "mip/protection_descriptor.h"
    using mip::FileHandler;
    using mip::ProtectionDescriptor;
    using mip::ProtectionDescriptorBuilder;
    using mip::ProtectionSettings;
    using std::endl;
    ```

3. Rimuovere l'implementazione della funzione `main()` dalla guida di avvio rapido precedente. Inserire il codice seguente all'interno del corpo di `main()`. Nel blocco di codice seguente il flag `enable_msg_file_type` viene impostato durante la creazione del motore di file e un file con estensione msg può quindi essere elaborato dagli oggetti `mip::FileHandler` creati usando il motore di file.

```cpp
int main()
{
    // Construct/initialize objects required by the application's profile object
    ApplicationInfo appInfo { "<application-id>",                    // ApplicationInfo object (App ID, name, version)
                              "<application-name>", 
                              "1.0" 
    };

    auto mipContext = mip::MipContext::Create(appInfo,
                                                "file_sample",
                                                mip::LogLevel::Trace,
                                                false,
                                                nullptr /*loggerDelegateOverride*/,
                                                nullptr /*telemetryOverride*/);

    auto profileObserver = make_shared<ProfileObserver>();                      // Observer object
    auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>");  // Authentication delegate object (App ID)
    auto consentDelegateImpl = make_shared<ConsentDelegateImpl>();              // Consent delegate object

    // Construct/initialize profile object
    FileProfile::Settings profileSettings(mipContext,mip::CacheStorageType::OnDisk,authDelegateImpl,
        consentDelegateImpl,profileObserver);

    // Set up promise/future connection for async profile operations; load profile asynchronously
    auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
    auto profileFuture = profilePromise->get_future();
    try
    {
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
        std::cout << "An exception occurred. Are the Settings and ApplicationInfo objects populated correctly?\n\n"<< e.what() << "'\n";
        system("pause");
        return 1;
    }

    auto profile = profileFuture.get();

    // Construct/initialize engine object
    FileEngine::Settings engineSettings(
                            mip::Identity("<engine-account>"),      // Engine identity (account used for authentication)
                            "<engine-state>",                       // User-defined engine state
                            "en-US");                               // Locale (default = en-US)

    //Set enamble_msg_file_type flag as true
    std::vector<std::pair<string, string>> customSettings;
    customSettings.emplace_back(mip::GetCustomSettingEnableMsgFileType(), "true");
    engineSettings.SetCustomSettings(customSettings);

    // Set up promise/future connection for async engine operations; add engine to profile asynchronously
    auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
    auto engineFuture = enginePromise->get_future();
    profile->AddEngineAsync(engineSettings, enginePromise);
    std::shared_ptr<FileEngine> engine;

    try
    {
        engine = engineFuture.get();
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... is the access token incorrect/expired?\n\n"<< e.what() << "'\n";
        system("pause");
        return 1;
    }

    //Set file paths
    string inputFilePath = "<input-file-path>"; //.msg file to be protected
    string actualFilePath = inputFilePath;
    string outputFilePath = "<output-file-path>"; //protected .msg file
    string actualOutputFilePath = outputFilePath;

    //Create a file handler for original file
    auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto handlerFuture = handlerPromise->get_future();

    engine->CreateFileHandlerAsync(inputFilePath,
                                    actualFilePath,
                                    true,
                                    std::make_shared<FileHandlerObserver>(),
                                    handlerPromise);

    auto fileHandler = handlerFuture.get();

    //List templates available to the user and use one of them to protect the mail file.

    ///Listing of protection templates must be performed by creating protection engine as described in protection quick start

    string templateId = "<template-id>"; //protection template retrieved using protection engine

    //Create a protection descriptor using templateID and use it to set protection to the file
    auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
    const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();
    fileHandler->SetProtection(descriptor, ProtectionSettings());

    // Commit changes, save as outputFilePath
    auto commitPromise = std::make_shared<std::promise<bool>>();
    auto commitFuture = commitPromise->get_future();
    fileHandler->CommitAsync(outputFilePath, commitPromise);
    if (commitFuture.get()) {
        cout << "\n Protection applied to file: " << outputFilePath << endl;
    }
    else {
        cout << "Failed to protect: " + outputFilePath << endl;
        return 1;
    }

    // Create a new handler to read the protected file metadata
    auto protectedHandlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto protectedHandlerFuture = protectedHandlerPromise->get_future();
    engine->CreateFileHandlerAsync(outputFilePath, 
                                   actualOutputFilePath, 
                                   true, 
                                   std::make_shared<FileHandlerObserver>(), 
                                   protectedHandlerPromise);

    auto protectedFileHandler = protectedHandlerFuture.get();

    cout << "Original file: " << inputFilePath << endl;
    cout << "Protected file: " << outputFilePath << endl;
    cout << "TemplateID applied to protected file : " 
            << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetTemplateId() 
            << endl;
    cout << "Protection Owner of protected file : " 
            << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetOwner() 
            << endl;

    // Application shutdown. Null out profile and engine, call ReleaseAllResources();
    // Application may crash at shutdown if resources aren't properly released.
    protectedFileHandler = nullptr;
    fileHandler = nullptr;
    engine = nullptr;
    profile = nullptr;
    mipContext = nullptr;

    return 0;
}
```

Per altri dettagli sulle operazioni sui file, vedere i [concetti relativi al gestore di file](concept-handler-file-cpp.md).

4. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<application-id\> | ID applicazione registrato nel tenant Azure AD, ad esempio: `0edbblll-8773-44de-b87c-b8c6276d41eb`. |
   | \<engine-account\> | Account usato per l'identità del motore, ad esempio: `user@tenant.onmicrosoft.com`. |
   | \<engine-state\> | Stato dell'applicazione definito dall'utente, ad esempio: `My engine state`. |
   | \<input-file-path\> | Percorso completo di un file di messaggio di input di prova, ad esempio: `c:\\Test\\message.msg`. |
   | \<output-file-path\> | Percorso completo del file di output, che è una copia con etichetta del file di input, ad esempio: `c:\\Test\\message_protected.msg`. |
   | \<template-id\> | TemplateId recuperato usando il motore di protezione, ad esempio: `667466bf-a01b-4b0a-8bbf-a79a3d96f720`. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Usare **F6** (Compila soluzione) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere **F5** (Avvia debug) per eseguire l'applicazione.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione dell'applicazione C#

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| TemplateNotFoundException | Unrecognized template ID (ID modello non riconosciuto), CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad, CorrelationId.Description=FileHandler, HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689;78538a57-a9fd-4717-8924-33581a04598b| Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il templateID non sia valido. Tornare al blocco di codice e correggere l'ID del modello di protezione, quindi ricompilare e rieseguire il test. |