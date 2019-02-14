---
title: Guida introduttiva - inizializzazione per i client di Microsoft Information Protection (MIP) SDK C++
description: Guida introduttiva che mostra come scrivere la logica di inizializzazione per applicazioni client di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: bryanla
ms.openlocfilehash: 75ca6b078275a2547cebfee3c78f8741f367c788
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255955"
---
# <a name="quickstart-client-application-initialization-c"></a>Guida introduttiva: Inizializzazione dell'applicazione client (C++)

Questa Guida introduttiva illustra come implementare il modello di inizializzazione client, usato dal SDK C++ MIP in fase di esecuzione. 

> [!NOTE]
> I passaggi descritti in questa guida introduttiva sono necessari per qualsiasi applicazione client che usa le API File, Criteri e Protezione di MIP. Sebbene questa guida introduttiva illustri l'utilizzo delle API File, lo stesso modello è applicabile ai client che usano le API Criteri e Protezione. Completare le guide introduttive rimanenti in modo seriale, come ognuno di essi si basa su quello precedente, con questo non è il primo.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, assicurarsi di:

- Completare i passaggi descritti in [Installazione e configurazione di Microsoft Information Protection (MIP) SDK](setup-configure-mip.md). La guida introduttiva "Inizializzazione delle applicazioni client" si basa sull'installazione e la configurazione corrette dell'SDK.
- Se lo si desidera:
  - Vedere [Oggetti profilo e motore](concept-profile-engine-cpp.md). Gli oggetti profilo e motore sono concetti universali, necessari per i client che usano le API File, Criteri e Protezione di MIP. 
  - Revisione [concetti di autenticazione](concept-authentication-cpp.md) per informazioni su come l'autenticazione e autorizzazione vengono implementate dal SDK e l'applicazione client.
  - Vedere [Concetti relativi agli osservatori](concept-async-observers.md) per altre informazioni sugli osservatori e su come vengono implementati. Microsoft Information Protection SDK Usa il modello observer per implementare le notifiche degli eventi asincroni.

## <a name="create-a-visual-studio-solution-and-project"></a>Creare una soluzione e un progetto di Visual Studio

È prima di tutto creare e configurare la soluzione di Visual Studio e il progetto, in cui compilare altre guide introduttive iniziale. 

