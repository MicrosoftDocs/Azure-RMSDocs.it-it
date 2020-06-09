---
title: "Procedura: eseguire il downgrade o la rimozione di un'etichetta che richiede una giustificazione (C#)"
description: Questo articolo consente di comprendere lo scenario di come effettuare il downgrade o la rimozione di un'etichetta che necessita di giustificazione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: cdf128d5d01db0362fac1b76c1e0d81a15e55432
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548344"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>API file di Microsoft Information Protection SDK-giustificazione dell'azione per abbassare un'etichetta di riservatezza in un file (C#)

Questa Guida introduttiva gestisce un'operazione di downgrade dell'etichetta quando il criterio dell'etichetta richiede una giustificazione. In questo caso, si userà `IFileHandler` Interface per modificare le etichette di un file. Per ulteriori informazioni, consultare le informazioni di [riferimento sulle API](/dotnet/api/?term=microsoft.informationprotection).

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- [Guida introduttiva completa: impostare/ottenere prima le etichette di riservatezza (C#)](quick-file-set-get-label-csharp.md) , che compila una soluzione Starter di Visual Studio, per elencare le etichette di riservatezza di un'organizzazione, per impostare e leggere le etichette di riservatezza in/da un file. Questa Guida introduttiva "come eseguire il downgrade o la rimozione di un'etichetta che necessita di una giustificazione C#" si basa su quella precedente.
- Facoltativamente: esaminare i [concetti relativi ai gestori di file](concept-handler-file-cpp.md) nei concetti relativi a MIP SDK.

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>Aggiungere la logica per impostare un'etichetta inferiore su un file protetto

Aggiungere la logica per impostare un'etichetta di riservatezza su un file, usando l'oggetto gestore di file.

1. Aprire la soluzione di Visual Studio creata nella precedente sezione "Guida introduttiva: impostare/ottenere le etichette di riservatezza (C#).

2. Utilizzando Esplora soluzioni, aprire il file con estensione cs nel progetto che contiene l'implementazione del `Main()` metodo. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Aggiornare il `<label-id>` valore dalla Guida introduttiva precedente a un'etichetta di riservatezza che richiede una giustificazione per la riduzione. Durante l'esecuzione di questa Guida introduttiva, si imposterà prima questa etichetta e quindi si tenterà di abbassarla tramite frammenti di codice in ulteriori passaggi.

4. `Main()`Inserire il codice seguente verso la fine del corpo, sotto `Console.ReadKey()` e sopra il blocco di arresto dell'applicazione (in cui è stato interrotto nella Guida introduttiva precedente).

    ```csharp
    //Set paths and label ID
    string lowerInput = actualOutputFilePath;
    string lowerActualInput = lowerInput;
    string newLabelId = "<new-label-id>";
    string lowerOutput = "<downgraded-labled-output>";
    string lowerActualOutput = lowerOutput;

    //Create a file handler for that file
    var downgradeHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerInput, lowerActualInput, true)).Result;

    //Set Labeling Options
    LabelingOptions options = new LabelingOptions()
    {
        AssignmentMethod = AssignmentMethod.Standard
    };

    try
    {
        //Try to set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    catch (Microsoft.InformationProtection.Exceptions.JustificationRequiredException)
    {
        //Request justification from user
        Console.Write("Please provide justification for downgrading a label: ");
        string justification = Console.ReadLine();

        options.IsDowngradeJustified = true;
        options.JustificationMessage = justification;

        //Set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    // Commit changes, save as outputFilePath
    var downgradedResult = Task.Run(async () => await downgradeHandler.CommitAsync(lowerActualOutput)).Result;

    // Create a new handler to read the labeled file metadata
    var commitHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerOutput, lowerActualOutput, true)).Result;

    // Get the label from output file
    var newContentLabel = commitHandler.Label;
    Console.WriteLine(string.Format("Getting the new label committed to file: {0}", lowerOutput));
    Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", newContentLabel.Label.Name, newContentLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();

    ```

5. Verso la fine di Main () individuare il blocco di arresto dell'applicazione creato nella Guida introduttiva precedente e aggiungere le righe del gestore per rilasciare le risorse.

    ````csharp
    downgradeHandler = null;
    commitHandler = null;

    ````

6. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | valore |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | Percorso del file di output in cui si desidera salvare il file modificato. |
   | \<new-label-id\> | ID modello, copiato dall'output della console nella Guida introduttiva precedente, ad esempio: `bb7ed207-046a-4caf-9826-647cff56b990` . Assicurarsi che abbia una sensibilità inferiore rispetto all'etichetta del file precedentemente protetto. |

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

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Confidential
    IsProtected: True
    Press any key to continue . . .

    Please provide justification for downgrading a label: Lower label approved.
    Getting the new label committed to file: c:\Test\Test_downgraded.docx
    File Label: General
    IsProtected: False
    Press a key to continue.
   ```

Si noti che l'approccio simile si applica anche all' `DeleteLabel()` operazione, nel caso in cui l'etichetta da eliminare da un file richiede una giustificazione in base ai criteri di etichetta.`DeleteLabel()` la funzione genera un' `JustificationRequiredException` eccezione e il `IsDowngradeJustified` flag deve essere impostato su true nella gestione delle eccezioni prima di eliminare correttamente un'etichetta.