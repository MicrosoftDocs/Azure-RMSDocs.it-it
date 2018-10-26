---
title: Installazione e configurazione di Microsoft Information Protection (MIP) SDK
description: Informazioni sui prerequisiti di installazione e configurazione per poter usare le applicazioni compilate con Microsoft Information Protection SDK.
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 430e130a5ba2026c0a3c69a59dddd6f9d6b4e8f0
ms.sourcegitcommit: cc65c3851d4b8169a1a62c83afaf0f75402f7631
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/20/2018
ms.locfileid: "49476205"
---
# <a name="microsoft-information-protection-mip-sdk-setup-and-configuration"></a>Installazione e configurazione di Microsoft Information Protection (MIP) SDK 

Gli articoli dedicati a guide introduttive ed esercitazioni sono incentrati sulla creazione di applicazioni che usano le librerie e le API di MIP SDK. Questo articolo illustra come installare e configurare l'abbonamento a Office 365 e una workstation client, in preparazione per l'uso dell'SDK.

MIP SDK è supportato nelle piattaforme seguenti:  

[!INCLUDE [MIP SDK platform support](../include/mip-sdk-platform-support.md)]

Assicurarsi di consultare gli argomenti seguenti prima di iniziare:

- [Che cos'è il Centro conformità e sicurezza di Office 365?](https://docs.microsoft.com/office365/securitycompliance/security-and-compliance)
- [Che cos'è Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
- [Come funziona la protezione in Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="sign-up-for-an-office-365-subscription"></a>Iscriversi per un abbonamento a Office 365

Molti degli esempi dell'SDK richiedono l'accesso a un abbonamento a Office 365. Se non è già stato fatto, assicurarsi di iscriversi per uno dei tipi di abbonamento seguenti:

| Nome | Iscrizione |
|------|---------|
| Office 365 Enterprise E3 - Versione di valutazione (versione di valutazione gratuita di 30 giorni) | https://go.microsoft.com/fwlink/p/?LinkID=403802 |
| Office 365 Enterprise E3 o E5 | https://products.office.com/business/office-365-enterprise-e3-business-software |
| Enterprise Mobility and Security E3 o E5 | https://www.microsoft.com/cloud-platform/enterprise-mobility-security |
| Azure Information Protection Premium P1 o P2 | https://azure.microsoft.com/pricing/details/information-protection/ |
| Microsoft 365 E3, E5 o F1 | https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans | 

## <a name="configure-sensitivity-labels"></a>Configurare le etichette di riservatezza

Se si usa già Azure Information Protection, è necessario eseguire alcune operazioni per eseguire la migrazione delle etichette nel Centro sicurezza e conformità di Office 365. Per altre informazioni sul processo, vedere [Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365](/azure/information-protection/configure-policy-migrate-labels). 

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

3. Installare il [modulo di PowerShell ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2). 

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

4. Scaricare gli esempi dell'SDK da GitHub 

   - Se non è già disponibile, creare prima di tutto un [profilo GitHub](https://github.com/join).
   - Installare quindi la versione più recente degli [strumenti client Git di Software Freedom Conservancy (Git Bash)](https://git-scm.com/download/)
   - Usare Git Bash per scaricare gli esempi di interesse:
     - Usare la query seguente per visualizzare i repository: https://github.com/Azure-Samples?utf8=%E2%9C%93&q=MipSdk. 
     - Con Git Bash, usare `git clone https://github.com/azure-samples/<repo-name>` per scaricare ogni repository di esempi.

5. Scaricare i file binari e le intestazione dell'SDK

   Un file ZIP che contiene i file binari e le intestazioni dell'SDK per tutte le piattaforme è disponibile all'indirizzo https://aka.ms/mipsdkbinaries. Il file ZIP contiene vari altri file ZIP, uno per ogni piattaforma e API. I file hanno i nomi seguenti, dove \<API\> = `file`, `protection` o `upe` e \<OS\> = la piattaforma: `mip_sdk_<API>_<OS>_1.0.0.0.zip (or .tar.gz)`.

   Ad esempio, il file ZIP per i file binari e le intestazioni dell'API Protezione per la piattaforma Debian sarebbe denominato `mip_sdk_protection_debian9_1.0.0.0.tar.gz`.

   Ogni file ZIP o file tarball contiene tre sottodirectory:

   - **Bins:** file binari compilati per ogni architettura della piattaforma, dove applicabile.
   - **Include:** file di intestazione di Microsoft Information Protection SDK
   - **Samples:** codice sorgente per le applicazioni di esempio

   Per lo sviluppo in Visual Studio, l'SDK può essere installato anche tramite la Console di Gestione pacchetti NuGet:

    ```console
    Install-Package Microsoft.InformationProtection.File
    Install-Package Microsoft.InformationProtection.Policy
    Install-Package Microsoft.InformationProtection.Protection
    ```  
    
6. Aggiungere i percorsi dei file binari dell'SDK (librerie a collegamento dinamico (DLL)), alla variabile di ambiente PATH. La variabile PATH consente alle applicazioni client di trovare le DLL dipendenti in fase di esecuzione:
   - Fare clic sull'icona di Windows nell'angolo inferiore sinistro.
   - Digitare "Path" e premere "INVIO", quando viene visualizzata la voce **Modifica le variabili di ambiente relative al sistema**.
   - Nella finestra di dialogo **Proprietà del sistema** fare clic su **Variabili di ambiente**.
   - Nella finestra di dialogo **Variabili di ambiente** fare clic sulla riga della variabile **Path** in **Variabili dell'utente per \<utente\>** e quindi fare clic su **Modifica**.
   - Nella finestra di dialogo **Modifica variabile di ambiente** fare clic su **Nuovo**, che consente di creare una nuova riga modificabile. Usando il percorso completo per ognuna delle sottodirectory `file\bins\debug\amd64`, `protection\bins\debug\amd64` e `upe\bins\debug\amd64`, aggiungere una nuova riga per ognuna. Le directory dell'SDK sono archiviate nel formato `<API>\bins\<target>\<platform>`, dove:
     - \<API\> = `file`, `protection`, `upe`
     - \<target\> = `debug`, `release`
     - \<platform\> = `amd64` (ad esempio: x64), `x86` e così via.
   
   - Dopo aver completato la modifica della variabile **Path** fare clic su **OK**. Fare quindi clic su **OK** quando si torna alla finestra di dialogo **Variabili di ambiente**.

## <a name="register-a-client-application-with-azure-active-directory"></a>Registrare un'applicazione client in Azure Active Directory

Come parte del processo di provisioning dell'abbonamento a Office 365 viene creato un tenant di Azure AD associato. Il tenant di Azure AD consente la gestione delle identità e dell'accesso per gli *account utente* e gli *account di applicazione* di Office 365. Per le applicazioni che richiedono l'accesso ad API protette (ad esempio le API MIP) è necessario un account di applicazione.

Per il processo di autenticazione e autorizzazione in fase di esecuzione, gli account sono rappresentati da un'*entità di sicurezza*, derivata dalle informazioni di identità dell'account. Le entità di sicurezza che rappresentano un account di applicazione vengono definite [*entità servizio*](/azure/active-directory/develop/developer-glossary#service-principal-object). 

Per registrare un account di applicazione in Azure AD per l'uso con gli esempi e le guide introduttive di MIP SDK:

  > [!IMPORTANT] 
  > Per accedere alla gestione del tenant Azure AD per la creazione dell'account, sarà necessario accedere al portale di Azure con un account utente membro del [ruolo "Proprietario" nella sottoscrizione](/azure/billing/billing-add-change-azure-subscription-administrator). A seconda della configurazione del tenant, potrebbe anche essere necessario essere membri del ruolo della directory "Amministratore globale" per [registrare un'applicazione](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
  > È consigliabile eseguire le operazioni di test con un account con restrizioni. Assicurarsi che l'account disponga solo dei diritti per accedere agli endpoint SCC necessari. Le password passate come testo non crittografato tramite riga di comando possono essere raccolte dai sistemi di registrazione.

1. Seguire la procedura in [Guida introduttiva: registrare un'app con l'endpoint v1.0 di Azure Active Directory](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#adding-an-application). A scopo di test, usare i valori seguenti per le proprietà specificate quando si eseguono i passaggi della guida: 
    - **Tipo di applicazione** - selezionare "Nativa", in quanto le applicazioni usate nelle dimostrazioni dell'SDK sono applicazioni console installate in modo nativo. Le applicazioni native sono considerate client "pubblici" da OAuth2, perché non sono in grado di archiviare/usare le credenziali dell'applicazione in modo sicuro. Diversamente da un'applicazione basata su server "riservata", ad esempio un'applicazione Web, che è registrata con le proprie credenziali. 
    - **URI di reindirizzamento** - Dato che l'SDK usa applicazioni client console semplici, usare un URI nel formato `<app-name>://authorize`.

2. Al termine, si tornerà alla pagina **App registrata** per la registrazione della nuova applicazione. Copiare e salvare il GUID nel campo **ID applicazione**, perché sarà necessario per le guide introduttive. 

3. Fare quindi clic su **Impostazioni** per aggiungere le API e le autorizzazioni a cui il client dovrà accedere. Nella pagina **Impostazioni** fare clic su **Autorizzazioni necessarie**.

4. A questo punto si aggiungeranno le API e le autorizzazioni MIP che verranno richieste dall'applicazione in fase di esecuzione:
   - Nella pagina **Autorizzazioni necessarie** fare clic su **Aggiungi**. 
   - Nella pagina **Aggiungi accesso all'API** fare clic su **Selezionare un'API**.
   - Nella pagina **Selezionare un'API** fare clic sull'API "**Microsoft Rights Management Services**" e quindi su **Seleziona**.
   - Nella pagina**Abilita accesso** per le autorizzazioni disponibili dell'API fare clic su "**Create and access protected content for users**" (Creazione e accesso a contenuto protetto per gli utenti), fare clic su **Seleziona** e quindi fare clic su **Fine**.

5. Ripetere il passaggio 4, ma questa volta quando si raggiunge la pagina **Selezionare un'API** sarà necessario cercare l'API.
   - Nella pagina **Selezionare un'API**, nella casella di ricerca digitare "**Microsoft Information Protection Sync Service**", quindi fare clic sull'API e fare clic su **Seleziona**.
   - Nella pagina **Abilita accesso** per le autorizzazioni disponibili dell'API fare clic su "**Read all unified policies a user has access to**" (Lettura di tutti i criteri unificati a cui ha accesso un utente), fare clic su **Seleziona** e quindi fare clic su **Fine**

6. Quando si torna alla pagina **Autorizzazioni necessarie** fare clic su **Concedi autorizzazioni** e quindi su **Sì**. Questo passaggio concede il pre-consenso all'applicazione che usa questa registrazione per accedere alle API con le autorizzazioni specificate. Se è stato effettuato l'accesso come amministratore globale, il consenso viene registrato per tutti gli utenti nel tenant che eseguono l'applicazione. In caso contrario, si applica solo al proprio account utente. 

Al termine, la registrazione dell'applicazione e le autorizzazioni per le API dovrebbero essere simili all'esempio seguente:

   [![Registrazione di un'app in Azure AD](media/setup-mip-client/aad-app-registration.png)](media/setup-mip-client/aad-app-registration.png#lightbox)


Per altre informazioni sull'aggiunta di API e autorizzazioni a una registrazione, vedere [Aggiornare un'applicazione in Azure Active Directory, sezione Configurare un'applicazione client per accedere alle API Web](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#updating-an-application). In questo articolo sono disponibili informazioni su come aggiungere le API e le autorizzazioni necessarie per un'applicazione client.  

## <a name="next-steps"></a>Passaggi successivi

- Prima di iniziare la sezione delle guide introduttive, assicurarsi di leggere le informazioni sugli [osservatori in MIP SDK](concept-async-observers.md), perché MIP SDK è progettato per essere quasi interamente asincrono.
- Se si è pronti per qualche esperienza pratica con l'SDK, iniziare con [Guida introduttiva: Inizializzazione delle applicazioni client (C++)](quick-app-initialization-cpp.md).
