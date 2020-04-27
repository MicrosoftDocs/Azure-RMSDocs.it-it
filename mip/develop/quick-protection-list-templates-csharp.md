---
title: "Avvio rapido: Elencare i modelli di protezione disponibili per l'utente autenticato in un tenant di Microsoft Information Protection (MIP) usando il wrapper C# SDK di MIP"
description: Avvio rapido che illustra come usare il wrapper C# dell'API Protezione SDK di Microsoft Information Protection per elencare i modelli di protezione disponibili per l'utente.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 0a71ac710aec82c7a5de16c7f603ccdfe4803f79
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766304"
---
# <a name="quickstart-list-templates-c"></a>Guida introduttiva: Elencare i modelli (C#)

Questo Avvio rapido illustra come usare l'API Protezione SDK di MIP per elencare i modelli di protezione disponibili per l'utente.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Inizializzazione delle applicazioni client - API Protezione (C#)](quick-protection-app-initialization-csharp.md) per compilare una soluzione Visual Studio iniziale. L'Avvio rapido "Elencare i modelli di protezione" si basa sull'Avvio rapido precedente per la creazione corretta della soluzione iniziale.
- Facoltativamente: Esaminare i concetti in [Modelli RMS](https://docs.microsoft.com/azure/information-protection/configure-policy-templates). 

## <a name="add-logic-to-list-the-protection-templates"></a>Aggiungere la logica per elencare i modelli di protezione

Aggiungere la logica per elencare i modelli di protezione disponibili per un utente, usando l'oggetto motore Protezione.

1. Aprire la soluzione di Visual Studio creata nell'articolo precedente "Avvio rapido: Inizializzazione delle applicazioni client - API Protezione (C#).

2. Usare **Esplora soluzioni** per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

3. Verso la fine del corpo `Main()`, sopra la sezione dell'arresto dell'applicazione della funzione `Main()`, nel punto in cui è stata interrotta la procedura di Avvio rapido precedente, inserire il codice seguente:

  ```csharp
  // List protection templates using protectionEngine and display the list  
  
  var templates=protectionEngine.GetTemplates();

  for(int i = 0; i < templates.Count; i++)
  {
      Console.WriteLine("{0}: {1}", i.ToString(), templates[i].Name + " : " + templates[i].Id);
  }
  
  Console.WriteLine("Press a key to continue...");
  ```

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Infine, compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione *potrebbe* richiedere l'autenticazione tramite ADAL ogni volta che il SDK chiama il metodo `AcquireToken()`. Se esistono già credenziali memorizzate, nella cache non verrà richiesto di eseguire l'accesso e visualizzare l'elenco delle etichette.

     [![Accesso per l'acquisizione del token in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox) 

   - Potrebbe anche essere necessario dare il consenso, per permettere all'applicazione di accedere alle API MIP mentre viene eseguita con l'account di accesso. Ciò si verifica quando non è già stato dato il consenso per la registrazione dell'applicazione in Azure AD (come descritto in "Installazione e configurazione di MIP SDK") o si accede con un account da un tenant diverso da quello in cui è registrata l'applicazione. È sufficiente fare clic su **Accetta** per registrare il consenso.

     [![Consenso in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Dopo l'autenticazione l'output della console visualizzerà i modelli di protezione per l'utente autenticato, in modo simile all'esempio seguente:

  ```console
  0: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
  1: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
  2: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
  3: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
  Press a key to continue.
  ```

   > [!NOTE]
   > Copiare e salvare l'ID di uno o più dei modelli di protezione (ad esempio `bb7ed207-046a-4caf-9826-647cff56b990`), perché verranno usati nell'Avvio rapido successivo.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione dell'applicazione C#

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| Token di accesso non valido | *An exception occurred... is the access token incorrect/expired?<br><br>Failed API call: profile_add_engine_async Failed with: [class mip::PolicySyncException] Failed acquiring policy, Request failed with http status code: 401, x-ms-diagnostics: [2000001;reason="OAuth token submitted with the request cannot be parsed.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) exited with code 0.<br><br>Press any key to close this window . . .* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il token nel metodo `AcquireOAuth2Token()` sia non valido o scaduto. Tornare a [Compilare e testare l'applicazione](#build-and-test-the-application) e rigenerare il token di accesso, aggiornare di nuovo `AcquireOAuth2Token()`, quindi ripetere compilazione e test. È anche possibile esaminare e verificare il token e le relative attestazioni usando l'applicazione Web a pagina singola [jwt.ms](https://jwt.ms/). |

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come elencare i modelli di protezione disponibili per l'utente autenticato, provare l'Avvio rapido successivo:

> [!div class="nextstepaction"]
> [Avvio rapido: Crittografare e decrittografare il testo](quick-protection-encrypt-decrypt-text-csharp.md)
