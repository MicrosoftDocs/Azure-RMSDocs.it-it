---
title: Guida introduttiva - Elenca le etichette di riservatezza in un tenant di Microsoft Information Protection (MIP) tramite Microsoft Information Protection SDK C# Wrapper
description: Una Guida introduttiva che illustra come usare il SDK di Microsoft Information Protection C# wrapper per elencare le etichette di riservatezza nel tenant.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: mbaldwin
ms.openlocfilehash: 0b1b110fe3b2e96c258c7b94a3d356b9404d6e7e
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809744"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Guida introduttiva: Elencare le etichette di riservatezza (C#)

Questa Guida introduttiva illustra come usare l'API di File MIP SDK per elencare le etichette di riservatezza configurate per l'organizzazione.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, completare i prerequisiti seguenti prima di continuare:

- Completa [Guida introduttiva: Inizializzazione dell'applicazione client (C#)](quick-app-initialization-csharp.md) first, che compila una soluzione di Visual Studio starter. Questa guida introduttiva "Elencare le etichette di riservatezza" si basa su quella precedente per la creazione corretta della soluzione iniziale.
- Se lo si desidera: Revisione [le etichette di classificazione](concept-classification-labels.md) concetti.

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Aggiungere la logica per elencare le etichette di riservatezza

Aggiungere la logica per elencare le etichette di riservatezza dell'organizzazione, usando l'oggetto motore dell'API File. 

1. Aprire la soluzione di Visual Studio è stato creato nella precedente "Guida introduttiva: Inizializzazione dell'applicazione client (C#) "articolo.

2. Usando **Esplora soluzioni**, aprire il file con estensione cs del progetto che contiene l'implementazione del `Main()` (metodo). Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto. 

3. Verso la fine del `Main()` corpo, sotto la parentesi graffa di chiusura `}` del `Main()` funzione (in cui è stata interrotta nella Guida introduttiva precedente), inserire il codice seguente:

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

1. Usare CTRL + MAIUSC + B (**Compila soluzione**) per compilare l'applicazione client. Se non si registrano errori di compilazione, premere F5 (**Avvia debug**) per eseguire l'applicazione.

2. Se il progetto compilato ed eseguito correttamente, l'applicazione *potrebbe* prompt dei comandi per l'autenticazione tramite la libreria ADAL ogni volta che il SDK chiama la `AcquireToken()` (metodo). Se esistono già credenziali memorizzate nella cache, non verrà richiesto di accedere e visualizzare l'elenco delle etichette. 

     [![Accesso per l'acquisizione del token in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Potrebbe anche essere necessario dare il consenso, per permettere all'applicazione di accedere alle API MIP mentre viene eseguita con l'account di accesso. Ciò si verifica quando non è già stato dato il consenso per la registrazione dell'applicazione in Azure AD (come descritto in "Installazione e configurazione di MIP SDK") o si accede con un account da un tenant diverso da quello in cui è registrata l'applicazione. È sufficiente fare clic su **Accetta** per registrare il consenso.

     [![Consenso in Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Dopo l'autenticazione, l'output della console dovrebbe mostrare le etichette di riservatezza, simile all'esempio seguente:

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

### <a name="problems-during-execution-of-c-application"></a>Problemi durante l'esecuzione di C# dell'applicazione

| Riepilogo | Messaggio di errore | Soluzione |
|---------|---------------|----------|
| Token di accesso non valido | *Si è verificata un'eccezione... è il token di accesso errato/scaduti? <br> <br>Chiamata API non è riuscita: non è riuscita profile_add_engine_async con: l'acquisizione dei criteri non riuscite [classe mip::PolicySyncException], richiesta non è riuscita con codice di stato http: 401, x-ms-diagnostics: [2000001; motivo = "token OAuth inviato con la richiesta non può essere analizzato."; error_category = "invalid_token"], ID correlazione: [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processo 29924) terminato con codice 0.<br> <br>Premere un tasto qualsiasi per chiudere questa finestra...* | Se il progetto viene compilato correttamente, ma viene visualizzato un output simile a quello riportato a sinistra, è probabile che il token nel metodo `AcquireOAuth2Token()` sia non valido o scaduto. Tornare alla [compilare e testare l'applicazione](#build-and-test-the-application) e rigenerare l'aggiornamento, token di accesso `AcquireOAuth2Token()` anche in questo caso e ricompilazione o eseguire nuovamente il test. È anche possibile esaminare e verificare il token e le relative attestazioni usando l'applicazione Web a pagina singola [jwt.ms](https://jwt.ms/). |
| Le etichette di riservatezza non sono configurate | n/d | Se il progetto viene compilato correttamente, ma non è presente alcun output nella finestra della console, verificare che le etichette di riservatezza dell'organizzazione siano configurate correttamente. Vedere [Installazione e configurazione di MIP SDK](setup-configure-mip.md) per informazioni dettagliate sulle impostazioni per la protezione e la tassonomia delle etichette.  |

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come elencare le etichette di riservatezza per l'organizzazione, provare la guida introduttiva successiva:

> [!div class="nextstepaction"]
> [Impostare e ottenere un'etichetta di riservatezza](quick-file-set-get-label-csharp.md)
