---
title: Installazione e configurazione di Microsoft Information Protection (MIP) SDK
description: Informazioni sui prerequisiti di installazione e configurazione per poter usare le applicazioni compilate con Microsoft Information Protection SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 06/13/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 5daada951fb888fc7aa01071236af751ec38e002
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215528"
---
# <a name="microsoft-information-protection-mip-sdk-setup-and-configuration"></a>Installazione e configurazione di Microsoft Information Protection (MIP) SDK

Gli articoli dedicati a guide introduttive ed esercitazioni sono incentrati sulla creazione di applicazioni che usano le librerie e le API di MIP SDK. Questo articolo illustra come installare e configurare l'abbonamento a Microsoft 365 e una workstation client, in preparazione per l'uso dell'SDK.

## <a name="prerequisites"></a>Prerequisiti

Assicurarsi di consultare gli argomenti seguenti prima di iniziare:

- [Che cos'è il Centro conformità e sicurezza di Office 365?](/office365/securitycompliance/security-and-compliance)
- [Che cos'è Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
- [Come funziona la protezione in Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

> [!IMPORTANT]
> **Per rispettare la privacy degli utenti, è necessario chiedere il consenso all'utente prima di abilitare la registrazione automatica.** L'esempio seguente è un messaggio standard usato da Microsoft per la notifica di registrazione:
>
> *Attivando la registrazione degli errori e delle prestazioni, l’utente accetta l'invio di tali dati a Microsoft. Microsoft raccoglie i dati sugli errori e sulle prestazioni tramite Internet ("Dati"). Microsoft usa questi dati per offrire e migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi Microsoft. Vengono analizzate, ad esempio, prestazioni e affidabilità quali le funzionalità usate dagli utenti, la velocità di risposta delle funzionalità, le prestazioni del dispositivo, le interazioni con l'interfaccia utente e tutti i problemi che possono verificarsi durante l'uso del prodotto. I Dati includono anche informazioni sulla configurazione del software, ad esempio la versione in esecuzione e l'indirizzo IP.*

## <a name="sign-up-for-an-office-365-subscription"></a>Iscriversi per un abbonamento a Office 365

Molti degli esempi dell'SDK richiedono l'accesso a un abbonamento a Office 365. Se non è già stato fatto, assicurarsi di iscriversi per uno dei tipi di abbonamento seguenti:

| Name                                               | Iscrizione                                                                         |
| -------------------------------------------------- | ------------------------------------------------------------------------------- |
| Office 365 Enterprise E3 - Versione di valutazione (versione di valutazione gratuita di 30 giorni) | https://go.microsoft.com/fwlink/p/?LinkID=403802                                |
| Office 365 Enterprise E3 o E5                     | https://products.office.com/business/office-365-enterprise-e3-business-software |
| Enterprise Mobility and Security E3 o E5          | https://www.microsoft.com/cloud-platform/enterprise-mobility-security           |
| Azure Information Protection Premium P1 o P2      | https://azure.microsoft.com/pricing/details/information-protection/             |
| Microsoft 365 E3, E5 o F1                        | https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans         |

## <a name="configure-sensitivity-labels"></a>Configurare le etichette di riservatezza

Se si usa già Azure Information Protection, è necessario eseguire la migrazione delle etichette nel Centro sicurezza e conformità di Office 365. Per altre informazioni sul processo, vedere [Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365](/azure/information-protection/configure-policy-migrate-labels).

## <a name="configure-your-client-workstation"></a>Configurare la workstation client

Seguire poi questa procedura per assicurarsi che il computer client sia installato e configurato correttamente.

1. Se si usa una workstation Windows 10:

   - Usare Windows Update per aggiornare il computer a Windows 10 Fall Creators Update (versione 1709) o versioni successive. Per verificare la versione corrente:
     - Fare clic sull'icona di Windows nell'angolo inferiore sinistro.
     - Digitare "Informazioni sul PC" e premere "INVIO".
     - Scorrere verso il basso fino a **Specifiche Windows** e controllare in **Versione**.

   - Verificare che nella workstation sia abilitata la "Modalità sviluppatore":
     - Fare clic sull'icona di Windows nell'angolo inferiore sinistro.
     - Digitare "Usa le funzionalità per gli sviluppatori" e premere "INVIO" quando viene visualizzata la voce **Usa le funzionalità per gli sviluppatori**.
     - Nella finestra di dialogo **Impostazioni**, scheda **Per sviluppatori**, selezionare l'opzione **Modalità sviluppatore** in "Usa le funzionalità per gli sviluppatori".
     - Chiudere la finestra di dialogo **Impostazioni**.

2. Installare [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) con i carichi di lavoro e i componenti facoltativi seguenti:
   - Carico di lavoro per Windows **Sviluppo di app per la piattaforma UWP (Universal Windows Platform)** con i componenti facoltativi seguenti:
     - **Supporto per la piattaforma UWP in C++**
     - **Windows 10 SDK 10.0.16299.0 SDK** o versione successiva, se non è incluso per impostazione predefinita
   - Carico di lavoro per Windows **Sviluppo di applicazioni desktop con C++** con i componenti facoltativi seguenti:
     - **Windows 10 SDK 10.0.16299.0 SDK** o versione successiva, se non è incluso per impostazione predefinita

     [![Installazione di Visual Studio](media/setup-mip-client/visual-studio-install.png)](media/setup-mip-client/visual-studio-install.png#lightbox)

3. Installare il [modulo PowerShell ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2):

   - Poiché sono necessari diritti di amministratore per installare i moduli, è prima di tutto necessario:

     - Accedere al computer con un account con diritti di amministratore.
     - Eseguire la sessione di Windows PowerShell con diritti elevati (Esegui come amministratore).

   - Eseguire quindi il cmdlet `install-module -name adal.ps`:

     ```powershell
     PS C:\WINDOWS\system32> install-module -name adal.ps

     Untrusted repository
     You are installing the modules from an untrusted repository. If you trust this repository, change its
     InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
     'PSGallery'?
     [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A

     PS C:\WINDOWS\system32>
     ```

4. Scaricare i file SDK:

   MIP SDK è supportato nelle piattaforme seguenti con download separati per ogni piattaforma/linguaggio supportato:

   [!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

   **Download Tar.gz/.Zip**

   I download Tar.gz e .Zip contengono file compressi, uno per ogni API. I file compressi sono denominati nel modo seguente, dove \<API\> = `file`, `protection` o `upe` e \<OS\> = la piattaforma: `mip_sdk_<API>_<OS>_1.0.0.0.zip (or .tar.gz)`. Ad esempio, il file per i file binari e le intestazioni dell'API di protezione per la piattaforma Debian è denominato `mip_sdk_protection_debian9_1.0.0.0.tar.gz`. Ogni file con estensione tar.gz o zip completo è suddiviso in tre directory:

   - **Bins:** file binari compilati per ogni architettura di piattaforma, dove applicabile.
   - **Include:** file di intestazione (C++).
   - **Samples:** codice sorgente per applicazioni di esempio.

   **Pacchetti NuGet**

   Per lo sviluppo in Visual Studio, l'SDK può essere installato anche tramite la Console di Gestione pacchetti NuGet:

    ```console
    Install-Package Microsoft.InformationProtection.File
    Install-Package Microsoft.InformationProtection.Policy
    Install-Package Microsoft.InformationProtection.Protection
    ```

5. Se non si usa il pacchetto NuGet, aggiungere i percorsi dei file binari dell'SDK alla variabile di ambiente PATH. La variabile PATH consente alle applicazioni client di trovare i file binari dipendenti (DLL) in fase di esecuzione (FACOLTATIVO):

   Se si usa una workstation Windows 10:

   - Fare clic sull'icona di Windows nell'angolo inferiore sinistro.
   - Digitare "Path" e premere "INVIO", quando viene visualizzata la voce **Modifica le variabili di ambiente relative al sistema**.
   - Nella finestra di dialogo **Proprietà del sistema** fare clic su **Variabili di ambiente**.
   - Nella finestra di dialogo **Variabili di ambiente** fare clic sulla riga della variabile **Path** in **Variabili dell'utente per \<user\>** e quindi fare clic su **Modifica**.
   - Nella finestra di dialogo **Modifica variabile di ambiente** fare clic su **Nuovo**, che consente di creare una nuova riga modificabile. Usando il percorso completo per ognuna delle sottodirectory `file\bins\debug\amd64`, `protection\bins\debug\amd64` e `upe\bins\debug\amd64`, aggiungere una nuova riga per ognuna. Le directory dell'SDK sono archiviate nel formato `<API>\bins\<target>\<platform>`, dove:
     - \<API\> = `file`, `protection`, `upe`
     - \<target\> = `debug`, `release`
     - \<platform\> = `amd64` (x64), `x86` e così via.

   - Dopo aver completato la modifica della variabile **Path** fare clic su **OK**. Fare quindi clic su **OK** quando si torna alla finestra di dialogo **Variabili di ambiente**.

6. Scaricare gli esempi SDK da GitHub (FACOLTATIVO):

   - Se non è già disponibile, creare prima di tutto un [profilo GitHub](https://github.com/join).
   - Installare quindi la versione più recente degli [strumenti client Git di Software Freedom Conservancy (Git Bash)](https://git-scm.com/download/)
   - Usare Git Bash per scaricare gli esempi di interesse:
     - Usare la query seguente per visualizzare i repository: https://github.com/Azure-Samples?utf8=%E2%9C%93&q=MipSdk.
     - Con Git Bash, usare `git clone https://github.com/azure-samples/<repo-name>` per scaricare ogni repository di esempi.

## <a name="register-a-client-application-with-azure-active-directory"></a>Registrare un'applicazione client in Azure Active Directory

Come parte del processo di provisioning dell'abbonamento a Microsoft 365 viene creato un tenant di Azure Active Directory (Azure AD) associato. Il tenant di Azure AD consente la gestione delle identità e dell'accesso per gli *account utente* e gli *account di applicazione* di Microsoft 365. Per le applicazioni che richiedono l'accesso ad API protette (ad esempio le API MIP) è necessario un account di applicazione.

Per il processo di autenticazione e autorizzazione in fase di esecuzione, gli account sono rappresentati da un'*entità di sicurezza*, derivata dalle informazioni di identità dell'account. Le entità di sicurezza che rappresentano un account di applicazione vengono definite [*entità servizio*](/azure/active-directory/develop/developer-glossary#service-principal-object).

Per registrare un account di applicazione in Azure AD per l'uso con gli esempi e le guide introduttive di MIP SDK:

  > [!IMPORTANT]
  > Per accedere alla gestione del tenant Azure AD per la creazione dell'account, sarà necessario accedere al portale di Azure con un account utente membro del [ruolo "Proprietario" nella sottoscrizione](/azure/billing/billing-add-change-azure-subscription-administrator). A seconda della configurazione del tenant, potrebbe anche essere necessario essere membri del ruolo della directory "Amministratore globale" per [registrare un'applicazione](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
  > È consigliabile eseguire le operazioni di test con un account con restrizioni. Assicurarsi che l'account disponga solo dei diritti per accedere agli endpoint SCC necessari. Le password passate come testo non crittografato tramite riga di comando possono essere raccolte dai sistemi di registrazione.

1. Seguire la procedura indicata in [Registrare un'app con Azure AD, sezione Registrare una nuova applicazione](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#register-a-new-application-using-the-azure-portal). A scopo di test, usare i valori seguenti per le proprietà specificate quando si eseguono i passaggi della guida:
    - **Tipi di account supportati**: selezionare "Account solo in questa directory organizzativa".
    - **URI di reindirizzamento**: impostare il tipo di URI di reindirizzamento su "Client pubblico (per dispositivi mobili e desktop)". Se l'applicazione usa Microsoft Authentication Library (MSAL), servirsi di `http://localhost`. In caso contrario, usare un elemento nel formato `<app-name>://authorize`.

2. Al termine, si tornerà alla pagina **App registrata** per la registrazione della nuova applicazione. Copiare e salvare il GUID nel campo **ID applicazione (client)** , perché sarà necessario per le guide introduttive.

3. Fare quindi clic su **Autorizzazioni API** per aggiungere le API e le autorizzazioni a cui il client dovrà accedere. Fare clic su **Aggiungi un'autorizzazione** per aprire il pannello "Richiedi le autorizzazioni dell'API".

4. A questo punto si aggiungeranno le API e le autorizzazioni MIP che verranno richieste dall'applicazione in fase di esecuzione:
   - Nella pagina **Selezionare un'API** fare clic su **Azure Rights Management Services**.
   - Nella pagina dell'API **Azure Rights Management Services** fare clic su **Autorizzazioni delegate**.
   - Nella sezione **Selezionare le autorizzazioni** selezionare l'autorizzazione **user_impersonation**. Questo diritto consente all'applicazione di creare e accedere al contenuto protetto per conto di un utente.
   - Fare clic su **Aggiungi autorizzazioni** per salvare.

5. Ripetere il passaggio 4, ma questa volta quando si raggiunge la pagina **Selezionare un'API** sarà necessario cercare l'API.
   - Nella pagina **Selezionare un'API** fare clic su **API usate dall'organizzazione**, quindi nella casella di ricerca digitare "**Microsoft Information Protection Sync Service**" e selezionarlo.
   - Nella pagina dell'API **Microsoft Information Protection Sync Service** fare clic su **Autorizzazioni delegate**.
   - Espandere il nodo **UnifiedPolicy** e selezionare **UnifiedPolicy.User.Read**
   - Fare clic su **Aggiungi autorizzazioni** per salvare.

6. Quando si torna alla pagina **Autorizzazioni API** fare clic su **Concedi consenso amministratore per (nome del tenant)** , quindi su **Sì**. Questo passaggio concede il pre-consenso all'applicazione che usa questa registrazione per accedere alle API con le autorizzazioni specificate. Se è stato effettuato l'accesso come amministratore globale, il consenso viene registrato per tutti gli utenti nel tenant che eseguono l'applicazione. In caso contrario, si applica solo al proprio account utente.

Al termine, la registrazione dell'applicazione e le autorizzazioni per le API dovrebbero essere simili agli esempi seguenti:

   [![Registrazione dell'app in Azure AD](media/setup-mip-client/aad-app-registration-overview.png)](media/setup-mip-client/aad-app-registration-overview.png#lightbox) [![Registrazione dell'app in Azure AD](media/setup-mip-client/aad-app-api-permissions.png)](media/setup-mip-client/aad-app-api-permissions.png#lightbox)

Per altre informazioni sull'aggiunta di API e autorizzazioni a una registrazione, vedere [Configurare un'applicazione client per accedere alle API Web](/azure/active-directory/develop/quickstart-v1-update-azure-ad-app#configure-a-client-application-to-access-web-apis). In questo articolo sono disponibili informazioni su come aggiungere le API e le autorizzazioni necessarie per un'applicazione client.

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Richiedere un contratto per l'integrazione di Information Protection (IPIA, Information Protection Integration Agreement)

Prima di poter rilasciare un'applicazione sviluppata con MIP, è necessario richiedere e concludere un contratto formale con Microsoft.

1. Per ottenere il contratto, inviare un messaggio di posta elettronica all'indirizzo [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Requesting%20IPIA%20for%20<company-name>) con le informazioni seguenti:

   **Oggetto:** Requesting IPIA for *nome azienda*

   Nel corpo del messaggio di posta elettronica includere:
   - Nome dell'applicazione e del prodotto
   - Nome e cognome del richiedente
   - Indirizzo di posta elettronica del richiedente

2. Dopo aver ricevuto la richiesta del contratto, Microsoft invierà un modulo come documento Word. Leggere i termini e le condizioni del contratto di integrazione di Information Protection e restituire il modulo all'indirizzo [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=IPIA%20Response%20for%20<company-name>) con le informazioni seguenti:

   - Ragione sociale dell'azienda
   - Stato/provincia (Stati Uniti o Canada) o paese di costituzione
   - URL dell'azienda
   - Indirizzo di posta elettronica del contatto
   - Ulteriori indirizzi dell'azienda (facoltativo)
   - Nome dell'applicazione dell'azienda
   - Breve descrizione dell'applicazione
   - *ID tenant di Azure*
   - *ID app* per l'applicazione
   - Contatti, indirizzo di posta elettronica e numero di telefono dell'azienda per la corrispondenza relativa a situazioni critiche

3. Al ricevimento del modulo, Microsoft invierà il collegamento al contratto di integrazione di Information Protection finale per la firma digitale. Dopo la firma da parte dell'azienda il contratto verrà sottoscritto anche dal rappresentante Microsoft appropriato e sarà così concluso.

### <a name="already-have-a-signed-ipia"></a>È già stato sottoscritto un contratto di integrazione di Information Protection?

Se è già stato sottoscritto un contratto di integrazione di Information Protection e si vuole aggiungere un nuovo *ID app* per un'applicazione da rilasciare, inviare un messaggio di posta elettronica all'indirizzo [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Updating%20IPIA%20for%20<company-name>) e fornire le informazioni seguenti:

- Nome dell'applicazione dell'azienda
- Breve descrizione dell'applicazione
- ID tenant di Azure (anche se è uguale)
- ID app per l'applicazione
- Contatti, indirizzo di posta elettronica e numero di telefono dell'azienda per la corrispondenza relativa a situazioni critiche

Dopo aver inviato il messaggio di posta elettronica, si riceverà conferma della ricezione entro 72 ore.

## <a name="ensure-your-app-has-the-required-runtime"></a>Verificare la presenza del runtime necessario per l'app

> [!NOTE]
> Questo passaggio è necessario solo se l'applicazione viene distribuita in un computer senza Visual Studio o se l'installazione di Visual Studio non include i componenti di runtime di Visual C++.

Le applicazioni compilate con MIP SDK richiedono l'installazione del runtime di Visual C++ 2015 o Visual C++ 2017, se non è già presente.
- [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/download/details.aspx?id=53587)
- [Microsoft Visual C++ Redistributable per Visual Studio 2017](https://visualstudio.microsoft.com/downloads/#microsoft-visual-c-redistributable-for-visual-studio-2017)

Questi funzioneranno solo se l'applicazione è stata compilata come Release. Se l'applicazione è compilata come Debug, le DLL di debug del runtime di Visual C++ devono essere incluse con l'applicazione o installate nel computer.

## <a name="next-steps"></a>Passaggi successivi

- Per sviluppatori C++
  - Assicurarsi di leggere [Concetti relativi agli osservatori](concept-async-observers.md) prima di iniziare la sezione Avvio rapido, per ottenere informazioni sulla natura asincrona delle API C++.
  - Quando si è pronti ad acquisire familiarità con l'SDK, iniziare con [Avvio rapido: Inizializzazione dell'applicazione client (C++)](quick-app-initialization-cpp.md).
- Gli sviluppatori C#, quando sono pronti ad acquisire familiarità con l'SDK, possono iniziare con [Avvio rapido: Inizializzazione dell'applicazione client (C#)](quick-app-initialization-csharp.md).