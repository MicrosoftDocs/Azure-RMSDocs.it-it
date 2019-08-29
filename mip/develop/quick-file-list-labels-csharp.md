---
title: 'Avvio rapido: Elencare le etichette di riservatezza in un tenant di Microsoft Information Protection (MIP) con il wrapper C# del SDK di MIP'
description: Questa procedura di avvio rapido illustra come usare il wrapper C# del SDK di Microsoft Information Protection per elencare le etichette di riservatezza nel tenant.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 3a26352f7b8e23e2de55eb21846e20feca7096ff
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885980"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Guida introduttiva: Elencare le etichette di riservatezza (C#)

Questo Avvio rapido illustra come usare l'API File del SDK di MIP per elencare le etichette di riservatezza configurate per l'organizzazione.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- In primo luogo completare [Avvio rapido: Inizializzazione delle applicazioni client (C#)](quick-app-initialization-csharp.md) per creare una soluzione Visual Studio iniziale. Questa guida introduttiva "Elencare le etichette di riservatezza" si basa su quella precedente per la creazione corretta della soluzione iniziale.
- Facoltativamente: vedere i concetti relativi alle [etichette di classificazione](concept-classification-labels.md).

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Aggiungere la logica per elencare le etichette di riservatezza

Aggiungere la logica per elencare le etichette di riservatezza dell'organizzazione, usando l'oggetto motore dell'API File. 

1. Aprire la soluzione Visual Studio creata nell'articolo precedente "Avvio rapido: Inizializzazione dell'applicazione client (C#)".

2. Usare **Esplora soluzioni** per aprire il file con estensione cs nel progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto. 

3. Verso la fine del corpo `Main()`, sopra la sezione dell'arresto dell'applicazione della funzione `Main()` (nel punto in cui è stata interrotta la procedura di Avvio rapido precedente), inserire il codice seguente:

  ```csharp
  // List sensitivity labels from fileEngine and display name and id  
  foreach(var label in fileEngine.SensitivityLabels)
  {
      Console.WriteLine(string.Format("{0} : {1}", label.Name, label.Id));

      if (label.Children.Count != 0)
      {
          foreach (var child in label.Children)
          {
              Console.WriteLine(string.Format("{0}{1} : {2}", "\t",child.Name, child.Id));
          }
      }
  }
  ```

## <a name="build-and-test-the-application"></a>Compilare e testare l'applicazione

Infine, compilare e testare l'applicazione client.

1. Usare CTRL+MAIUSC+B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto viene compilato ed eseguito correttamente, l'applicazione *potrebbe* richiedere l'autenticazione tramite ADAL ogni volta che il SDK chiama il metodo `AcquireToken()`. Se esistono già credenziali memorizzate, nella cache non verrà richiesto di eseguire l'accesso e visualizzare l'elenco delle etichette. 

     [![Accesso per l'acquisizione del token in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Potrebbe anche essere necessario dare il consenso, per permettere all'applicazione di accedere alle API MIP mentre viene eseguita con l'account di accesso. Ciò si verifica quando non è già stato dato il consenso per la registrazione dell'applicazione in Azure AD (come descritto in "Installazione e configurazione di MIP SDK") o si accede con un account da un tenant diverso da quello in cui è registrata l'applicazione. È sufficiente fare clic su **Accetta** per registrare il consenso.

     [![Consenso in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Dopo l'autenticazione l'output della console visualizza le etichette di riservatezza, in modo simile all'esempio seguente:

  ```console
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.
  ```

   > [!NOTE]
   > Copiare e salvare l'ID di una o più delle etichette di riservatezza (ad esempio, `f42a3342-8706-4288-bd31-ebb85995028z`), perché verranno usati nella guida introduttiva successiva.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione dell'applicazione C#

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| Token di accesso non valido | *An exception occurred... is the access token incorrect/expired?<br><br>Failed API call: profile_add_engine_async Failed with: [class mip::PolicySyncException] Failed acquiring policy, Request failed with http status code: 401, x-ms-diagnostics: [2000001;reason="OAuth token submitted with the request cannot be parsed.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) exited with code 0.<br><br>Press any key to close this window . . .* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il token nel metodo `AcquireOAuth2Token()` sia non valido o scaduto. Tornare a [Compilare e testare l'applicazione](#build-and-test-the-application) e rigenerare il token di accesso, aggiornare di nuovo `AcquireOAuth2Token()`, quindi ripetere compilazione e test. È anche possibile esaminare e verificare il token e le relative attestazioni usando l'applicazione Web a pagina singola [jwt.ms](https://jwt.ms/). |
| Le etichette di riservatezza non sono configurate | n/d | Se il progetto viene compilato correttamente, ma non è presente alcun output nella finestra della console, verificare che le etichette di riservatezza dell'organizzazione siano configurate correttamente. Vedere [Installazione e configurazione di MIP SDK](setup-configure-mip.md) per informazioni dettagliate sulle impostazioni per la protezione e la tassonomia delle etichette.  |

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come elencare le etichette di riservatezza per l'organizzazione, provare la guida introduttiva successiva:

> [!div class="nextstepaction"]
> [Impostare e ottenere un'etichetta di riservatezza](quick-file-set-get-label-csharp.md)
