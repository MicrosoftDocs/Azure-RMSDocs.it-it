---
title: Guida introduttiva - inizializzazione per Microsoft Information Protection (MIP) SDK C# i client
description: Una Guida introduttiva che illustra come scrivere la logica di inizializzazione per un SDK di Microsoft Information Protection (MIP) C# applicazioni client.
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 7efaaba799afa01b07a5eefc0b6798983cc590d2
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652371"
---
# <a name="quickstart-client-application-initialization-c"></a>Guida introduttiva: Inizializzazione dell'applicazione client (C#)

Questa Guida introduttiva spiega come implementare il modello di inizializzazione client, utilizzato dal wrapper MIP SDK .NET in fase di esecuzione.

> [!NOTE]
> I passaggi descritti in questa Guida introduttiva sono necessari per qualsiasi applicazione client che utilizza il File o le API dei criteri del wrapper .NET MIP. L'API di protezione non è ancora disponibile. Sebbene questa guida introduttiva illustri l'utilizzo delle API File, lo stesso modello è applicabile ai client che usano le API Criteri e Protezione. Le guide introduttive successive devono essere eseguite in sequenza, perché ognuna è basata sulla precedente e questa è la prima.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, assicurarsi di:

- Completare i passaggi descritti in [Installazione e configurazione di Microsoft Information Protection (MIP) SDK](setup-configure-mip.md). La guida introduttiva "Inizializzazione delle applicazioni client" si basa sull'installazione e la configurazione corrette dell'SDK.
- Se lo si desidera:
  - Vedere [Oggetti profilo e motore](concept-profile-engine-cpp.md). Gli oggetti profilo e motore sono concetti universali, necessari per i client che usano le API File, Criteri e Protezione di MIP. 
  - Vedere [Concetti relativi all'autenticazione](concept-authentication-cpp.md) per informazioni su come vengono implementati l'autenticazione e il consenso dall'SDK e dalle applicazioni client.

## <a name="create-a-visual-studio-solution-and-project"></a>Creare una soluzione e un progetto di Visual Studio

Verranno prima di tutto creati e configurati la soluzione e il progetto iniziali di Visual Studio su cui si baseranno le altre guide introduttive.

1. Aprire Visual Studio 2017 e scegliere **File**, **Nuovo**, **Progetto** dal menu. Nella finestra di dialogo **Nuovo progetto**:
   - Nel riquadro sinistro, sotto **Installed**, **Visual C#** , selezionare **Desktop di Windows**.
   - Nel riquadro centrale selezionare **App Console (.NET Framework)**
   - Nel riquadro inferiore, aggiornare **Nome** e **Posizione** del progetto, nonché il **Nome della soluzione** in cui è contenuto corrispondentemente.
   - Al termine fare clic sul pulsante **OK** in basso a destra. 

     [![Creazione di una soluzione Visual Studio](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. Aggiungere il pacchetto NuGet per l'API File di MIP SDK al progetto:
   - In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto (subito sotto il nodo della soluzione principale) e scegliere **Gestisci pacchetti NuGet**:
   - Quando viene aperta la scheda **Gestione pacchetti NuGet** nell'area delle schede Gruppo di editor:
     - Selezionare **Sfoglia**.
     - Immettere "Microsoft.InformationProtection" nella casella di ricerca.
     - Selezionare il pacchetto "Microsoft.InformationProtection.File".
     - Fare clic su "Installa" e quindi su "OK" quando viene visualizzata la finestra di dialogo di conferma **Anteprima modifiche**.

3. Ripetere i passaggi precedenti per aggiungere il pacchetto dell'API File di MIP SDK, ma invece di aggiungere "ActiveDirectory" all'applicazione.

## <a name="implement-an-authentication-delegate"></a>Implementare un delegato di autenticazione

MIP SDK implementa l'autenticazione usando l'estensibilità delle classi, che rende disponibile un meccanismo per condividere le operazioni di autenticazione con l'applicazione client. Il client deve acquisire un token di accesso OAuth2 adatto e fornirlo a MIP SDK in fase di esecuzione.

Creare ora un'implementazione di un delegato, l'autenticazione mediante l'estensione del SDK `Microsoft.InformationProtection.IAuthDelegate` interfaccia e si esegue l'override o implementa il `IAuthDelegate.AcquireToken()` funzione virtuale. Delegato dell'autenticazione viene creata un'istanza e utilizzato in un secondo momento dal `FileProfile` e `FileEngine` oggetti.

1. Fare clic sul nome del progetto in Visual Studio, selezionare **Add** quindi **classe**.
2. Immettere "AuthDelegateImplementation" i **nome** campo. Fare clic su **Aggiungi**.
3. Aggiungere istruzioni using per Active Directory Authentication Library (ADAL) e la libreria di MIP:

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     ```

4. Impostare `AuthDelegateImplementation` ereditare `Microsoft.InformationProtection.IAuthDelegate` e l'implementazione di una variabile privata di `Microsoft.InformationProtection.ApplicationInfo` e un costruttore che accetta lo stesso tipo.

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
     {
        private ApplicationInfo _appInfo;
        private string redirectUri = "mip-sdk-app://authorize";
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }
     }
     ```

Il `ApplicationInfo` oggetto contiene due proprietà. Il `_appInfo.ApplicationId` verrà usato nel `AuthDelegateImplementation` classe per fornire l'ID client per la libreria di autenticazione.

5. Aggiungere il `public string AcquireToken()` classe. Questa classe deve accettare `Microsoft.InformationProtection.Identity`e due stringhe: autorità e risorse. Queste variabili di stringa verranno passate per la libreria di autenticazione dall'API e non devono essere modificate. La modifica può comportare errori di autenticazione.

     ```csharp
     public string AcquireToken(Identity identity, string authority, string resource)
     {
          AuthenticationContext authContext = new AuthenticationContext(authority);
          var result = authContext.AcquireTokenAsync(resource, _appInfo.ApplicationId, new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, null), UserIdentifier.AnyUser).Result;
          return result.AccessToken;
     }
     ```

## <a name="implement-a-consent-delegate"></a>Implementare un delegato di consenso

Creare ora un'implementazione per un delegato di consenso dell'utente, mediante l'estensione del SDK `Microsoft.InformationProtection.IConsentDelegate` interfaccia e l'implementazione di override/`GetUserConsent()`. In seguito si creerà un'istanza del delegato di consenso che verrà usata dagli oggetti profilo e motore dell'API File. Il delegato di consenso viene fornito con l'indirizzo del servizio l'utente deve fornire il consenso all'uso in di `url` parametro. Il delegato deve in genere forniscono un flusso che consente all'utente di accettare o rifiutare per fornire il consenso per l'accesso al servizio. Per questo livello di codice di avvio rapido `Consent.Accept`.

1. Usando la stessa funzionalità "Aggiungi classe" di Visual Studio usata in precedenza, aggiungere un'altra classe al progetto. Questa volta, immettere "ConsentDelegateImplementation" nel **nome della classe** campo. 

2. A questo punto aggiornare **ConsentDelegateImpl.cs** per implementare la nuova classe di consenso dell'utente delegato. Aggiungere l'usando informativa `Microsoft.InformationProtection` e impostare la classe per ereditare `IConsentDelegate`.

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. Facoltativamente, provare a compilare la soluzione per verificare se viene compilato senza errori.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Inizializzare il Wrapper gestito MIP SDK

1. Dal **Esplora soluzioni**, aprire il file con estensione cs del progetto che contiene l'implementazione del `Main()` (metodo). Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Rimuovere l'implementazione generata di `main()`. 

3. Il wrapper gestito include una classe statica, `Microsoft.InformationProtection.MIP` utilizzato per l'inizializzazione, il caricamento di profili e il rilascio delle risorse. Per inizializzare il wrapper per le operazioni API file, chiamare MIP. Initialize, passando `MipComponent.File` per caricare le librerie necessarie per operazioni su file. 

4. Nelle `Main()` nelle *Program.cs* aggiungere quanto segue, sostituendo **\<application-id\>** con l'ID di registrazione dell'applicazione AD Azure creata in precedenza.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for File API operations 
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>Creare un profilo di File e il motore

Come accennato, sono richiesti per i client SDK tramite MIP APIs oggetti del profilo e il motore. Completare la scrittura di codice parte di questa Guida introduttiva, aggiungendo il codice per caricare le DLL native, quindi creare gli oggetti del profilo e il motore.

   ```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               //Initialize Wrapper for File API operations
               MIP.Initialize(MipComponent.File);

               //Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               //Instatiate the AuthDelegateImpl object, passing in AppInfo. 
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               //Initialize and instantiate the File Profile
               //Create the FileProfileSettings object
               var profileSettings = new FileProfileSettings("mip_data", false, authDelegate, new ConsentDelegateImplementation(), appInfo, LogLevel.Trace);

               //Load the Profile async and wait for the result
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               //Create a FileEngineSettings object, then use that to add an engine to the profile
               var engineSettings = new FileEngineSettings("user1@tenant.com", "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;
          }
     }
}
``` 

3. Sostituire i valori segnaposto nel codice sorgente incollata, usando i valori seguenti:

   | Segnaposto | Value | Esempio |
   |:----------- |:----- |:--------|
   | \<application-id\> | ID di applicazione Azure AD assegnato all'applicazione registrata in "Installazione e configurazione di MIP SDK" (2 istanze).  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | Nome descrittivo definito dall'utente per l'applicazione. | AppInitialization |


4. Eseguire ora la compilazione finale dell'applicazione e risolvere gli eventuali errori. Il codice dovrebbe essere compilato correttamente.

## <a name="next-steps"></a>Passaggi successivi

Ora che il codice di inizializzazione è completo, si è pronti per la guida introduttiva successiva, in cui si inizieranno a provare le API File MIP.

> [!div class="nextstepaction"]
> [Elencare le etichette di riservatezza](quick-file-list-labels-csharp.md)
