---
title: 'Avvio rapido: Inizializzazione per i client del SDK C# di Microsoft Information Protection (MIP)'
description: Avvio rapido che illustra come scrivere la logica di inizializzazione per applicazioni client del SDK C# di Microsoft Information Protection (MIP).
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 5b64da83fad3ca9187398f77780fd0810740668a
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764186"
---
# <a name="quickstart-client-application-initialization-c"></a>Guida introduttiva: Inizializzazione dell'applicazione client (C#)

Questo Avvio rapido spiega come implementare il modello di inizializzazione client usato dal wrapper .NET del SDK MIP in fase di runtime.

> [!NOTE]
> I passaggi descritti in questo avvio rapido sono necessari per qualsiasi applicazione client che usa le API dei file o dei criteri del wrapper .NET di MIP. L'API di protezione non è ancora disponibile. Sebbene questa guida introduttiva illustri l'utilizzo delle API File, lo stesso modello è applicabile ai client che usano le API Criteri e Protezione. Le guide introduttive successive devono essere eseguite in sequenza, perché ognuna è basata sulla precedente e questa è la prima.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, assicurarsi di:

- Completare i passaggi descritti in [Installazione e configurazione di Microsoft Information Protection (MIP) SDK](setup-configure-mip.md). La guida introduttiva "Inizializzazione delle applicazioni client" si basa sull'installazione e la configurazione corrette dell'SDK.
- Facoltativamente:
  - Vedere [Oggetti profilo e motore](concept-profile-engine-cpp.md). Gli oggetti profilo e motore sono concetti universali, necessari per i client che usano le API File, Criteri e Protezione di MIP. 
  - Vedere [Concetti relativi all'autenticazione](concept-authentication-cpp.md) per informazioni su come vengono implementati l'autenticazione e il consenso dall'SDK e dalle applicazioni client.

## <a name="create-a-visual-studio-solution-and-project"></a>Creare una soluzione e un progetto di Visual Studio

Verranno prima di tutto creati e configurati la soluzione e il progetto iniziali di Visual Studio su cui si baseranno le altre guide introduttive.

1. Aprire Visual Studio 2017 e scegliere **File**, **Nuovo**, **Progetto** dal menu. Nella finestra di dialogo **Nuovo progetto**:
   - Nel riquadro a sinistra in **Installati**, **Visual C#** selezionare **Windows Desktop**.
   - Nel riquadro centrale selezionare **App console (.NET Framework)** .
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

3. Ripetere i passaggi precedenti per aggiungere il pacchetto dell'API File del SDK MIP, ma aggiungere invece "Microsoft.IdentityModel.Clients.ActiveDirectory" all'applicazione.

## <a name="implement-an-authentication-delegate"></a>Implementare un delegato di autenticazione

MIP SDK implementa l'autenticazione usando l'estensibilità delle classi, che rende disponibile un meccanismo per condividere le operazioni di autenticazione con l'applicazione client. Il client deve acquisire un token di accesso OAuth2 adatto e fornirlo a MIP SDK in fase di esecuzione.

Ora si creerà un'implementazione per un delegato di autenticazione mediante l'estensione dell'interfaccia `Microsoft.InformationProtection.IAuthDelegate` del SDK e l'override/implementazione della funzione virtuale `IAuthDelegate.AcquireToken()`. In seguito si creerà un'istanza del delegato di autenticazione che verrà usata dagli oggetti `FileProfile` e `FileEngine`.

1. Fare clic con il pulsante destro del mouse sul nome del progetto in Visual Studio, selezionare **Aggiungi** e quindi **Classe**.
2. Immettere "AuthDelegateImplementation" nel campo **Nome**. Fare clic su **Aggiungi**.
3. Aggiungere istruzioni using per Active Directory Authentication Library (ADAL) e la libreria MIP:

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     ```

4. Impostare `AuthDelegateImplementation` in modo che erediti `Microsoft.InformationProtection.IAuthDelegate` e implementi una variabile privata `Microsoft.InformationProtection.ApplicationInfo` e un costruttore che accetta lo stesso tipo.

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

L'oggetto `ApplicationInfo` contiene tre proprietà. `_appInfo.ApplicationId` verrà usata nella classe `AuthDelegateImplementation` per specificare l'ID client per la libreria di autenticazione. `ApplicationName` e `ApplicationVersion` saranno visualizzate nei report di analisi di Azure Information Protection Analytics.

5. Aggiungere il metodo `public string AcquireToken()`. Questo metodo accetterà `Microsoft.InformationProtection.Identity` e tre stringhe: URL dell'autorità, URI della risorsa e attestazioni, se necessario. Queste variabili stringa verranno passate alla libreria di autenticazione dall'API e non devono essere modificate. La modifica può provocare errori di autenticazione.

     ```csharp
     public string AcquireToken(Identity identity, string authority, string resource, string claims)
     {
          AuthenticationContext authContext = new AuthenticationContext(authority);
          var result = Task.Run(async() => await authContext.AcquireTokenAsync(resource, AppInfo.ApplicationId, new Uri(redirectUri), new PlatformParameters(PromptBehavior.Always))).Result;
          return result.AccessToken;
     }
     ```

## <a name="implement-a-consent-delegate"></a>Implementare un delegato di consenso

Si creerà ora un'implementazione per un delegato di consenso mediante l'estensione dell'interfaccia `Microsoft.InformationProtection.IConsentDelegate` del SDK e l'override/implementazione di `GetUserConsent()`. In seguito si creerà un'istanza del delegato di consenso che verrà usata dagli oggetti profilo e motore dell'API File. Il delegato di consenso viene fornito con l'indirizzo del servizio per il quale l'utente deve fornire il consenso tramite il parametro `url`. Il delegato fornisce in genere un flusso che consente all'utente di accettare o rifiutare il consenso per l'accesso al servizio. Per questo avvio rapido codificare `Consent.Accept`.

1. Usando la stessa funzionalità "Aggiungi classe" di Visual Studio usata in precedenza, aggiungere un'altra classe al progetto. Questa volta immettere "ConsentDelegateImplementation" nel campo **Nome classe**. 

2. A questo punto aggiornare **ConsentDelegateImpl.cs** per implementare la nuova classe del delegato di consenso. Aggiungere l'istruzione using per `Microsoft.InformationProtection` e impostare la classe in modo che erediti `IConsentDelegate`.

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. Facoltativamente provare a compilare la soluzione per verificare se viene compilata senza errori.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Inizializzare il wrapper gestito del SDK MIP

1. Da **Esplora soluzioni** aprire il file con estensione cs del progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Rimuovere l'implementazione generata di `main()`. 

3. Il wrapper gestito include una classe statica `Microsoft.InformationProtection.MIP` usata per l'inizializzazione, la creazione di `MipContext`, il caricamento di profili e il rilascio delle risorse. Per inizializzare il wrapper per le operazioni dell'API File chiamare `MIP.Initialize()`, passando `MipComponent.File` per caricare le librerie necessarie per le operazioni sui file. 

4. In `Main()` in *Program.cs* aggiungere quanto segue, sostituendo **\<application-id\>** con l'ID di registrazione dell'applicazione Azure AD creata in precedenza.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.File;
using Microsoft.InformationProtection.Protection;

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

## <a name="construct-a-file-profile-and-engine"></a>Costruire un profilo e un motore per il file

Come detto, gli oggetti profilo e motore sono necessari per i client del SDK che usano API MIP. Completare la parte di scrittura del codice di questo Avvio rapido aggiungendo il codice necessario per caricare le DLL native, quindi creare un'istanza degli oggetti profilo e motore.



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
               // Initialize Wrapper for File API operations.
               MIP.Initialize(MipComponent.File);

               // Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId.
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               // Instantiate the AuthDelegateImpl object, passing in AppInfo.
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               MipContext mipContext = MIP.CreateMipContext(appInfo,
                                        "mip_data",
                                        LogLevel.Trace,
                                        null,
                                        null);

               // Initialize and instantiate the File Profile.
               // Create the FileProfileSettings object.
               // Initialize file profile settings to create/use local state.
               var profileSettings = new FileProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,                                        
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               // Create a FileEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               fileEngine = null;
               fileProfile = null;
               mipContext = null;
          }
     }
}
```

3. Sostituire i valori segnaposto nel codice sorgente incollato, usando i valori seguenti:

   | Segnaposto | Valore | Esempio |
   |:----------- |:----- |:--------|
   | \<application-id\> | ID di applicazione Azure AD assegnato all'applicazione registrata in "Installazione e configurazione di MIP SDK" (2 istanze).  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | Nome descrittivo definito dall'utente per l'applicazione. | AppInitialization |


4. Eseguire ora la compilazione finale dell'applicazione e risolvere gli eventuali errori. Il codice verrà compilato correttamente.

## <a name="next-steps"></a>Passaggi successivi

Ora che il codice di inizializzazione è completo, si è pronti per la guida introduttiva successiva, in cui si inizieranno a provare le API File MIP.

> [!div class="nextstepaction"]
> [Elencare le etichette di riservatezza](quick-file-list-labels-csharp.md)
