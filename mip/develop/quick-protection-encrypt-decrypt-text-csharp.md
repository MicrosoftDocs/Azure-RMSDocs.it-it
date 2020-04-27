---
title: "Avvio rapido: Crittografare e decrittografare il testo usando l'API Protezione SDK C# di MIP"
description: Avvio rapido che illustra come usare il wrapper . NET SDK di Protezione di Microsoft Information Protection per crittografare e decrittografare il testo ad hoc usando un modello di protezione.
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 62db0dae8eb0c2c7c0f63d9fd995259077601148
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766355"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>Guida introduttiva: Crittografare/decrittografare il testo usando SDK MIP (C#)

Questo Avvio rapido illustra come sfruttare le API Protezione di MIP. Con uno dei modelli di protezione elencati nell'Avvio rapido precedente, si usa un gestore di Protezione per crittografare il testo ad hoc. La classe del gestore di Protezione espone diverse operazioni per applicare/rimuovere la protezione.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: In primo luogo elencare i modelli di protezione (C#)](quick-protection-list-templates-csharp.md), che compilano una soluzione Visual Studio iniziale, per elencare i modelli di protezione disponibili per un utente autenticato. Questo Avvio rapido per crittografare/decrittografare il testo si basa su sull'avvio precedente.
- Facoltativamente: Rivedere i concetti in [Gestori di Protezione nell'SDK MIP](concept-handler-protection-cpp.md).

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Aggiungere codice per impostare e ottenere un'etichetta di riservatezza

Aggiungere la logica per crittografare il testo ad hoc, usando l'oggetto motore di Protezione.

1. Usare **Esplora soluzioni** per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Verso la fine del corpo `Main()`, nel punto in cui è stato interrotto l'Avvio rapido precedente inserire il codice seguente:

   ```csharp
   //Set text to encrypt and template ID
   string inputText = "<Sample-text>";
   string templateId = "<template-id>";
   //Create a template based publishing descriptor
   ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(templateId);

   //Create publishing settings using protection descriptor
   PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor);

   //Generate Protection Handler for publishing
   var publishingHandler = Task.Run(async() => await protectionEngine.CreateProtectionHandlerForPublishingAsync(publishingSettings)).Result;

   //Encrypt text using Publishing handler
   long bufferSize = publishingHandler.GetProtectedContentLength(inputText.Length, true);
   byte[] inputTextBuffer = Encoding.ASCII.GetBytes(inputText);
   byte[] encryptedTextBuffer = new byte[bufferSize];
   publishingHandler.EncryptBuffer(0, inputTextBuffer, encryptedTextBuffer, true);
   Console.WriteLine("Original text: {0}", inputText);
   Console.WriteLine("Encrypted text: {0}", Encoding.UTF8.GetString(encryptedTextBuffer));

   //Create a Protection handler for consumption using the same publishing licence
   var serializedPublishingLicense = publishingHandler.GetSerializedPublishingLicense();
   PublishingLicenseInfo plInfo = PublishingLicenseInfo.GetPublishingLicenseInfo(serializedPublishingLicense);
   ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo);
   var consumptionHandler = protectionEngine.CreateProtectionHandlerForConsumption(consumptionSettings);

   //Use the handler to decrypt the encrypted text
   long buffersize = encryptedTextBuffer.Length;
   byte[] decryptedBuffer = new byte[bufferSize];
   var bytesDecrypted = consumptionHandler.DecryptBuffer(0, encryptedTextBuffer, decryptedBuffer, true);
   byte[] OutputBuffer = new byte[bytesDecrypted];
   for (int i = 0; i < bytesDecrypted; i++){
      OutputBuffer[i] = decryptedBuffer[i];
   }

   Console.WriteLine("Decrypted content: {0}", Encoding.UTF8.GetString(OutputBuffer));
   Console.WriteLine("Press a key to quit.");
   Console.ReadKey();

   ```

3. Verso la fine di `Main()` trovare il blocco di arresto dell'applicazione creato nel primo avvio rapido e aggiungere le righe del gestore:

   ```csharp
   // Application Shutdown
   publishingHandler = null;
   consumptionHandler = null;
   protectionEngine = null;
   protectionProfile = null;
   mipContext = null;
   ```

4. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<sample-text\> | Testo di esempio che si vuole crittografare, ad esempio: `My secure text`. |
   | \<template-id\> | ID modello, copiato dall'output della console nell'Avvio rapido precedente, ad esempio: `bb7ed207-046a-4caf-9826-647cff56b990`. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione *potrebbe* richiedere l'autenticazione tramite ADAL ogni volta che il SDK chiama il metodo `AcquireToken()`. Se esistono già credenziali memorizzate nella cache, non verrà richiesto di accedere e visualizzare l'elenco delle etichette e quindi le informazioni sull'etichetta applicata e sul file modificato.

  ```console
   Original content: My secure text
   Encrypted content: c?_hp???Q??+<?
   Decrypted content: My secure text
   Press a key to quit.
   ```
