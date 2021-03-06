---
title: Guida introduttiva - Elencare le etichette di riservatezza in un tenant di Microsoft Information Protection (MIP) con MIP SDK per C++
description: Questa guida introduttiva mostra come usare Microsoft Information Protection SDK per C++ per elencare le etichette di riservatezza nel tenant.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 14b36ecee7fc49c5b50d627e6ef1ab95d436d7ee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865264"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Guida introduttiva: Elencare le etichette di riservatezza (C++)

Questa guida introduttiva illustra come usare l'API File MIP per elencare le etichette di riservatezza configurate per l'organizzazione.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Inizializzazione delle applicazioni client (C++)](quick-app-initialization-cpp.md) per creare una soluzione Visual Studio iniziale. Questa guida introduttiva "Elencare le etichette di riservatezza" si basa su quella precedente per la creazione corretta della soluzione iniziale.
- Facoltativamente: vedere i concetti relativi alle [etichette di classificazione](concept-classification-labels.md).

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Aggiungere la logica per elencare le etichette di riservatezza

Aggiungere la logica per elencare le etichette di riservatezza dell'organizzazione, usando l'oggetto motore dell'API File.

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Inizializzazione dell'applicazione client (C++)".

2. Usare **Esplora soluzioni** per aprire il file con estensione cpp nel progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Aggiungere la direttiva `using` seguente dopo `using mip::FileEngine;`, vicino all'inizio del file:

   ```cpp
   using std::endl;
   ```

4. Verso la fine del corpo `main()`, dopo la parentesi graffa di chiusura `}` dell'ultimo blocco `catch` e prima di `return 0;` (il punto in cui è stata interrotto l'Avvio rapido precedente), inserire il codice seguente:

   ```cpp
   // List sensitivity labels
   cout << "\nSensitivity labels for your organization:\n";
   auto labels = engine->ListSensitivityLabels();
   for (const auto& label : labels)
   {
      cout << label->GetName() << " : " << label->GetId() << endl;

      for (const auto& child : label->GetChildren())
      {
        cout << "->  " << child->GetName() << " : " << child->GetId() << endl;
      }
   }
   system("pause");
   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>Creare uno script di PowerShell per generare i token di accesso

Usare lo script PowerShell seguente per generare i token di accesso, richiesti dal SDK nell'implementazione `AuthDelegateImpl::AcquireOAuth2Token`. Lo script usa il cmdlet `Get-ADALToken` dal modulo ADAL.PS installato in precedenza, in "Installazione e configurazione di MIP SDK".

1. Creare un file di script di PowerShell (con estensione ps1) e copiare e incollare lo script seguente nel file:

   - I valori `$authority` e `$resourceUrl` vengono aggiornati più avanti, nella sezione seguente.
   - Aggiornare `$appId` e `$redirectUri` in modo che corrispondano ai valori specificati nella registrazione dell'app in Azure AD.

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. Salvare il file di script per poterlo eseguire in seguito, quando richiesto dall'applicazione client.

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Infine, compilare e testare l'applicazione client.

1. Usare F6 (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione richiede un token di accesso ogni volta che il SDK chiama il metodo `AcquireOAuth2Token()`. È possibile riutilizzare un token generato in precedenza, se viene richiesto più volte e i valori necessari sono uguali.

3. Per generare un token di accesso per il prompt tornare allo script di PowerShell e:

   - Aggiornare le variabili `$authority` e `$resourceUrl`. Devono corrispondere ai valori specificati nell'output della console nel passaggio 2. Questi valori vengono forniti da MIP SDK nel parametro `challenge` di `AcquireOAuth2Token()`:
   - Eseguire lo script di PowerShell. Il cmdlet `Get-ADALToken` attiva una richiesta di autenticazione di Azure AD simile all'esempio seguente. Specificare lo stesso account specificato nell'output della console nel passaggio 2. Dopo l'accesso, il token di accesso verrà inserito negli Appunti.

     [![Accesso per l'acquisizione del token in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Potrebbe anche essere necessario dare il consenso, per permettere all'applicazione di accedere alle API MIP mentre viene eseguita con l'account di accesso. Ciò si verifica quando non è già stato dato il consenso per la registrazione dell'applicazione in Azure AD (come descritto in "Installazione e configurazione di MIP SDK") o si accede con un account da un tenant diverso da quello in cui è registrata l'applicazione. È sufficiente fare clic su **Accetta** per registrare il consenso.

     [![Consenso in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. Dopo aver incollato il token di accesso nella richiesta del passaggio 2, l'output della console mostra le etichette di riservatezza, in modo simile all'esempio seguente:

   ```console
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z

   Press any key to continue . . .
   ```

   > [!NOTE]
   > Copiare e salvare l'ID di una o più delle etichette di riservatezza (ad esempio, `f42a3342-8706-4288-bd31-ebb85995028z`), perché verranno usati nella guida introduttiva successiva.

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione dell'applicazione C++

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| Token di accesso non valido | *An exception occurred... is the access token incorrect/expired?<br><br>Failed API call: profile_add_engine_async Failed with: [class mip::PolicySyncException] Failed acquiring policy, Request failed with http status code: 401, x-ms-diagnostics: [2000001;reason="OAuth token submitted with the request cannot be parsed.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) exited with code 0.<br><br>Press any key to close this window . . .* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il token nel metodo `AcquireOAuth2Token()` sia non valido o scaduto. Tornare a [Creare uno script di PowerShell per generare i token di accesso](#create-a-powershell-script-to-generate-access-tokens) e rigenerare il token di accesso, aggiornare di nuovo `AcquireOAuth2Token()` e ricompilare o eseguire di nuovo il test. È anche possibile esaminare e verificare il token e le relative attestazioni usando l'applicazione Web a pagina singola [jwt.ms](https://jwt.ms/). |
| Le etichette di riservatezza non sono configurate | n/d | Se il progetto viene compilato correttamente, ma non è presente alcun output nella finestra della console, verificare che le etichette di riservatezza dell'organizzazione siano configurate correttamente. Vedere [Installazione e configurazione di MIP SDK](setup-configure-mip.md) per informazioni dettagliate sulle impostazioni per la protezione e la tassonomia delle etichette.  |

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come elencare le etichette di riservatezza per l'organizzazione, provare la guida introduttiva successiva:

> [!div class="nextstepaction"]
> [Impostare e ottenere un'etichetta di riservatezza](quick-file-set-get-label-cpp.md)
