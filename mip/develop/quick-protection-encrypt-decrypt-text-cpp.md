---
title: "Avvio rapido: Crittografare e decrittografare il testo usando l'API Protezione SDK C++ di MIP"
description: Argomento di avvio rapido che illustra come usare l'API Protezione di Microsoft Information Protection SDK per crittografare e decrittografare il testo ad hoc tramite un modello di protezione (C++)
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 1258bfcd6c47611b439a29406ed0e78b644a5803
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535842"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>Guida introduttiva: Crittografare/decrittografare il testo usando l'SDK MIP (C++)

Questo Avvio rapido illustra come sfruttare le API Protezione di MIP. Con uno dei modelli di protezione elencati nell'Avvio rapido precedente, si usa un gestore di Protezione per crittografare il testo ad hoc. La classe del gestore di Protezione espone diverse operazioni per applicare/rimuovere la protezione.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: In primo luogo elencare i modelli di protezione (C++)](quick-protection-list-templates-cpp.md), che compilano una soluzione Visual Studio iniziale, per elencare i modelli di protezione disponibili per un utente autenticato. Questo Avvio rapido per crittografare/decrittografare del testo si basa su sull'avvio precedente.
- Facoltativamente: Rivedere i concetti in [Gestori di Protezione nell'SDK MIP](concept-handler-protection-cpp.md).

## <a name="implement-an-observer-class-to-monitor-the-protection-handler-object"></a>Implementare una classe osservatore per monitorare l'oggetto gestore di Protezione

Analogamente all'osservatore implementato per il profilo e il motore di Protezione nell'Avvio rapido per l'inizializzazione dell'applicazione, ora si implementa una classe osservatore per oggetti gestore di Protezione.

Creare un'implementazione di base per un osservatore gestore di Protezione estendendo la classe `mip::ProtectionHandler::Observer` dell'SDK. Si creerà un'istanza dell'osservatore che sarà usata in seguito per il monitoraggio delle operazioni gestore di Protezione.

1. Aprire la soluzione Visual Studio sulla quale si è lavorato nell'articolo precedente "Avvio rapido: Elencare i modelli di protezione (C++)".

2. Aggiungere una nuova classe al progetto, che genera automaticamente i file di intestazione (.h) e di implementazione (.cpp):

   - In **Esplora soluzioni** fare di nuovo clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi**, quindi scegliere **Classe**.
   - Nella finestra di dialogo **Aggiungi classe**:
     - Nel campo **Nome classe** immettere "handler_observer". Si noti che i campi del **file con estensione h** e del **file con estensione cpp** vengono popolati automaticamente in base al nome immesso.
     - Al termine fare clic su **OK**.

3. Dopo la generazione dei file con estensione h e cpp per la classe, entrambi i file vengono aperti nelle schede Editor gruppo. A questo punto aggiornare ogni file per implementare la nuova classe osservatore:

   - Aggiornare "handler_observer.h", selezionando/eliminando la classe `handler_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::shared_ptr;
     using std::exception_ptr;

     class ProtectionHandlerObserver final : public mip::ProtectionHandler::Observer {
          public:
          ProtectionHandlerObserver() { }
          void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
          void OnCreateProtectionHandlerFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;
          };

     ```

   - Aggiornare "handler_observer.cpp", selezionando/eliminando l'implementazione della classe `handler_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include "handler_observer.h"
     using std::shared_ptr;
     using std::promise;
     using std::exception_ptr;

     void ProtectionHandlerObserver::OnCreateProtectionHandlerSuccess(
          const shared_ptr<mip::ProtectionHandler>& protectionHandler,const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
               createProtectionHandlerPromise->set_value(protectionHandler);
               };

     void ProtectionHandlerObserver::OnCreateProtectionHandlerFailure(
          const exception_ptr& Failure, const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get())
               createProtectionHandlerPromise->set_exception(Failure);
               };

     ```

4. Facoltativamente, usare CTRL+MAIUSC+B (**Compila soluzione**) per eseguire una compilazione/collegamento di prova della soluzione e assicurarsi che venga compilata correttamente prima di continuare.

## <a name="add-logic-to-encrypt-and-decrypt-ad-hoc-text"></a>Aggiungere la logica per crittografare e decrittografare il testo ad hoc

Aggiungere la logica per crittografare e decrittografare il testo ad hoc, usando l'oggetto motore di Protezione.

1. Usare **Esplora soluzioni** per aprire il file con estensione cpp nel progetto che contiene l'implementazione del metodo `main()`.

2. Aggiungere le direttive #include e using seguenti sotto le direttive esistenti corrispondenti, nella parte superiore del file:

   ```cpp
     #include "mip/protection/protection_descriptor_builder.h"
     #include "mip/protection_descriptor.h"
     #include "handler_observer.h"

     using mip::ProtectionDescriptor;
     using mip::ProtectionDescriptorBuilder;
     using mip::ProtectionHandler;
   ```

3. Verso la fine del corpo `Main()`, nel punto in cui è stato interrotto l'Avvio rapido precedente inserire il codice seguente:

   ```cpp
   //Encrypt/Decrypt text:
   string templateId = "<Template-ID>";//Template ID from previous QuickStart e.g. "bb7ed207-046a-4caf-9826-647cff56b990"
   string inputText = "<Sample-Text>";//Sample Text

   //Refer to ProtectionDescriptor docs for details on creating the descriptor
   auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
   const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();

   //Create Publishing settings using a descriptor
   mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);

   //Create a publishing protection handler using Protection Descriptor
   auto handlerObserver = std::make_shared<ProtectionHandlerObserver>();
   engine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, pHandlerPromise);
   auto publishingHandler = pHandlerFuture.get();

   std::vector<uint8_t> inputBuffer(inputText.begin(), inputText.end());

   //Show action plan
   cout << "Applying Template ID " + templateId + " to: " << endl << inputText << endl;

   //Encrypt buffer using Publishing Handler
   std::vector<uint8_t> encryptedBuffer;
   encryptedBuffer.resize(static_cast<size_t>(publishingHandler->GetProtectedContentLength(inputText.size(), true)));

   publishingHandler->EncryptBuffer(0,
                         &inputBuffer[0],
                         static_cast<int64_t>(inputBuffer.size()),
                         &encryptedBuffer[0],
                         static_cast<int64_t>(encryptedBuffer.size()),
                         true);

   std::string encryptedText(encryptedBuffer.begin(), encryptedBuffer.end());
   cout << "Encrypted Text :" + encryptedText;

   //Show action plan
   cout << endl << "Decrypting string: " << endl << endl;

   //Generate publishing licence, so it can be used later to decrypt text.
   auto serializedPublishingLicense = publishingHandler->GetSerializedPublishingLicense();

   //Use same PL to decrypt the encryptedText.
   auto cHandlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
   auto cHandlerFuture = cHandlerPromise->get_future();
   shared_ptr<ProtectionHandlerObserver> cHandlerObserver = std::make_shared<ProtectionHandlerObserver>();

   //Create consumption settings using serialised publishing licence.
   mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
   engine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, cHandlerObserver, cHandlerPromise);

   auto consumptionHandler = cHandlerFuture.get();

   //Use consumption handler to decrypt the text.
   std::vector<uint8_t> decryptedBuffer(static_cast<size_t>(encryptedText.size()));

   int64_t decryptedSize = consumptionHandler->DecryptBuffer(
        0,
        &encryptedBuffer[0],
        static_cast<int64_t>(encryptedBuffer.size()),
        &decryptedBuffer[0],
        static_cast<int64_t>(decryptedBuffer.size()),
        true);

   decryptedBuffer.resize(static_cast<size_t>(decryptedSize));

   std::string decryptedText(decryptedBuffer.begin(), decryptedBuffer.end());

   // Output decrypted content. Should match original input text.
   cout << "Decrypted Text :" + decryptedText << endl;

   ```

4. Verso la fine di `main()` trovare il blocco di arresto dell'applicazione creato nel primo avvio rapido e aggiungerlo sotto le righe per rilasciare le risorse del gestore:

   ```cpp
    publishingHandler = nullptr;
    consumptionHandler = nullptr;
   ```

5. Sostituire come segue i valori segnaposto nel codice sorgente, usando costanti stringa:

   | Segnaposto | Valore |
   |:----------- |:----- |
   | \<sample-text\> | Testo di esempio che si vuole proteggere, ad esempio: `"cipher text"`. |
   | \<Template-Id\> | ID modello che da usare per proteggere il testo. ad esempio `"bb7ed207-046a-4caf-9826-647cff56b990"` |
  
## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione richiede un token di accesso ogni volta che il SDK chiama il metodo `AcquireOAuth2Token()`. Come già fatto in precedenza nell'Avvio rapido "Elencare i modelli di protezione", eseguire lo script di PowerShell per acquisire ogni volta il token usando i valori specificati per $authority e $resourceUrl.

   ```console
   *** Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
   Applying Template ID bb7ed207-046a-4caf-9826-647cff56b990 to:
   <Sample-Text>
   Encrypted Text :y¬╩$Ops7Γ╢╖¢t
   Decrypting string:

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Decrypted Text :<Sample-Text>
   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
   Press any key to close this window . . .
   ```
