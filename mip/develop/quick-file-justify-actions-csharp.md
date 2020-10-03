---
title: Procedura - Effettuare il downgrade o la rimozione di un'etichetta che richiede una giustificazione (C#)
description: Le informazioni in questo articolo sono utili per comprendere come effettuare il downgrade o la rimozione di un'etichetta che richiede una giustificazione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 666b0c7fdbc483f638f76def37ec3082c9eb7377
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2020
ms.locfileid: "91421195"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>API File di Microsoft Information Protection SDK - Giustificazione dell'azione per abbassare un'etichetta di riservatezza per un file (C#)

Questa guida di avvio rapido riguarda la gestione di un'operazione di downgrade di etichette quando i criteri per le etichette richiedono una giustificazione. In questo contesto verrà usata l'interfaccia `IFileHandler` per modificare le etichette di un file. Per altri dettagli, vedere le [informazioni di riferimento sull'API](/dotnet/api/?term=microsoft.informationprotection).

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Impostare/ottenere le etichette di riservatezza (C#)](quick-file-set-get-label-csharp.md), che crea una soluzione Visual Studio iniziale, per creare un elenco delle etichette di riservatezza di un'organizzazione, nonché per impostare e leggere le etichette di riservatezza in/da un file. Questa guida di avvio rapido "Procedura - Eseguire il downgrade o la rimozione di un'etichetta che richiede una giustificazione (C#)" si basa su quella precedente.
- Facoltativamente: rivedere i [concetti relativi ai gestori di file](concept-handler-file-cpp.md) in MIP SDK.

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>Aggiungere la logica per impostare un'etichetta inferiore su un file protetto

Aggiungere la logica per impostare un'etichetta di riservatezza su un file usando l'oggetto gestore di file.

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Impostare/ottenere etichette di riservatezza (C#).

2. Usare Esplora soluzioni per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Aggiornare il valore `<label-id>` dalla guida di avvio rapido precedente impostando un'etichetta di riservatezza che richiede una giustificazione per l'abbassamento. Durante l'esecuzione di questa guida di avvio rapido, si imposterà prima questa etichetta e quindi si tenterà di abbassarla tramite frammenti di codice in ulteriori passaggi.

4. Verso la fine del corpo di `Main()`, sotto `Console.ReadKey()` e prima del bocco di arresto dell'applicazione (il punto in cui è stata interrotta la guida di avvio rapido precedente), inserire il codice seguente.

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

5. Verso la fine di Main() trovare il blocco di arresto dell'applicazione creato nella guida di avvio rapido precedente e aggiungerlo sotto le righe del gestore per rilasciare le risorse.

    ````csharp
    downgradeHandler = null;
    commitHandler = null;
    ````

6. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | Percorso del file di output in cui si vuole salvare il file modificato. |
   | \<new-label-id\> | ID modello, copiato dall'output della console nell'Avvio rapido precedente, ad esempio: `bb7ed207-046a-4caf-9826-647cff56b990`. Assicurarsi che abbia una riservatezza inferiore rispetto all'etichetta del file precedentemente protetto. |

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

Si noti che è necessario seguire un approccio simile per l'operazione `DeleteLabel()`, nel caso in cui l'etichetta da eliminare da un file richieda una giustificazione in base ai criteri per le etichette. La funzione `DeleteLabel()` genera un'eccezione `JustificationRequiredException` e il flag `IsDowngradeJustified` deve essere impostato su true nella gestione delle eccezioni prima di eliminare correttamente un'etichetta.