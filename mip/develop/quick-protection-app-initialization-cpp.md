---
title: Avvio rapido - Inizializzazione per i client MIP SDK per C++ per l'API Protezione
description: Argomento di avvio rapido che illustra come scrivere la logica di inizializzazione per applicazioni client di Microsoft Information Protection (MIP) SDK con l'API Protezione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 063db1a923e66f108583b17ee998549511265bee
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564146"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>Guida introduttiva: Inizializzazione delle applicazioni client per le API Protezione (C++)

Questo avvio rapido spiega come implementare il modello di inizializzazione client usato dal SDK C++ di MIP in fase di esecuzione.

> [!NOTE]
> I passaggi descritti in questo avvio rapido sono necessari per qualsiasi applicazione client che usa le API Protezione di MIP. Questi Avvi rapidi devono essere eseguiti in modo seriale dopo l'inizializzazione dell'applicazione e l'implementazione delle classi dei delegati di autenticazione e di consenso.

## <a name="prerequisites"></a>Prerequisiti

Se non è già stato fatto, assicurarsi di:

- Completare i passaggi descritti in [Installazione e configurazione di Microsoft Information Protection (MIP) SDK](setup-configure-mip.md). La guida introduttiva "Inizializzazione delle applicazioni client" si basa sull'installazione e la configurazione corrette dell'SDK.
- Facoltativamente:
  - Vedere [Oggetti profilo e motore](concept-profile-engine-cpp.md). Gli oggetti profilo e motore sono concetti universali, necessari per i client che usano le API File, Criteri e Protezione di MIP.
  - Vedere [Concetti relativi all'autenticazione](concept-authentication-cpp.md) per informazioni su come vengono implementati l'autenticazione e il consenso dal SDK e dall'applicazione client.
  - Vedere [Concetti relativi agli osservatori](concept-async-observers.md) per altre informazioni sugli osservatori e su come vengono implementati. Il SDK di MIP usa il modello basato su osservatori per implementare le notifiche di eventi asincroni.

## <a name="create-a-visual-studio-solution-and-project"></a>Creare una soluzione e un progetto di Visual Studio

Verranno prima di tutto creati e configurati la soluzione e il progetto iniziali di Visual Studio su cui si baseranno le altre procedure di avvio rapido.

1. Aprire Visual Studio 2017 e scegliere **File**, **Nuovo**, **Progetto** dal menu. Nella finestra di dialogo **Nuovo progetto**:
   - Nel riquadro sinistro, in **Installati**, **Altri linguaggi**, selezionare **Visual C++** .
   - Nel riquadro centrale selezionare **Applicazione console di Windows**.
   - Nel riquadro inferiore, aggiornare **Nome** e **Posizione** del progetto, nonché il **Nome della soluzione** in cui è contenuto corrispondentemente.
   - Al termine fare clic sul pulsante **OK** in basso a destra.

     [![Creazione di una soluzione Visual Studio](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. Aggiungere il pacchetto NuGet per l'API Protezione SDK di MIP al progetto:
   - In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto (subito sotto il nodo della soluzione principale) e scegliere **Gestisci pacchetti NuGet**:
   - Quando viene aperta la scheda **Gestione pacchetti NuGet** nell'area delle schede Gruppo di editor:
     - Selezionare **Sfoglia**.
     - Immettere "Microsoft.InformationProtection" nella casella di ricerca.
     - Selezionare il pacchetto "Microsoft.InformationProtection.Protection".
     - Fare clic su "Installa" e quindi su "OK" quando viene visualizzata la finestra di dialogo di conferma **Anteprima modifiche**.

     [![Aggiunta del pacchetto NuGet in Visual Studio](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)

## <a name="implement-observer-classes-to-monitor-the-protection-profile-and-engine-objects"></a>Implementare le classi osservatore per monitorare gli oggetti profilo e motore di Protezione

Creare ora un'implementazione di base per una classe osservatore per il profilo Protezione usando l'estensione della classe `mip::ProtectionProfile::Observer` dell'SDK. In seguito si creerà e userà un'istanza dell'osservatore per monitorare il caricamento dell'oggetto profilo Protezione e l'aggiunta dell'oggetto motore al profilo.

1. Aggiungere una nuova classe al progetto, che genera automaticamente i file di intestazione (.h) e di implementazione (.cpp):

   - In **Esplora soluzioni** fare di nuovo clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi**, quindi scegliere **Classe**.
   - Nella finestra di dialogo **Aggiungi classe**:
     - Nel campo **Nome classe** immettere "profile_observer". Si noti che i campi del **file con estensione h** e del **file con estensione cpp** vengono popolati automaticamente in base al nome immesso.
     - Al termine fare clic su **OK**.

     [![Aggiunta della classe in Visual Studio](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. Dopo la generazione dei file con estensione h e cpp per la classe, entrambi i file vengono aperti nelle schede Editor gruppo. A questo punto aggiornare ogni file per implementare la nuova classe osservatore:

   - Aggiornare "profile_observer.h" selezionando ed eliminando la classe `profile_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <memory>
     #include "mip/protection/protection_profile.h"
     using std::exception_ptr;
     using std::shared_ptr;


     class ProtectionProfileObserver final : public mip::ProtectionProfile::Observer {
     public:
          ProtectionProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::ProtectionProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& Failure, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::ProtectionEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& Failure, const std::shared_ptr<void>& context) override;
     };
     ```

   - Aggiornare "profile_observer.cpp", selezionando ed eliminando l'implementazione della classe `profile_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::ProtectionEngine;
     using mip::ProtectionProfile;

     void ProtectionProfileObserver::OnLoadSuccess(const shared_ptr<ProtectionProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionProfile>>>(context);
          promise->set_value(profile);
     }

     void ProtectionProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionProfile>>>(context);
          promise->set_exception(error);
     }

     void ProtectionProfileObserver::OnAddEngineSuccess(const shared_ptr<ProtectionEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionEngine>>>(context);
          promise->set_value(engine);
     }

     void ProtectionProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. Dopo aver eseguito i passaggi del punto 1, aggiungere una nuova classe per l'osservatore del motore di Protezione "engine_observer" al progetto, che genera automaticamente i file di intestazione (.h) e di implementazione (.cpp).

4. Dopo la generazione dei file con estensione h e cpp per la classe, entrambi i file vengono aperti nelle schede Editor gruppo. A questo punto aggiornare ogni file per implementare la nuova classe osservatore:

   - Aggiornare "engine_observer.h" selezionando ed eliminando la classe `engine_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::vector;
     using std::exception_ptr;
     using std::shared_ptr;

     class ProtectionEngineObserver final : public mip::ProtectionEngine::Observer {
       public:
       ProtectionEngineObserver() {}
       void OnGetTemplatesSuccess(const vector<std::shared_ptr<mip::TemplateDescriptor>>& templateDescriptors, const shared_ptr<void>& context) override;
       void OnGetTemplatesFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;

     };
     ```

   - Aggiornare "engine_observer.cpp", selezionando/eliminando l'implementazione della classe `engine_observer` generata. **Non** rimuovere le direttive del preprocessore generate nel passaggio precedente (#pragma, #include). Quindi copiare e incollare il codice seguente nel file, dopo le eventuali direttive del preprocessore esistenti:

     ```cpp
     #include "mip/protection/protection_profile.h"
     #include "engine_observer.h"

     using std::promise;
     void ProtectionEngineObserver::OnGetTemplatesSuccess(const vector<shared_ptr<mip::TemplateDescriptor>>& templateDescriptors,const shared_ptr<void>& context) {
         auto loadPromise = static_cast<promise<vector<shared_ptr<mip::TemplateDescriptor>>>*>(context.get());
         loadPromise->set_value(templateDescriptors);
       };

       void ProtectionEngineObserver::OnGetTemplatesFailure(const exception_ptr& Failure, const shared_ptr<void>& context) {
         auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
         loadPromise->set_exception(Failure);
       };
     ```

5. Facoltativamente, usare CTRL+MAIUSC+B (**Compila soluzione**) per eseguire una compilazione/collegamento di prova della soluzione e assicurarsi che venga compilata correttamente prima di continuare.

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>Implementare un delegato di autenticazione e un delegato di consenso

MIP SDK implementa l'autenticazione usando l'estensibilità delle classi, che rende disponibile un meccanismo per condividere le operazioni di autenticazione con l'applicazione client. Il client deve acquisire un token di accesso OAuth2 adatto e fornirlo a MIP SDK in fase di esecuzione.

Creare un'implementazione per un delegato di autenticazione estendendo la classe `mip::AuthDelegate` dell'SDK ed eseguendo l'override e l'implementazione della funzione virtuale pura `mip::AuthDelegate::AcquireOAuth2Token()`. **Seguire la procedura descritta in [Avvio rapido: Inizializzazione dell'applicazione API File](quick-app-initialization-cpp.md).** In seguito si creerà un'istanza del delegato di autenticazione che verrà usata dagli oggetti profilo e motore dell'API Protezione.

## <a name="implement-a-consent-delegate"></a>Implementare un delegato di consenso

Si creerà ora un'implementazione per un delegato di consenso mediante l'estensione della classe `mip::ConsentDelegate` dell'SDK e l'override/implementazione della funzione virtuale pura `mip::AuthDelegate::GetUserConsent()`.  **Seguire la procedura descritta in [Avvio rapido: Inizializzazione dell'applicazione API File](quick-app-initialization-cpp.md).** In seguito si creerà un'istanza del delegato di consenso che verrà usata dagli oggetti profilo e motore dell'API Protezione.

## <a name="construct-a-protection-profile-and-engine"></a>Costruire un profilo e un motore di Protezione

Come detto, gli oggetti profilo e motore sono necessari per i client del SDK che usano API MIP. Completare la parte di scrittura del codice di questa guida introduttiva, aggiungendo il codice per creare un'istanza degli oggetti profilo e motore:

1. Da **Esplora soluzioni** aprire il file con estensione cpp del progetto che contiene l'implementazione del metodo `main()`. Per impostazione predefinita il file ha lo stesso nome del progetto che lo contiene, specificato durante la creazione del progetto.

2. Rimuovere l'implementazione generata di `main()`. **Non** rimuovere le direttive del preprocessore generate da Visual Studio durante la creazione del progetto (#pragma, #include). Aggiungere il codice seguente dopo eventuali direttive del preprocessore:

  ```cpp
  #include "mip/mip_init.h"
  #include "mip/mip_context.h"  
  #include "auth_delegate.h"
  #include "consent_delegate.h"
  #include "profile_observer.h"
  #include"engine_observer.h"

  using std::promise;
  using std::future;
  using std::make_shared;
  using std::shared_ptr;
  using std::string;
  using std::cout;
  using mip::ApplicationInfo;
  using mip::ProtectionProfile;
  using mip::ProtectionEngine;

  int main(){
    // Construct/initialize objects required by the application's profile object
    ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                            "<application-name>",
                            "<application-version>"};

    auto mipContext = mip::MipContext::Create(appInfo,
                                              "file_sample",
                                              mip::LogLevel::Trace,
                                              false,
                                              nullptr /*loggerDelegateOverride*/,
                                              nullptr /*telemetryOverride*/);


    auto profileObserver = make_shared<ProtectionProfileObserver>(); // Observer object
    auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>"); // Authentication delegate object (App ID)
    auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object

    // Construct/initialize profile object
    ProtectionProfile::Settings profileSettings(
      mipContext,
      mip::CacheStorageType::OnDisk,      
      consentDelegateImpl,
      profileObserver);

    // Set up promise/future connection for async profile operations; load profile asynchronously
    auto profilePromise = make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    try
    {
      mip::ProtectionProfile::LoadAsync(profileSettings, profilePromise);
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
    ProtectionEngine::Settings engineSettings(
       authDelegateImpl,                          // Reference to mip::AuthDelegate implementation
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state
       "en-US");                                  // Locale (default = en-US)

    // Set up promise/future connection for async engine operations; add engine to profile asynchronously
    auto enginePromise = make_shared<promise<shared_ptr<ProtectionEngine>>>();
    auto engineFuture = enginePromise->get_future();
    profile->AddEngineAsync(engineSettings, enginePromise);
    std::shared_ptr<ProtectionEngine> engine;

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

    // Application shutdown. Null out profile and engine, call ReleaseAllResources();
    // Application may crash at shutdown if resources aren't properly released.
    engine = nullptr;
    profile = nullptr;
    mipContext = nullptr;

    return 0;
  }
   ```

3. Sostituire tutti i valori segnaposto nel codice sorgente appena incollato, usando costanti stringa:

   | Segnaposto | Valore | Esempio |
   |:----------- |:----- |:--------|
   | \<application-id\> | ID di applicazione (GUID) di Azure AD assegnato all'applicazione registrata nel passaggio 2 dell'articolo "Installazione e configurazione dell'SDK MIP" (setup-configure-mip.md). Sostituire 2 istanze. | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | Nome descrittivo definito dall'utente per l'applicazione. Deve contenere caratteri ASCII validi (escluso ';') e idealmente corrisponde al nome dell'applicazione usato nella registrazione di Azure AD. | `"AppInitialization"` |
   | \<application-version\> | Informazioni sulla versione definite dall'utente per l'applicazione. Deve contenere caratteri ASCII validi (escluso ';'). | `"1.1.0.0"` |
   | \<engine-account\> | Account usato per l'identità del motore. Quando si esegue l'autenticazione con un account utente durante l'acquisizione dei token, deve corrispondere a questo valore. | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | Stato definito dall'utente da associare al motore. | `"My App State"` |

4. Eseguire ora la compilazione finale dell'applicazione e risolvere gli eventuali errori. Il codice dovrebbe essere compilato correttamente, ma non verrà eseguito correttamente fino al completamento della guida introduttiva successiva. Se si esegue l'applicazione viene visualizzato un output simile al seguente. L'applicazione costruirà il profilo e il motore di Protezione ma non attiverà il modulo di autenticazione e non sarà ancora disponibile un token di accesso fin al completamento dell'Avvio rapido successivo.

   ```console
    C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
    To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
    Press any key to close this window . . .
   ```

## <a name="next-steps"></a>Passaggi successivi

Ora che il codice di inizializzazione è completo, è possibile passare all'avvio rapido successivo in cui si inizierà a provare l'API Protezione MIP.

> [!div class="nextstepaction"]
> [Elencare i modelli di protezione](quick-protection-list-templates-cpp.md)
