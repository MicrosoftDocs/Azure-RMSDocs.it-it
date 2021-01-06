---
title: API File - Elaborare file con estensione msg di posta elettronica (C#)
description: Le informazioni in questo articolo sono utili per comprendere come usare l'API File di MIP SDK per elaborare i file con estensione msg (C#).
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: mbaldwin
ms.openlocfilehash: da7679c1d736cb6d732c417c3c38b2fbfd46eff0
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865298"
---
# <a name="file-api---process-email-msg-files-c"></a>API File - Elaborare file con estensione msg di posta elettronica (C#)

L'API File supporta operazioni di protezione per i file con estensione msg in modo identico a qualsiasi altro tipo di file, ad eccezione del fatto che l'SDK richiede che l'applicazione abiliti il flag di funzionalità MSG. In questo articolo verrà spiegato come impostare questo flag.

Come illustrato in precedenza, la creazione di un'istanza di `IFileEngine` richiede l'oggetto impostazione `FileEngineSettings`. È possibile usare FileEngineSettings per passare i parametri per le impostazioni personalizzate che l'applicazione deve impostare per una particolare istanza. La proprietà `CustomSettings` di `FileEngineSettings` viene usata per impostare il flag per `enable_msg_file_type` per abilitare l'elaborazione dei file con estensione msg.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Inizializzazione dell'applicazione API File (C#)](quick-app-initialization-csharp.md) per creare una soluzione Visual Studio iniziale. Questa guida di avvio rapido "Procedura - Elaborazione dei file con estensione msg dei messaggi di posta elettronica (C#)" si basa su quella precedente.
- Vedere i concetti relativi ai [file di posta elettronica in MIP SDK](concept-email.md).
- Facoltativamente: vedere i concetti relativi ai [motori di file in MIP SDK](concept-profile-engine-file-engine-cpp.md).
- Facoltativamente: rivedere i concetti esposti in [Gestori di file in MIP SDK](concept-handler-file-cpp.md).

## <a name="set-enable_msg_file_type-and-use-file-api-for-protecting-msg-file"></a>Impostare enable_msg_file_type e usare l'API File per proteggere il file con estensione msg

Come continuazione della guida di avvio rapido sull'inizializzazione dell'applicazione dell'API File, modificare il codice di costruzione del motore di file per impostare `enable_msg_file_type flag` e quindi usare il motore di file per proteggere un file con estensione msg.

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Inizializzazione dell'applicazione dell'API File (C#)".

2. Usare Esplora soluzioni per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Rimuovere l'implementazione della funzione `Main()` dalla guida di avvio rapido precedente. Inserire il codice seguente all'interno del corpo di `Main()`. Nel blocco di codice seguente il flag `enable_msg_file_type` viene impostato durante la creazione del motore di file e un file con estensione msg può quindi essere elaborato dagli oggetti `IFileHandler` creati usando il motore di file.

    ```csharp
    static void Main(string[] args)
    {
        // Initialize Wrapper for File API operations.
        MIP.Initialize(MipComponent.File);

        // Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId.
        ApplicationInfo appInfo = new ApplicationInfo()
        {
                ApplicationId = clientId,
                ApplicationName = appName,
                ApplicationVersion = "1.0.0"
        };

        // Instantiate the AuthDelegateImpl object, passing in AppInfo.
        AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

        MipContext mipContext = MIP.CreateMipContext(appInfo,"mip_data",LogLevel.Trace,null,null);

        // Initialize and instantiate the File Profile.
        // Create the FileProfileSettings object.
        // Initialize file profile settings to create/use local state.
        var profileSettings = new FileProfileSettings(mipContext, 
                                    CacheStorageType.OnDiskEncrypted, 
                                    new ConsentDelegateImplementation());

        // Load the Profile async and wait for the result.
        var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var customSettings = new List<KeyValuePair<string, string>>();
        customSettings.Add(new KeyValuePair<string, string>("enable_msg_file_type", "true"));

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
        engineSettings.Identity = new Identity("user1@tenant.com");
        //set custom settings for the engine
        engineSettings.CustomSettings = customSettings;

        //Add fileEngine to profile
        var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

        //Set file paths
        string inputFilePath = "<input-file-path>"; //.msg file to be protected
        string actualFilePath = inputFilePath;
        string outputFilePath = "<output-file-path>"; //protected .msg file
        string actualOutputFilePath = outputFilePath;

        //Create a file handler for original file
        var fileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, 
                                                                    actualFilePath, 
                                                                    true)).Result;

        // List templates available to the user and use one of them to protect the mail file.

            /// Listing of protection templates has to be performed by creating protection engine as described in protection quick start

        string templateId = "<template-id>"; //protection template retrieved using protection engine

        // Construct a protection descriptor on input file and use the same to set protection to the file
        ProtectionDescriptor descriptor = new ProtectionDescriptor(templateId);
        fileHandler.SetProtection(descriptor, new ProtectionSettings());

        // Commit changes, save as outputFilePath
        var result = Task.Run(async () => await fileHandler.CommitAsync(outputFilePath)).Result;

        // Create a new handler to read the protected file metadata
        var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, 
                                                                        actualOutputFilePath, 
                                                                        true)).Result;

        Console.WriteLine(string.Format("Original file: {0}", inputFilePath));
        Console.WriteLine(string.Format("Protected file: {0}", outputFilePath));
        Console.WriteLine(string.Format("TemplateID applied to file: {0} \r\nProtectionOwner: {1}", 
            handlerModified.Protection.ProtectionDescriptor.TemplateId,handlerModified.Protection.Owner));
        Console.WriteLine("Press a key to continue.");
        Console.ReadKey();

        // Application Shutdown
        fileHandler = null;
        handlerModified = null;
        fileEngine = null;
        fileProfile = null;
        mipContext = null;
    }

    ```

    Per altri dettagli sulle operazioni sui file, vedere i [concetti relativi al gestore di file](concept-handler-file-cpp.md).

4. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<input-file-path\> | Percorso completo di un file di messaggio di input di prova, ad esempio: `c:\\Test\\message.msg`. |
   | \<output-file-path\> | Percorso completo del file di output, che è una copia con etichetta del file di input, ad esempio: `c:\\Test\\message_protected.msg`. |
   | \<template-id\> | TemplateId recuperato usando il motore di protezione, ad esempio: `667466bf-a01b-4b0a-8bbf-a79a3d96f720`. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Usare **F6** (Compila soluzione) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere **F5** (Avvia debug) per eseguire l'applicazione.

```Console
    Original file: C:\Test.msg
    Protected file: C:\Test_protected.msg
    TemplateID applied to file: 667466bf-a01b-4b0a-8bbf-a79a3d96f720
    ProtectionOwner: user1@tenant.com
    Press a key to continue.
```

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione dell'applicazione C#

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| NetworkException: RMS service detected bad input in request. (Il servizio RMS ha rilevato un input errato nella richiesta.) Codice di errore RMS: Microsoft.RightsManagement.Exceptions.BadInputException | * Parameters are invalid if both TemplateID and Policy are null.(I parametri non sono validi se sia TemplateID sia Policy sono Null.), CorrelationId=f265b189-ebf6-4b30-a191-41539cdff215, CorrelationId.Description=FileHandler, HttpRequest.Id=04990d53-cf12-4969-9c80-06e365b312f2;d5fb4794-ac84-4445-abc6-647e41df62b2, HttpRequest.SanitizedUrl=https://api.aadrm.com/my/v2/publishinglicenses, HttpResponse.StatusCode=400, NetworkError.Category=FailureResponseCode* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il templateID non sia valido. Tornare al blocco di codice e correggere l'ID del modello di protezione, quindi ricompilare e rieseguire il test. |
| TemplateNotFoundException | *Unrecognized template ID (ID modello non riconosciuto), CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad, CorrelationId.Description=FileHandler, HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689;78538a57-a9fd-4717-8924-33581a04598b* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il templateID non sia valido. Tornare al blocco di codice e correggere l'ID del modello di protezione, quindi ricompilare e rieseguire il test. |
