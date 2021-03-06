---
title: "Avvio rapido: Elencare i modelli di protezione disponibili per l'utente autenticato in un tenant di Microsoft Information Protection (MIP) usando l'SDK C++ di MIP"
description: Argomento di avvio rapido che illustra come usare l'API Protezione di Microsoft Information Protection C++ SDK per elencare i modelli di protezione disponibili per l'utente (C++)
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 62f694248da10c7663c551240b204711b52163d5
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865072"
---
# <a name="quickstart-list-protection-templates-c"></a>Guida introduttiva: Elencare i modelli di protezione (C++)

Questo Avvio rapido illustra come usare l'API Protezione di MIP per i modelli di protezione disponibili per l'utente.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare l'[Avvio rapido: Inizializzazione delle applicazioni client - API Protezione (C++)](quick-protection-app-initialization-cpp.md) che compila una soluzione Visual Studio iniziale. L'Avvio rapido "Elencare i modelli di protezione" si basa sull'Avvio rapido precedente per la creazione corretta della soluzione iniziale.
- Facoltativamente: Esaminare i concetti in [Modelli RMS](/azure/information-protection/configure-policy-templates).

## <a name="add-logic-to-list-the-protection-templates"></a>Aggiungere la logica per elencare i modelli di protezione

Aggiungere la logica per elencare i modelli di protezione disponibili per un utente, usando l'oggetto motore Protezione.

1. Aprire la soluzione di Visual Studio creata nell'articolo precedente "Avvio rapido: Inizializzazione delle applicazioni client - API Protezione (C++).

2. Usare **Esplora soluzioni** per aprire il file con estensione cpp nel progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Aggiungere la direttiva `using` seguente dopo `using mip::ProtectionEngine;`, vicino all'inizio del file:

   ```cpp
   using std::endl;
   ```

4. Verso la fine del corpo `main()`, dopo la parentesi graffa di chiusura `}` dell'ultimo blocco `catch` e prima di `return 0;` (il punto in cui è stata interrotto l'Avvio rapido precedente), inserire il codice seguente:

   ```cpp
    // List protection templates
    const shared_ptr<ProtectionEngineObserver> engineObserver = std::make_shared<ProtectionEngineObserver>();
    // Create a context to pass to 'ProtectionEngine::GetTemplateListAsync'. That context will be forwarded to the
    // corresponding ProtectionEngine::Observer methods. In this case, we use promises/futures as a simple way to detect
    // the async operation completes synchronously.
    auto loadPromise = std::make_shared<std::promise<vector<shared_ptr<mip::TemplateDescriptor>>>>();
    std::future<vector<shared_ptr<mip::TemplateDescriptor>>> loadFuture = loadPromise->get_future();
    engine->GetTemplatesAsync(engineObserver, loadPromise);
    auto templates = loadFuture.get();

    cout << "**_ Template List: " << endl;

    for (const auto& protectionTemplate : templates) {
        cout << "Name: " << protectionTemplate->GetName() << " : " << protectionTemplate->GetId() << endl;
    }

   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>Creare uno script di PowerShell per generare i token di accesso

Usare lo script PowerShell seguente per generare i token di accesso, richiesti dal SDK nell'implementazione `AuthDelegateImpl::AcquireOAuth2Token`. Lo script usa il cmdlet `Get-ADALToken` dal modulo ADAL.PS installato in precedenza, in "Installazione e configurazione di MIP SDK".

1. Creare un file di script di PowerShell (con estensione ps1) e copiare e incollare lo script seguente nel file:

   - I valori `$authority` e `$resourceUrl` vengono aggiornati più avanti, nella sezione seguente.
   - Aggiornare `$appId` e `$redirectUri` in modo che corrispondano ai valori specificati nella registrazione dell'app in Azure AD.

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '<app-ID>'                              # App ID of the Azure AD app registration
   $redirectUri = '<redirect-uri>'                  # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. Salvare il file di script per poterlo eseguire in seguito, quando richiesto dall'applicazione client.

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Infine, compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (_*Compila soluzione **) per compilare l'applicazione client. Se non si registrano errori di compilazione, usare F5 (** Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione richiede un token di accesso ogni volta che il SDK chiama il metodo `AcquireOAuth2Token()`. È possibile riutilizzare un token generato in precedenza, se viene richiesto più volte e i valori necessari sono uguali:

3. Per generare un token di accesso per il prompt tornare allo script di PowerShell e:

   - Aggiornare le variabili `$authority` e `$resourceUrl`. Devono corrispondere ai valori specificati nell'output della console nel passaggio 2.
   - Eseguire lo script di PowerShell. Il cmdlet `Get-ADALToken` attiva una richiesta di autenticazione di Azure AD simile all'esempio seguente. Specificare lo stesso account specificato nell'output della console nel passaggio 2. Dopo l'accesso, il token di accesso verrà inserito negli Appunti.

     [![Accesso per l'acquisizione del token in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Potrebbe anche essere necessario dare il consenso, per permettere all'applicazione di accedere alle API MIP mentre viene eseguita con l'account di accesso. Ciò si verifica quando non è già stato dato il consenso per la registrazione dell'applicazione in Azure AD (come descritto in "Installazione e configurazione di MIP SDK") o si accede con un account da un tenant diverso da quello in cui è registrata l'applicazione. È sufficiente fare clic su **Accetta** per registrare il consenso.

     [![Consenso in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. Dopo aver incollato il token di accesso nella richiesta del passaggio 2, l'output della console indica i modelli di protezione, in modo simile all'esempio seguente:

   ```console
   **_ Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720

   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.

   Press any key to continue . . .
   ```

   > [!NOTE]
   > Copiare e salvare l'ID di uno o più dei modelli di protezione (ad esempio `f42a3342-8706-4288-bd31-ebb85995028z`), perché verranno usati nell'Avvio rapido successivo.

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione dell'applicazione C++

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| Token di accesso non valido | _An exception occurred... is the access token incorrect/expired?<br><br>Failed API call: profile_add_engine_async Failed with: [class mip::PolicySyncException] Failed acquiring policy, Request failed with http status code: 401, x-ms-diagnostics: [2000001;reason="OAuth token submitted with the request cannot be parsed.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) exited with code 0.<br><br>Press any key to close this window . . .* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il token nel metodo `AcquireOAuth2Token()` sia non valido o scaduto. Tornare a [Creare uno script di PowerShell per generare i token di accesso](#create-a-powershell-script-to-generate-access-tokens) e rigenerare il token di accesso, aggiornare di nuovo `AcquireOAuth2Token()` e ricompilare o eseguire di nuovo il test. È anche possibile esaminare e verificare il token e le relative attestazioni usando l'applicazione Web a pagina singola [jwt.ms](https://jwt.ms/). |

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come elencare i modelli di protezione disponibili per un utente autenticato, provare l'Avvio rapido successivo:

> [!div class="nextstepaction"]
> [Crittografare e decrittografare il testo](quick-protection-encrypt-decrypt text-cpp.md)