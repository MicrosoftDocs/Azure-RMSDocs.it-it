---
title: Procedura - Scenario di ripubblicazione C#
description: Le informazioni in questo articolo sono utili per comprendere lo scenario di riutilizzo del gestore protezione per gli scenari di ripubblicazione (C#).
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: c3044feb585e1e3d843f906711644f2ae861b1b5
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535876"
---
# <a name="microsoft-information-protection-sdk---file-api-republishing-quickstart-c"></a>Microsoft Information Protection SDK - Avvio rapido alla ripubblicazione dell'API File (C#)

## <a name="overview"></a>Panoramica

Per una panoramica su questo scenario e su dove usarlo, vedere [Ripubblicazione in MIP SDK](concept-republishing.md).

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Impostare/ottenere le etichette di riservatezza (C#)](quick-file-set-get-label-csharp.md), che crea una soluzione Visual Studio iniziale, per creare un elenco delle etichette di riservatezza di un'organizzazione, per impostare e leggere le etichette di riservatezza in/da un file. Questa guida di avvio rapido alla ripubblicazione di un file protetto in C# si basa sulla precedente.
- Facoltativamente: rivedere i concetti esposti in [Gestori di file in MIP SDK](concept-handler-file-cpp.md).
- Facoltativamente: Rivedere i concetti in [Gestori protezione in MIP SDK](concept-handler-protection-cpp.md).

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>Aggiungere la logica per modificare e ripubblicare un file protetto

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Impostare/ottenere etichette di riservatezza (C#).

2. Usare Esplora soluzioni per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Verso la fine del corpo di `Main()`, sotto `Console.ReadKey()` e prima del bocco di arresto dell'applicazione (il punto in cui è stata interrotta la guida di avvio rapido precedente), inserire il codice seguente.

```csharp
string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

//Create a fileHandler for consumption for the Protected File.
var protectedFileHandler = Task.Run(async () => 
                            await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
                                                                    protectedFilePath,// actualFilePath
                                                                    false, //isAuditDiscoveryEnabled
                                                                    null)).Result; // fileExecutionState

// Store protection handler from file
var protectionHandler = protectedFileHandler.Protection;

//Check if the user has the 'Edit' right to the file
if (protectionHandler.AccessCheck("Edit"))
{
    // Decrypt file to temp path
    var tempPath = Task.Run(async () => await protectedFileHandler.GetDecryptedTemporaryFileAsync()).Result;

    /*
        Your own application code to edit the decrypted file belongs here. 
    */

    /// Follow steps below for re-protecting the edited file. ///
    // Create a new file handler using the temporary file path.
    var republishHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(tempPath, tempPath, false)).Result;

    // Set protection using the ProtectionHandler from the original consumption operation.
    republishHandler.SetProtection(protectionHandler);

    // New file path to save the edited file
    string reprotectedFilePath = "<reprotected-file-path>" // New file path for saving reprotected file.

    // Write changes
    var reprotectedResult = Task.Run(async () => await republishHandler.CommitAsync(reprotectedFilePath)).Result;

    var protectedLabel = protectedFileHandler.Label;
    Console.WriteLine(string.Format("Originally protected file: {0}", protectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        protectedLabel.Label.Id, 
                        protectedFileHandler.Protection.Owner, 
                        protectedLabel.IsProtectionAppliedFromLabel.ToString()));
    var reprotectedLabel = republishHandler.Label;
    Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        reprotectedLabel.Label.Id, 
                        republishHandler.Protection.Owner, 
                        reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();
}
```

4. Verso la fine di Main() trovare il blocco di arresto dell'applicazione creato nella guida di avvio rapido precedente e aggiungerlo sotto le righe del gestore per rilasciare le risorse.

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;
    ````

5. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<protected-file-path\> | File protetto dalla guida di avvio rapido precedente. |
   | \<reprotected-file-path\> | Percorso del file di output per il file modificato da ripubblicare. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione *potrebbe* richiedere l'autenticazione tramite ADAL ogni volta che il SDK chiama il metodo `AcquireToken()`. Se esistono già credenziali memorizzate nella cache, non verrà richiesto di accedere e visualizzare l'elenco delle etichette e quindi le informazioni sull'etichetta applicata e sul file modificato.

  ```console
    Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
    Public : 73254501-3d5b-4426-979a-657881dfcb1e
    General : da480625-e536-430a-9a9e-028d16a29c59
    Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
    Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
    Press a key to continue.

    Getting the label committed to file: C:\Test\Test_protected.docx
    File Label: Confidential
    IsProtected: True
    Press a key to continue.
    Originally protected file: C:\Test\Test_protected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Reprotected file: C:\Test\Test_reprotected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Press a key to continue.
   ```