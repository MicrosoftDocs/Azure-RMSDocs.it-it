---
title: "Avvio rapido: Impostare e ottenere un'etichetta di riservatezza su un file mediante il SDK C# di MIP"
description: Questo Avvio rapido illustra come usare il wrapper .NET del SDK Microsoft Information Protection per impostare e ottenere un'etichetta di riservatezza su un file.
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: c081d20ba3cfffdc1db06ade5d918230f3b9eff8
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75554991"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Guida introduttiva: Impostare e ottenere un'etichetta di riservatezza (C#)

Questo Avvio rapido illustra come usare altre API dei file di MIP. Con una delle etichette di riservatezza elencate nell'Avvio rapido precedente, si usa un gestore di file per impostare/ottenere l'etichetta su un file. La classe del gestore di file dispone di varie operazioni per l'impostazione e l'ottenimento di etichette o della protezione per i tipi di file supportati.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Elencare le etichette di riservatezza (C#)](quick-file-list-labels-csharp.md), che crea una soluzione Visual Studio iniziale, per creare un elenco delle etichette di riservatezza di un'organizzazione. Il presente Avvio rapido "Impostare e ottenere un'etichetta di riservatezza" è basato su quello precedente.
- Facoltativamente: rivedere i concetti esposti in [Gestori di file in MIP SDK](concept-handler-file-cpp.md).

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Aggiungere codice per impostare e ottenere un'etichetta di riservatezza

Aggiungere codice per impostare e ottenere un'etichetta di riservatezza su un file mediante l'oggetto file engine. 

1. Usare **Esplora soluzioni** per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto. 

2. Verso la fine del corpo `Main()`, dopo `Console.ReadKey()` e prima di `}` (il punto in cui è stato interrotto l'Avvio rapido precedente), inserire il codice seguente:

   ```csharp
     //Set paths and label ID
     string inputFilePath = "<input-file-path>";
     string actualFilePath = inputFilePath;
     string labelId = "<label-id>";
     string outputFilePath = "<output-file-path>";
     string actualOutputFilePath = outputFilePath;

     //Create a file handler for that file
     //Note: the 2nd inputFilePath is used to provide a human-readable content identifier for admin auditing. 
     var handler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, actualFilePath, true)).Result;

     //Set Labeling Options
     LabelingOptions labelingOptions = new LabelingOptions()
     {
          AssignmentMethod = AssignmentMethod.Standard
     };

     // Set a label on input file
     handler.SetLabel(engine.GetLabelById(labelId), labelingOptions, new ProtectionSettings());

     // Commit changes, save as outputFilePath
     var result = Task.Run(async () => await handler.CommitAsync(outputFilePath)).Result;

     // Create a new handler to read the labeled file metadata
     var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, actualOutputFilePath, true)).Result;

     // Get the label from output file
     var contentLabel = handlerModified.Label;
     Console.WriteLine(string.Format("Getting the label committed to file: {0}", outputFilePath));
     Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", contentLabel.Label.Name, contentLabel.IsProtectionAppliedFromLabel.ToString()));
     Console.WriteLine("Press a key to continue.");
     Console.ReadKey();
   ```

3. Verso la fine di `Main()` trovare il blocco di arresto dell'applicazione creato nel primo avvio rapido e rimuovere il commento dalla riga del gestore:

   ```csharp
   // Application Shutdown
   handler = null;
   fileEngine = null;
   fileProfile = null;
   mipContext = null;
   ```

4. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<input-file-path\> | Percorso completo di un file di input di test, ad esempio: `c:\\Test\\Test.docx`. |
   | \<label-id\> | ID etichetta di riservatezza, copiato dalla console di output nell'Avvio rapido precedente, ad esempio: `f42a3342-8706-4288-bd31-ebb85995028z`. |
   | \<output-file-path\> | Percorso completo del file di output, che è una copia con etichetta del file di input, ad esempio: `c:\\Test\\Test_labeled.docx`. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client. 

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione *potrebbe* richiedere l'autenticazione tramite ADAL ogni volta che il SDK chiama il metodo `AcquireToken()`. Se esistono già credenziali memorizzate nella cache, non verrà richiesto di accedere e visualizzare l'elenco delle etichette e quindi le informazioni sull'etichetta applicata e sul file modificato.

  ```console   
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes
   
   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .
  
   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

È possibile verificare l'applicazione dell'etichetta aprendo il file di output ed esaminando visivamente le impostazioni di protezione delle informazioni del documento.

> [!NOTE]
> Se si sta applicando l'etichetta a un documento di Office ma non è stato effettuato l'accesso tramite un account del tenant Azure Active Directory (AD) in cui è stato ottenuto il token di accesso (e vengono configurate le etichette di riservatezza), è possibile che venga richiesto di effettuare l'accesso per poter aprire il documento con etichetta. 
