---
title: Procedura - Eseguire il downgrade o la rimozione di un'etichetta che richiede una giustificazione (C++)
description: Le informazioni in questo articolo sono utili per comprendere come effettuare il downgrade o la rimozione di un'etichetta che richiede una giustificazione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: 0e269238333a23da5b0b61f77f6be361838e8a17
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548140"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>API File di Microsoft Information Protection SDK - Giustificazione dell'azione per abbassare un'etichetta di riservatezza per un file (C++)

Questa guida di avvio rapido riguarda la gestione di un'operazione di downgrade dell'etichetta quando i criteri per le etichette richiedono una giustificazione. In questo caso si userà la classe `mip::FileHandler` per modificare le etichette di un file. Per altri dettagli, vedere le [informazioni di riferimento sull'API](./reference/mip-sdk-reference.md).

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Impostare/ottenere le etichette di riservatezza (C++)](quick-file-set-get-label-cpp.md), che crea una soluzione Visual Studio iniziale, per creare un elenco delle etichette di riservatezza di un'organizzazione, per impostare e leggere le etichette di riservatezza in/da un file. Questa guida di avvio rapido "Procedura - Eseguire il downgrade o la rimozione di un'etichetta che richiede una giustificazione (C++)" si basa su quella precedente.
- Facoltativamente: rivedere i [concetti relativi ai gestori di file](concept-handler-file-cpp.md) in MIP SDK.

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>Aggiungere la logica per impostare un'etichetta inferiore su un file protetto

Aggiungere la logica per impostare un'etichetta di riservatezza su un file usando l'oggetto `mip::FileHandler`.

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Impostare/ottenere etichette di riservatezza (C++).

2. Usare Esplora soluzioni per aprire il file con estensione cpp nel progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Aggiungere le direttive #include e using seguenti sotto le direttive esistenti corrispondenti, nella parte superiore del file:

    ```cpp

        #include "mip/file/file_error.h"

        using mip::JustificationRequiredError;
        using std::cin;

    ```

4. Aggiornare il valore `<label-id>` dalla guida di avvio rapido precedente impostando un'etichetta di riservatezza che richiede una giustificazione per l'abbassamento. Durante l'esecuzione di questa guida di avvio rapido, si imposterà prima questa etichetta e quindi si tenterà di abbassarla tramite frammenti di codice in ulteriori passaggi.

5. Verso la fine del corpo di `main()`, sotto `system("pause");` e prima del bocco di arresto (il punto in cui è stata interrotta la guida di avvio rapido precedente), inserire il codice seguente:

    ```cpp

    // Downgrade label
    // Set paths and lower label ID
    // Set a new label on input file.

    string lowerlabelId = "<lower-label-id>";
    cout << "\nApplying new Label ID " << lowerlabelId << " to " << filePathOut << endl;
    mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);

    // Try to apply a label with lower sensitivity.
    try
    {
        handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
    }

    catch (const mip::JustificationRequiredError& e)
    {
        // Request justification from user.
        cout<<"Please provide justification for downgrading a label: "<<endl;
        string justification;
        cin >> justification;

        // Set Justification provided flag
        bool isDowngradeJustified = true;
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
        labelingOptions.SetDowngradeJustification(isDowngradeJustified,justification);

        //Set new label.
        handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
    }

    catch (const std::exception& e)
    {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
    }

    // Commit changes, save as a different output file
    string lowerFilePathOut = "<lower-output-file-path>";
    try
    {
        cout << "Committing changes" << endl;
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        handler->CommitAsync(lowerFilePathOut, commitPromise);
        if (commitFuture.get()) {
            cout << "\nLabel committed to file: " << lowerFilePathOut << endl;
        }
        else {
            cout << "Failed to label: " + lowerFilePathOut << endl;
            return 1;
        }
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... did you specify a valid commit file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
    }
    system("pause");

    // Set up async FileHandler for output file operations
    string lowerActualFilePath = "<lower-content-identifier>";
    try
    {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
            lowerFilePathOut,
            lowerActualFilePath,
            true,
            std::make_shared<FileHandlerObserver>(),
            handlerPromise);

        handler = handlerFuture.get();
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
    }

    // Get the lowered label from output file
    try
    {
        cout << "\nGetting the label committed to file: " << lowerFilePathOut << endl;
        auto lowerLabel = handler->GetLabel();
        cout << "Name: " + lowerLabel->GetLabel()->GetName() << endl;
        cout << "Id: " + lowerLabel->GetLabel()->GetId() << endl;
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
    }
    system("pause");

    ```

6. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<lower-label-id\> | ID etichetta, copiato dall'output della console nella guida di avvio rapido precedente, ad esempio: `bb7ed207-046a-4caf-9826-647cff56b990`. Assicurarsi che abbia una riservatezza inferiore rispetto all'etichetta del file precedentemente protetto. |
   | \<lower-output-file-path\> | Percorso del file di output in cui si vuole salvare il file modificato. |
   | \<lower-content-identifier\> | Identificatore leggibile per il contenuto. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione richiede un token di accesso ogni volta che il SDK chiama il metodo `AcquireOAuth2Token()`. Come già fatto in precedenza nella guida di avvio rapido "Impostare/ottenere le etichette di riservatezza", eseguire lo script di PowerShell per acquisire ogni volta il token usando i valori specificati per $authority e $resourceUrl.

  ```console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID f55c2dea-db0f-47cd-8520-a52e1590fb6z to c:\Test\Test.docx
    Committing changes

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Label committed to file: c:\Test\Test.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Highly Confidential
    Id: f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying new Label ID f42a3342-8706-4288-bd31-ebb85995028z to c:\Test\Test_labeled.docx
    Please provide justification for downgrading a label:
    Need for sharing with wider audience.
    Committing changes

    Label committed to file: c:\Test\Test_downgraded.docx
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_downgraded.docx
    Name: General
    Id: f42a3342-8706-4288-bd31-ebb85995028z
    Press any key to continue . . .
   ```

Si noti che, nel caso in cui l'etichetta da eliminare da un file richieda una giustificazione in base ai criteri per le etichette, è necessario seguire un approccio simile per l'operazione `DeleteLabel()`. La funzione `DeleteLabel()` genera un'eccezione `mip::JustificationRequiredError`. Il flag `isDowngradeJustified` deve essere impostato su true nella gestione delle eccezioni prima di eliminare correttamente l'etichetta.