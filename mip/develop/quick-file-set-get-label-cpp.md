---
title: Avvio rapido - Impostare e ottenere un'etichetta di riservatezza su un file mediante il SDK C++ di MIP
description: Questo Avvio rapido illustra come usare il SDK C++ di Microsoft Information Protection per impostare e ottenere un'etichetta di riservatezza su un file.
services: information-protection
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 651fc73c00f18d06ad1a824337a096331bc7e897
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251744"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Avvio rapido: Impostare e ottenere un'etichetta di riservatezza (C++)

Questo Avvio rapido illustra come usare altre API dei file di MIP. Con una delle etichette di riservatezza elencate nell'Avvio rapido precedente, si usa un gestore di file per impostare/ottenere l'etichetta su un file. La classe del gestore di file dispone di varie operazioni per l'impostazione e l'ottenimento di etichette o della protezione per i tipi di file supportati.

## <a name="prerequisites"></a>Prerequisiti

Se non è stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Elencare le etichette di riservatezza (C++)](quick-file-list-labels-cpp.md), che crea una soluzione Visual Studio iniziale, per creare un elenco delle etichette di riservatezza di un'organizzazione. Il presente Avvio rapido "Impostare e ottenere un'etichetta di riservatezza" è basato su quello precedente.
- Facoltativo: rivedere i concetti esposti in [File handlers in the MIP SDK](concept-handler-file-cpp.md) (Gestori file nel SDK MIP).

## <a name="implement-an-observer-class-to-monitor-the-file-handler-object"></a>Implementare una classe observer per monitorare l'oggetto gestore file

Come nel caso dell'observer implementato per il profilo e il motore file nell'Avvio rapido Application initialization (Inizializzazione dell'applicazione), ora si implementa una classe observer per un oggetto gestore di file.

Creare un'implementazione di base per una classe observer mediante l'estensione della classe `mip::FileHandler::Observer` del SDK. Viene creata un'istanza di observer che viene usata in seguito per il monitoraggio delle operazioni gestore di file.

1. Aprire la soluzione Visual Studio sulla quale si è lavorato nell'articolo precedente "Quickstart: List sensitivity labels (C++)" (Avvio rapido: Elencare le etichette di riservatezza (C++)).

2. Aggiungere una nuova classe al progetto, che genera automaticamente i file header/.h e implementation/.cpp:

   - In **Esplora soluzioni** fare di nuovo clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi**, quindi scegliere **Classe**.
   - Nella finestra di dialogo **Aggiungi classe**:
     - Nel campo **Nome classe** immettere "filehandler_observer". Si noti che i campi del **file con estensione h** e del **file con estensione cpp** vengono popolati automaticamente in base al nome immesso.
     - Al termine fare clic su **OK**.

3. Dopo la generazione dei file con estensione h e cpp per la classe, entrambi i file vengono aperti nelle schede Editor gruppo. A questo punto aggiornare ogni file per implementare la nuova classe observer:

   - Aggiornare "filehandler_observer.h", selezionando ed eliminando la classe `filehandler_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare la seguente origine nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <memory>
     #include "mip/file/file_engine.h"
     #include "mip/file/file_handler.h"

     class FileHandlerObserver final : public mip::FileHandler::Observer {
     public:
        FileHandlerObserver() { }
        // Observer implementation
        void OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) override;
        void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
        void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) override;
        void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;       
     };
     ```

   - Aggiornare "filehandler_observer.cpp", selezionando ed eliminando l'implementazione della classe `filehandler_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare la seguente origine nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_value(fileHandler);
     }

     void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_exception(error);
     }

     void FileHandlerObserver::OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_value(committed);
     }

     void FileHandlerObserver::OnCommitFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_exception(error);
     }
     ```

4. Facoltativamente, usare F6 (**Compila soluzione**) per eseguire una compilazione/collegamento di prova della soluzione e assicurarsi che venga compilata correttamente prima di continuare.

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Aggiungere codice per impostare e ottenere un'etichetta di riservatezza

Aggiungere codice per impostare e ottenere un'etichetta di riservatezza su un file mediante l'oggetto file engine. 

1. Usare **Esplora soluzioni** per aprire il file con estensione cpp del progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file assume lo stesso nome del progetto che lo contiene, specificato dall'utente durante la creazione del progetto. 

2. Aggiungere le seguenti direttive `#include` e `using` sotto le direttive esistenti corrispondenti, nella parte superiore del file:

   ```cpp
   #include "filehandler_observer.h" 
   #include "mip/file/file_handler.h" 

   using mip::FileHandler;
   ```
3. Verso la fine del corpo `main()`, dopo `system("pause");` e prima di `return 0;` (il punto in cui è stato interrotto l'Avvio rapido precedente), inserire il codice seguente:

   ```cpp
   // Set up async FileHandler for input file operations
   string filePathIn = "<input-file-path>";
   std::shared_ptr<FileHandler> handler;
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(filePathIn, mip::ContentState::REST, std::make_shared<FileHandlerObserver>(), handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid input file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Set a label on input file
   try
   {
        string labelId = "<label-id>";
        cout << "\nApplying Label ID " << labelId << " to " << filePathIn << endl;
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
        handler->SetLabel(labelId, labelingOptions);
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Commit changes, save as a different/output file
   string filePathOut = "<output-file-path>";
   try
   {
        cout << "Committing changes" << endl;
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        handler->CommitAsync(filePathOut, commitPromise);
        if (commitFuture.get()) {
            cout << "\nLabel committed to file: " << filePathOut << endl;
        }
        else {
            cout << "Failed to label: " + filePathOut << endl;
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
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(filePathOut, mip::ContentState::REST, std::make_shared<FileHandlerObserver>(), handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Get the label from output file
   try
   {
        cout << "\nGetting the label committed to file: " << filePathOut << endl;
        auto label = handler->GetLabel();
        cout << "Name: " + label->GetLabel()->GetName() << endl;
        cout << "Id: " + label->GetLabel()->GetId() << endl;
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");
   ```

4. Sostituire i valori segnaposto nel codice sorgente appena incollato, usando i valori seguenti:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<input-file-path\> | Percorso completo di un file di input di test, ad esempio: `c:\\Test\\Test.docx`. |
   | \<label-id\> | ID etichetta di riservatezza, copiato dalla console di output nell'Avvio rapido precedente, ad esempio: `f42a3342-8706-4288-bd31-ebb85995028z`. |
   | \<output-file-path\> | Percorso completo del file di output, che è una copia con etichetta del file di input, ad esempio: `c:\\Test\\Test_labeled.docx`. |

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client. 

1. Usare F6 (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione richiede un token di accesso ogni volta che il SDK chiama il metodo `AcquireOAuth2Token()`. Come già fatto in precedenza nell'Avvio rapido "List sensitivity labels" (Elencare le etichette di riservatezza), eseguire lo script di PowerShell per acquisire ogni volta il token usando i valori specificati. `AcquireOAuth2Token()` prova a usare un token generato in precedenza, se l'autorità e la risorsa richieste sono le stesse:

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
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

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

È possibile verificare l'applicazione dell'etichetta aprendo il file di output ed esaminando visivamente le impostazioni di protezione delle informazioni del documento.

> [!NOTE]
> Se si sta applicando l'etichetta a un documento di Office ma non è stato effettuato l'accesso tramite un account del tenant Azure Active Directory (AD) in cui è stato ottenuto il token di accesso (e vengono configurate le etichette di riservatezza), è possibile che venga richiesto di effettuare l'accesso per poter aprire il documento con etichetta. 