1. Aprire Visual Studio 2017 e scegliere **File**, **Nuovo**, **Progetto** dal menu. Nella finestra di dialogo **Nuovo progetto**:
   - Nel riquadro sinistro, in **Installati**, **Altri linguaggi**, selezionare **Visual C++**.
   - Nel riquadro centrale selezionare **Applicazione console di Windows**.
   - Nel riquadro inferiore, aggiornare **Nome** e **Posizione** del progetto, nonché il **Nome della soluzione** in cui è contenuto corrispondentemente.
   - Al termine fare clic sul pulsante **OK** in basso a destra.

     [![Creazione di una soluzione Visual Studio](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. Aggiungere il pacchetto NuGet per l'API File di MIP SDK al progetto:
   - Nel **Esplora soluzioni**, fare clic sul nodo del progetto (direttamente sotto il nodo di inizio/soluzione) e selezionare **Gestisci pacchetti NuGet...** :
   - Quando viene aperta la scheda **Gestione pacchetti NuGet** nell'area delle schede Gruppo di editor:
     - Selezionare **Sfoglia**.
     - Immettere "Microsoft.InformationProtection" nella casella di ricerca.
     - Selezionare il pacchetto "Microsoft.InformationProtection.File".
     - Fare clic su "Installa" e quindi su "OK" quando viene visualizzata la finestra di dialogo di conferma **Anteprima modifiche**.
   
     [![Aggiunta del pacchetto NuGet in Visual Studio](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)
 
## <a name="implement-an-observer-class-to-monitor-the-file-profile-and-engine-objects"></a>Implementare una classe osservatore per monitorare gli oggetti profilo e motore dell'API File

Creare ora un'implementazione di base per una classe osservatore per il profilo File mediante l'estensione della classe `mip::FileProfile::Observer` dell'SDK. In seguito si creerà e userà un'istanza dell'osservatore per monitorare il caricamento dell'oggetto profilo File e l'aggiunta dell'oggetto motore al profilo.

1. Aggiungere una nuova classe al progetto, che genera automaticamente i file di intestazione (.h) e di implementazione (.cpp):

   - Nel **Esplora soluzioni**, fare doppio clic sul nodo del progetto, anche in questo caso, selezionare **Add**, quindi selezionare **classe**.
   - Nella finestra di dialogo **Aggiungi classe**:
     - Nel campo **Nome classe** immettere "profile_observer". Si noti che i campi del **file con estensione h** e del **file con estensione cpp** vengono popolati automaticamente in base al nome immesso.
     - Al termine fare clic su **OK**.

     [![Aggiunta della classe in Visual Studio](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. Dopo la generazione dei file con estensione h e cpp per la classe, entrambi i file vengono aperti nelle schede Editor gruppo. A questo punto aggiornare ogni file per implementare la nuova classe osservatore:

   - Aggiornare "profile_observer.h" selezionando ed eliminando la classe `profile_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <memory>
     #include "mip/file/file_profile.h"

     class ProfileObserver final : public mip::FileProfile::Observer {
     public:
          ProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
     };
     ```

   - Aggiornare "profile_observer.cpp", selezionando ed eliminando l'implementazione della classe `profile_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::FileEngine;
     using mip::FileProfile;

     void ProfileObserver::OnLoadSuccess(const shared_ptr<FileProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_value(profile);
     }

     void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_exception(error);
     }

     void ProfileObserver::OnAddEngineSuccess(const shared_ptr<FileEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_value(engine);
     }

     void ProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. Facoltativamente, usare F6 (**Compila soluzione**) per eseguire una compilazione/collegamento di prova della soluzione e assicurarsi che venga compilata correttamente prima di continuare.

## <a name="implement-an-authentication-delegate"></a>Implementare un delegato di autenticazione

MIP SDK implementa l'autenticazione usando l'estensibilità delle classi, che rende disponibile un meccanismo per condividere le operazioni di autenticazione con l'applicazione client. Il client deve acquisire un token di accesso OAuth2 adatto e fornirlo a MIP SDK in fase di esecuzione. 

Si creerà ora un'implementazione per un delegato di autenticazione mediante l'estensione della classe `mip::AuthDelegate` dell'SDK e l'override/implementazione della funzione virtuale pura `mip::AuthDelegate::AcquireOAuth2Token()`. In seguito si creerà un'istanza del delegato di autenticazione che verrà usata dagli oggetti profilo e motore dell'API File.

1. Usando la stessa funzionalità "Aggiungi classe" di Visual Studio usata nel passaggio 1 della sezione precedente, aggiungere un'altra classe al progetto. Questa volta, immettere "auth_delegate" nel campo **Nome classe**. 

2. A questo punto aggiornare ogni file per implementare la nuova classe del delegato di autenticazione:

   - Aggiornare "auth_delegate.h" sostituendo tutto il codice della classe `auth_delegate` generato con il codice sorgente seguente. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include):

     ```cpp
     #include <string>
     #include "mip/common_types.h"

     class AuthDelegateImpl final : public mip::AuthDelegate {
     public:
          AuthDelegateImpl() = delete;        // Prevents default constructor
          
          AuthDelegateImpl(
            const std::string& appId)         // AppID for registered AAD app
            : mAppId(appId) {};

          bool AcquireOAuth2Token(            // Called by MIP SDK to get a token
            const mip::Identity& identity,    // Identity of the account to be authenticated, if known
            const OAuth2Challenge& challenge, // Authority (AAD tenant issuing token), and resource (API being accessed; "aud" claim).
            OAuth2Token& token) override;     // Token handed back to MIP SDK
     private:
          std::string mAppId;
          std::string mToken;
          std::string mAuthority;
          std::string mResource;
     };
     ```

   - Aggiornare "auth_delegate.cpp" sostituendo tutto il codice dell'implementazione della classe `auth_delegate` generato con il codice sorgente seguente. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). 

     > [!IMPORTANT]
     > Il codice di acquisizione del token seguente non è adatto per l'uso in ambiente di produzione. Nell'ambiente di produzione questo deve essere sostituito da codice che acquisisce in modo dinamico un token, usando:
     > - AppId e URI di risposta/reindirizzamento specificati nella registrazione dell'app di Azure AD (l'URI di risposta/reindirizzamento **deve** corrispondere alla registrazione dell'app)
     > - L'URL dell'autorità e della risorsa passato dall'SDK nell'argomento `challenge` (l'URL della risorsa **deve** corrispondere ad API/autorizzazioni della registrazione dell'app)
     > - Credenziali valide per app/utente, in cui l'account corrisponde all'argomento `identity` passato dall'SDK. I client "nativi" OAuth2 devono richiedere le credenziali utente e usare il flusso di "codice di autorizzazione". I "client riservati" OAuth2 possono usare le proprie credenziali protette con il flusso di "credenziali client" (ad esempio, un servizio) o richiedere le credenziali utente usando il flusso di "codice di autorizzazione" (ad esempio, un'app Web). 
     >
     > L'acquisizione di token OAuth2 è un protocollo complesso e in genere viene eseguita usando una libreria. La funzione TokenAcquireOAuth2Token() viene chiamata **solo** da MIP SDK, all'occorrenza.

     ```cpp
     #include <iostream>
     using std::cout;
     using std::cin;
     using std::string;

     bool AuthDelegateImpl::AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) 
     {
          // Acquire a token manually, reuse previous token if same authority/resource. In production, replace with token acquisition code.
          string authority = challenge.GetAuthority();
          string resource = challenge.GetResource();
          if (mToken == "" || (authority != mAuthority || resource != mResource))
          {
              cout << "\nRun the PowerShell script to generate an access token using the following values, then copy/paste it below:\n";
              cout << "Set $authority to: " + authority + "\n";
              cout << "Set $resourceUrl to: " + resource + "\n";
              cout << "Sign in with user account: " + identity.GetEmail() + "\n";
              cout << "Enter access token: ";
              cin >> mToken;
              mAuthority = authority;
              mResource = resource;
              system("pause");
          }

          // Pass access token back to MIP SDK
          token.SetAccessToken(mToken);

          // True = successful token acquisition; False = failure
          return true;
     }
     ``` 
3. Facoltativamente, usare F6 (**Compila soluzione**) per eseguire una compilazione/collegamento di prova della soluzione e assicurarsi che venga compilata correttamente prima di continuare.

## <a name="implement-a-consent-delegate"></a>Implementare un delegato di consenso

Si creerà ora un'implementazione per un delegato di consenso mediante l'estensione della classe `mip::ConsentDelegate` dell'SDK e l'override/implementazione della funzione virtuale pura `mip::AuthDelegate::GetUserConsent()`. In seguito si creerà un'istanza del delegato di consenso che verrà usata dagli oggetti profilo e motore dell'API File.

1. Usando la stessa funzionalità "Aggiungi classe" di Visual Studio usata in precedenza, aggiungere un'altra classe al progetto. Questa volta, immettere "consent_delegate" nel campo **Nome classe**. 

2. A questo punto aggiornare ogni file per implementare la nuova classe del delegato di consenso:

   - Aggiornare "consent_delegate.h" sostituendo tutto il codice della classe `consent_delegate` generato con il codice sorgente seguente. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include):

     ```cpp
     #include "mip/common_types.h"
     #include <string>

     class ConsentDelegateImpl final : public mip::ConsentDelegate {
     public:
          ConsentDelegateImpl() = default;
          virtual mip::Consent GetUserConsent(const std::string& url) override;
     };
     ```

   - Aggiornare "consent_delegate.cpp" sostituendo tutto il codice dell'implementazione della classe `consent_delegate` generato con il codice sorgente seguente. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). 

     ```cpp
     #include <iostream>
     using mip::Consent;
     using std::string;

     Consent ConsentDelegateImpl::GetUserConsent(const string& url) 
     {
          // Accept the consent to connect to the url
          std::cout << "SDK will connect to: " << url << std::endl;
          return Consent::AcceptAlways;
     }
     ``` 
3. Facoltativamente, usare F6 (**Compila soluzione**) per eseguire una compilazione/collegamento di prova della soluzione e assicurarsi che venga compilata correttamente prima di continuare.

## <a name="construct-a-file-profile-and-engine"></a>Costruire gli oggetti profilo e motore File

Come accennato, sono richiesti per i client SDK tramite MIP APIs oggetti del profilo e il motore. Completare la parte di scrittura del codice di questa guida introduttiva, aggiungendo il codice per creare un'istanza degli oggetti profilo e motore: 

1. Da **Esplora soluzioni** aprire il file con estensione cpp del progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Rimuovere l'implementazione generata di `main()`. **Non** rimuovere le direttive del preprocessore generate da Visual Studio durante la creazione del progetto (#pragma, #include). Aggiungere il codice seguente dopo eventuali direttive del preprocessore:

   ```cpp
   #include "auth_delegate.h"
   #include "consent_delegate.h"
   #include "profile_observer.h"

   using std::promise;
   using std::future;
   using std::make_shared;
   using std::shared_ptr;
   using std::string;
   using std::cout;
   using mip::ApplicationInfo; 
   using mip::FileProfile;
   using mip::FileEngine;

   int main()
   {
     // Construct/initialize objects required by the application's profile object
     ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                 "<application-name>",
                 "<application-version>"};
     auto profileObserver = make_shared<ProfileObserver>();         // Observer object                  
     auto authDelegateImpl = make_shared<AuthDelegateImpl>(         // Authentication delegate object (App ID)
                 "<application-id>");
     auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object
 
     // Construct/initialize profile object
     FileProfile::Settings profileSettings("",    // Path for logging/telemetry/state
       true,                                      // true = use in-memory state storage (vs disk)
       authDelegateImpl,                            
       consentDelegateImpl,                     
       profileObserver,                         
       appInfo);                                    

     // Set up promise/future connection for async profile operations; load profile asynchronously
     auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
     auto profileFuture = profilePromise->get_future();
    try
    { 
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... are the Settings and ApplicationInfo objects populated correctly?\n\n"
            << e.what() << "'\n";
        system("pause");
        return 1;

    }
    auto profile = profileFuture.get();

     // Construct/initialize engine object
     FileEngine::Settings engineSettings(
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state      
       "en-US");                                  // Locale (default = en-US)

     // Set up promise/future connection for async engine operations; add engine to profile asynchronously
     auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
     auto engineFuture = enginePromise->get_future();
     profile->AddEngineAsync(engineSettings, enginePromise);
     std::shared_ptr<FileEngine> engine; 
     try
     {
       engine = engineFuture.get();             
     }
     catch (const std::exception& e)
     {
       cout << "An exception occurred... is the access token incorrect/expired?\n\n"
        << e.what() << "'\n";
       system("pause");
       return 1;
     }

   return 0;
   }
   ``` 

3. Sostituire tutti i valori segnaposto nel codice appena incollato, usando le costanti stringa di origine:

   | Segnaposto | Value | Esempio |
   |:----------- |:----- |:--------|
   | \<application-id\> | L'Azure AD Application ID (GUID) assegnati all'applicazione registrata nel [passaggio #2 della "il programma di installazione di Microsoft Information Protection SDK e della configurazione"](/information-protection/develop/setup-configure-mip#register-a-client-application-with-azure-active-directory) articolo. Sostituire 2 istanze. | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | Nome descrittivo definito dall'utente per l'applicazione. Deve contenere caratteri ASCII validi (escluso ';') e idealmente corrisponde al nome dell'applicazione è usato nella registrazione di Azure AD. | `"AppInitialization"` |
   | \<application-version\> | Informazioni di versione definito dall'utente per l'applicazione. Deve contenere caratteri ASCII validi (escluso ';'). | `"1.1.0.0"` |
   | \<engine-account\> | Account usato per l'identità del motore. Quando si esegue l'autenticazione con un account utente durante l'acquisizione dei token, deve corrispondere a questo valore. | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | Stato definito dall'utente da associare al motore. | `"My App State"` |


4. Eseguire ora la compilazione finale dell'applicazione e risolvere gli eventuali errori. Il codice dovrebbe essere compilato correttamente, ma non verrà eseguito correttamente fino al completamento della guida introduttiva successiva. Se si esegue l'applicazione, è visualizzato un output simile al seguente. Il token di accesso da specificare sarà disponibile solo dopo il completamento della guida introduttiva successiva.

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account:
   Enter access token:
   ```

## <a name="next-steps"></a>Passaggi successivi

Ora che il codice di inizializzazione è completo, si è pronti per la guida introduttiva successiva, in cui si inizieranno a provare le API File MIP.

> [!div class="nextstepaction"]
> [Elencare le etichette di riservatezza](quick-file-list-labels-cpp.md)
