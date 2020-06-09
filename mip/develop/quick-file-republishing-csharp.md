---
title: 'Procedura: ripubblicazione dello scenario C #'
description: Questo articolo consente di comprendere lo scenario di utilizzo del gestore protezione per gli scenari di ripubblicazione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: d82424c03fe8c2e050bbd4095706fa675de5ed6e
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548208"
---
# <a name="microsoft-information-protection-sdk---file-api-re-publishing-quickstart-c"></a>Microsoft Information Protection SDK-Guida introduttiva alla ripubblicazione dell'API file (C#)

## <a name="overview"></a>Panoramica

Per una panoramica su questo scenario e su dove è possibile usarlo, vedere [ripubblicazione in MIP SDK](concept-republishing-cpp.md).

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- [Guida introduttiva completa: impostare/ottenere prima le etichette di riservatezza (C#)](quick-file-set-get-label-csharp.md) , che compila una soluzione Starter di Visual Studio, per elencare le etichette di riservatezza di un'organizzazione, per impostare e leggere le etichette di riservatezza in/da un file. Questa Guida introduttiva "procedura: ripubblicare un file protetto-C#" si basa su quella precedente.
- Facoltativamente: esaminare i [gestori di file](concept-handler-file-cpp.md) nei concetti relativi a MIP SDK.
- Facoltativamente: esaminare i [gestori della protezione](concept-handler-protection-cpp.md) nei concetti relativi a MIP SDK.

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>Aggiungere la logica per modificare e ripubblicare un file protetto

1. Aprire la soluzione di Visual Studio creata nell'articolo precedente "Guida introduttiva: impostare/ottenere le etichette di riservatezza (C#)".

2. Utilizzando Esplora soluzioni, aprire il file con estensione cs nel progetto che contiene l'implementazione del `Main()` metodo. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. `Main()`Inserire il codice seguente verso la fine del corpo, sotto `Console.ReadKey()` e sopra il blocco di arresto dell'applicazione (in cui è stato interrotto nella Guida introduttiva precedente).

    ```csharp

        string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

            //Create a fileHandler for consumption for the Protected File.
            var protectedFileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
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

                /// Write code here to perform further operations for edit ///

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
                Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", protectedLabel.Label.Id, protectedFileHandler.Protection.Owner, protectedLabel.IsProtectionAppliedFromLabel.ToString()));
                var reprotectedLabel = republishHandler.Label;
                Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
                Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", reprotectedLabel.Label.Id, republishHandler.Protection.Owner, reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
                Console.WriteLine("Press a key to continue.");
                Console.ReadKey();

            }

    ```

4. Verso la fine di Main () individuare il blocco di arresto dell'applicazione creato nella Guida introduttiva precedente e aggiungere le righe del gestore per rilasciare le risorse.

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;

    ````

5. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | valore |
   |:----------- |:----- |
   | \<protected-file-path\> | File protetto dalla Guida introduttiva precedente. |
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