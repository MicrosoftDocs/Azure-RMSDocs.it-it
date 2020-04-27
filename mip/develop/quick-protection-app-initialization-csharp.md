---
title: 'Avvio rapido: Inizializzazione delle applicazioni client - API Protezione (C#)'
description: Avvio rapido che illustra come scrivere la logica di inizializzazione per applicazioni client di un SDK di Microsoft Information Protection (MIP) per l'API Protezione C#.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 6222326e569d03fbb208d42aacd7efb7ab406a78
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766372"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>Guida introduttiva: Inizializzazione delle applicazioni client per le API Protezione (C#)

Questo Avvio rapido spiega come implementare il modello di inizializzazione client usato dal wrapper .NET del SDK MIP in fase di runtime.

> [!NOTE]
> I passaggi descritti in questo avvio rapido sono necessari per qualsiasi applicazione client che usa l'API Protezione del wrapper .NET di MIP. Questi Avvi rapidi devono essere eseguiti in modo seriale dopo l'inizializzazione dell'applicazione e l'implementazione delle classi dei delegati di autenticazione e di consenso.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, assicurarsi di:

- Completare i passaggi descritti in [Installazione e configurazione di Microsoft Information Protection (MIP) SDK](setup-configure-mip.md). L'Avvio rapido "Configurazione del profilo e del motore di Protezione" si basa sull'installazione e la configurazione appropriate dell'SDK.
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

3. Ripetere i passaggi precedenti per aggiungere il pacchetto dell'API Protezione SDK di MIP, ma aggiungere invece "Microsoft.IdentityModel.Clients.ActiveDirectory" all'applicazione.

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>Implementare un delegato di autenticazione e un delegato di consenso

Se non è già implementato, seguire i passaggi elencati in[Inizializzazione dell'applicazione API File](quick-app-initialization-csharp.md) per implementare i delegati di autenticazione e di consenso.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Inizializzare il wrapper gestito del SDK MIP

1. Da **Esplora soluzioni** aprire il file con estensione cs del progetto che contiene l'implementazione del metodo `Main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Rimuovere l'implementazione generata di `main()`.

3. Il wrapper gestito include una classe statica `Microsoft.InformationProtection.MIP` usata per l'inizializzazione, la creazione di `MipContext`, il caricamento di profili e il rilascio delle risorse. Per inizializzare il wrapper per le operazioni dell'API, chiamare `MIP.Initialize()`, passando `MipComponent.Protection` per caricare le librerie necessarie per le operazioni di protezione.

4. In `Main()` in *Program.cs* aggiungere quanto segue, sostituendo **\<application-id\>** con l'ID di registrazione dell'applicazione Azure AD creata in precedenza.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for Protection API operations
            MIP.Initialize(MipComponent.Protection);
        }
    }
}
```

## <a name="construct-a-protection-profile-and-engine"></a>Costruire un profilo e un motore di Protezione

Come detto, gli oggetti profilo e motore sono necessari per i client del SDK che usano API MIP. Completare la parte di scrittura del codice di questo Avvio rapido aggiungendo il codice necessario per caricare le DLL native, quindi creare un'istanza degli oggetti profilo e motore.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               // Initialize Wrapper for Protection API operations.
               MIP.Initialize(MipComponent.Protection);

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

               // Initialize and instantiate the ProtectionProfile.
               // Create the ProtectionProfileSettings object.
               // Initialize protection profile settings to create/use local state.
               var profileSettings = new ProtectionProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,                                        
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var protectionProfile = Task.Run(async () => await MIP.LoadProtectionProfileAsync(profileSettings)).Result;

               // Create a ProtectionEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new ProtectionEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var protectionEngine = Task.Run(async () => await protectionProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               protectionEngine = null;
               protectionProfile = null;
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

Ora che il codice di inizializzazione è completo, è possibile passare all'avvio rapido successivo in cui si inizieranno a provare le API Protezione MIP.

> [!div class="nextstepaction"]
> [Elencare i modelli di protezione](quick-protection-list-templates-csharp.md)
