---
title: Procedura - Scenario di ripubblicazione C++
description: Le informazioni in questo articolo sono utili per comprendere lo scenario di riutilizzo del gestore protezione per gli scenari di ripubblicazione (C++).
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: a9edf2faf674968edf0121b677a79be39ec86cc7
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535859"
---
# <a name="file-api-re-publishing-quickstart-c"></a>Avvio rapido alla ripubblicazione dell'API File (C++)

## <a name="overview"></a>Panoramica

Per una panoramica su questo scenario e su dove usarlo, vedere [Ripubblicazione in MIP SDK](concept-republishing.md).

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Impostare/ottenere le etichette di riservatezza (C++)](quick-file-set-get-label-cpp.md), che crea una soluzione Visual Studio iniziale, per creare un elenco delle etichette di riservatezza di un'organizzazione, per impostare e leggere le etichette di riservatezza in/da un file. Questa guida di avvio rapido "Procedura - Eseguire il downgrade o la rimozione di un'etichetta che richiede una giustificazione (C++)" si basa su quella precedente.
- Facoltativamente: rivedere i concetti esposti in [Gestori di file in MIP SDK](concept-handler-file-cpp.md).
- Facoltativamente: rivedere i concetti in [Gestori protezione in MIP SDK](concept-handler-protection-cpp.md).

## <a name="add-logic-to-filehandler-observer-class"></a>Aggiungere la logica alla classe Observer FileHandler

Per poter decrittografare un file protetto usando il metodo `GetDecryptedTemporaryFileAsync()` esposto da `mip::FileHandler`, è necessario definire i callback per il metodo asincrono in caso di esito positivo e negativo come indicato di seguito.

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Impostare/ottenere etichette di riservatezza (C++).

2. Con Esplora soluzioni, aprire il file `filehandler_observer.h` nel progetto. Verso la fine della definizione FileHandler, prima di `};` aggiungere le righe seguenti per la dichiarazione del metodo.

    ```cpp
        void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) override;
        void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
    ```

3. Con Esplora soluzioni, aprire il file `filehandler_observer.cpp` nel progetto. Verso la fine del file, aggiungere le righe seguenti per le definizioni del metodo.

    ```cpp

        void FileHandlerObserver::OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_value(decryptedFilePath);
        }

        void FileHandlerObserver::OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_exception(error);
        }
    ```

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>Aggiungere la logica per modificare e ripubblicare un file protetto

1. Usare Esplora soluzioni per aprire il file con estensione cpp nel progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Verso la fine del corpo di main(), sotto system("pause"); e sopra return 0; (il punto in cui è stata interrotta la guida di avvio rapido precedente), inserire il codice seguente:

```cpp
//Originally protected file's path.
std::string protectedFilePath = "<protected-file-path>";

// Create file handler for the file
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
engine->CreateFileHandlerAsync(protectedFilePath, 
                                protectedFilePath, 
                                true, 
                                std::make_shared<FileHandlerObserver>(), 
                                handlerPromise);
auto protectedFileHandler = handlerFuture.get();

// retieve and store protection handler from file
auto protectionHandler = protectedFileHandler->GetProtection();

//Check if the user has the 'Edit' right to the file and if so decrypt the file.
if (protectionHandler->AccessCheck("Edit")) {

    // Decrypt file to temp path using the same file handler
    auto tempPromise = std::make_shared<std::promise<string>>();
    auto tempFuture = tempPromise->get_future();
    protectedFileHandler->GetDecryptedTemporaryFileAsync(tempPromise);
    auto tempPath = tempFuture.get();

    /// Write code here to perform further operations for edit ///

    /// Follow steps below for re-protecting the edited file ///

    // Create a new file handler using the temporary file path.
    auto reprotectPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto reprotectFuture = reprotectPromise->get_future();
    engine->CreateFileHandlerAsync(tempPath, 
                                    tempPath, 
                                    true, 
                                    std::make_shared<FileHandlerObserver>(), 
                                    reprotectPromise);
    auto republishHandler = reprotectFuture.get();

    // Set protection using the ProtectionHandler from the original consumption operation.
    republishHandler->SetProtection(protectionHandler);
    std::string reprotectedFilePath = "<protected-file-path>";

    // Commit changes
    auto republishPromise = std::make_shared<std::promise<bool>>();
    auto republishFuture = republishPromise->get_future();
    republishHandler->CommitAsync(reprotectedFilePath, republishPromise);

    // Validate republishing
    cout << "Protected File: " + protectedFilePath<<endl;
    cout << "Protected Label ID: " + protectedFileHandler->GetLabel()->GetLabel()->GetId() << endl;
    cout << "Protection Owner: " + protectedFileHandler->GetProtection()->GetOwner() << endl<<endl;

    cout << "Republished File: " + reprotectedFilePath<<endl;
    cout << "Republished Label ID: " + republishHandler->GetLabel()->GetLabel()->GetId() << endl;
    cout << "Republished Owner: " + republishHandler->GetProtection()->GetOwner() << endl;
}
```

3. Verso la fine di Main() trovare il blocco di arresto dell'applicazione creato nella guida di avvio rapido precedente e aggiungerlo sotto le righe del gestore per rilasciare le risorse.

    ````csharp
        protectedFileHandler = nullptr;
        protectionHandler = nullptr;

    ````

4. Sostituire i valori segnaposto nel codice sorgente, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<protected-file-path\> | File protetto dalla guida di avvio rapido precedente. |
   | \<reprotected-file-path\> | Percorso del file di output per il file modificato da ripubblicare. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione richiede un token di accesso ogni volta che il SDK chiama il metodo `AcquireOAuth2Token()`. Come già fatto in precedenza nella guida di avvio rapido "Impostare/ottenere etichette di riservatezza", eseguire lo script di PowerShell per acquisire ogni volta il token usando i valori specificati per $authority e $resourceUrl.

  ```console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Sensitivity labels for your organization:
    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to C:\Test\Test.docx
    Committing changes

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Label committed to file: C:\Test\Test_labeled.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: C:\Test\Test_labeled.docx
    Name: Confidential
    Id: 074e457c-5848-4542-9a6f-34a182080e7z
    Press any key to continue . . .
    Protected File: C:\Test\Test_labeled.docx
    Protected Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Protection Owner: user1@tenant.onmicrosoft.com

    Republished File: c:\Test\Test_republished.docx
    Republished Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Republished Owner: user1@tenant.onmicrosoft.com

    Press any key to close this window . . .

   ```
   