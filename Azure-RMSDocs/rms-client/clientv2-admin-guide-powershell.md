---
title: Usare PowerShell con il client di assegnazione di etichette unificato di Azure Information Protection
description: Istruzioni e informazioni per gli amministratori per gestire il client di assegnazione di etichette unificato di Azure Information Protection tramite PowerShell.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f90697e1e4df90ab8876843b45957b93c8ba8b07
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236874"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guida dell'amministratore: Uso di PowerShell con il client unificato di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Quando si installa il client di assegnazione di etichette unificato di Azure Information Protection, vengono installati automaticamente i comandi di PowerShell. Ciò consente di gestire il client eseguendo i comandi che è possibile inserire negli script per l'automazione.

I cmdlet installati con il modulo di PowerShell **AzureInformationProtection**, che include cmdlet per l'assegnazione di etichette. Ad esempio:

|Cmdlet per le etichette|Esempio di utilizzo|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Per una cartella condivisa, identifica tutti i file con un'etichetta specifica.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Per una cartella condivisa, esaminare il contenuto dei file e quindi etichettare automaticamente i file senza etichetta, in base alle condizioni specificate.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Per una cartella condivisa, applica un'etichetta specificata a tutti i file privi di etichetta.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Assegnare etichette ai file in modo interattivo, usando un account utente diverso con i propri.|

> [!TIP]
> Per usare cmdlet con percorsi di lunghezza superiore a 260 caratteri, usare l'[impostazione di Criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) seguente disponibile a partire da Windows 10 versione 1607:<br /> **Criteri del Computer locale** > **configurazione del Computer** > **modelli amministrativi** > **tutte le impostazioni**  >  **i percorsi lunghi abilitare Win32** 
> 
> Per Windows Server 2016 è possibile usare la stessa impostazione di Criteri di gruppo quando si installano i modelli amministrativi più recenti (con estensione admx) per Windows 10.
>
> Per altre informazioni, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) della documentazione per sviluppatori di Windows 10.

Questo modulo viene installato in **\Programmi (x86)\Microsoft Azure Information Protection** e aggiunge questa cartella alla variabile di sistema **PSModulePath**. Il file DLL per questo modulo si chiama **AIP.dll**.

> [!IMPORTANT]
> Il modulo AzureInformationProtection non supporta la configurazione delle impostazioni avanzate per i criteri di etichette o etichette. Per queste impostazioni, è necessaria la sicurezza e Office 365 PowerShell centro conformità. Per altre informazioni, vedere [configurazioni personalizzate per Azure Information Protection unified client l'assegnazione di etichette](clientv2-admin-guide-customizations.md).

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Prerequisiti per l'uso del modulo AzureInformationProtection

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, esistono prerequisiti aggiuntivi per quando si usano i cmdlet di assegnazione di etichette per Azure Information Protection:

1. Il servizio Azure Rights Management deve essere attivato.

2. Per rimuovere la protezione dai file per altri utenti tramite il proprio account: 

    - La funzionalità relativa agli utenti con privilegi avanzati deve essere abilitata per l'organizzazione e l'account deve essere configurato come account con privilegi avanzati per Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prerequisito 1: il servizio Azure Rights Management deve essere attivato

Se il tenant di Azure Information Protection non è attivato per applicare la protezione, vedere le istruzioni [attivazione di Azure Rights Management](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prerequisito 2: per rimuovere la protezione dai file per altri utenti usando il proprio account

Gli scenari tipici per la rimozione della protezione dai file per altri utenti includono l'individuazione dei dati o il ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica protezione oppure rimuovendo l'etichetta.

Per poter rimuovere la protezione dai file, è necessario avere diritti di utilizzo per Rights Management oppure un account utente con privilegi avanzati. Per l'individuazione dei dati o il ripristino dei dati, viene in genere usata la funzionalità per utenti con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../configure-super-users.md).

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection

Nota: Le informazioni contenute in questa sezione sono per la versione di anteprima solo del client Azure Information Protection unified imprevisto delle etichette.

È possibile eseguire i cmdlet per l'assegnazione delle etichette in modo non interattivo tramite il cmdlet **Set-AIPAuthentication**.

Per impostazione predefinita, quando si eseguono i cmdlet per l'assegnazione di etichette, i comandi vengono eseguiti nel contesto utente personale in una sessione interattiva di PowerShell. Per eseguirli senza interventi da parte dell'utente, creare un nuovo account utente di Azure AD per questo scopo. Nel contesto di tale utente, quindi, eseguire il cmdlet Set-AIPAuthentication per impostare e archiviare le credenziali usando un token di accesso da Azure AD. Questo account utente viene quindi autenticato e avviato per il servizio di protezione di Azure Information Protection. L'account Scarica i criteri di Azure Information Protection ed eventuali modelli di protezione usati dalle etichette.

> [!NOTE]
> Se si usano [criteri con ambito](../configure-policy-scope.md) tenere presente che potrebbe essere necessario aggiungere questo account ai criteri con ambito.

La prima volta che si esegue questo cmdlet viene richiesto di accedere ad Azure Information Protection. Specificare il nome dell'account utente e la password creata per l'account automatico. Successivamente, questo account può quindi eseguire i cmdlet di assegnazione di etichette in modo non interattivo fino alla scadenza del token di autenticazione in Azure AD. 

Per l'account utente sia in grado di accedere in modo interattivo la prima volta, l'account deve avere il **accedere localmente** assegnazione di utenti a destra. Questo diritto è standard per gli account utente, ma i criteri aziendali potrebbero non consentire questa configurazione per gli account del servizio. Se è questo il caso, è possibile eseguire Set-AIPAuthentication con il *OnBehalfOf* parametro in modo che l'autenticazione viene completata senza la richiesta di accesso.

Alla scadenza del token di Azure AD, eseguire nuovamente il cmdlet per acquisire un nuovo token.

Se si esegue questo cmdlet senza parametri, l'account acquisisce un token di accesso valido per 90 giorni o fino alla scadenza della password.  

Per determinare la scadenza del token di accesso, eseguire questo cmdlet con parametri. Questa configurazione consente di configurare il token di accesso in Azure AD per un anno, due anni o senza alcuna scadenza. Si richiedono due applicazioni registrate in Azure Active Directory: un'applicazione **app Web/API** e un'**applicazione nativa**. I parametri per Set-AIPAuthentication utilizzano valori di queste applicazioni.

Dopo aver eseguito questo cmdlet, è possibile eseguire i cmdlet di assegnazione di etichette nel contesto dell'account del servizio che è stato creato.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Per creare e configurare le applicazioni di Azure AD per Set-AIPAuthentication

1. In una nuova finestra del browser accedere al [Portale di Azure](https://portal.azure.com/).

2. Per il tenant di Azure AD che usa con Azure Information Protection, passare a **Azure Active Directory** > **Gestisci** > **registrazioniperl'App**. 

3. Selezionare **+ registrazione nuova**, per creare l'applicazione di app/API Web. Nel **registrare un'applicazione** blade, specificare i valori seguenti e quindi fare clic su **registrare**:

   - **Nome**: `AIPOnBehalfOf`
        
        Se preferibile, specificare un nome diverso. Deve essere univoco per ogni tenant.
    
    - **Tipi di account supportati**: **Account in questa directory dell'organizzazione solo**
    
    - **(Facoltativo) URI di reindirizzamento**: **Web** e `http://localhost`

4. Nel **AIPOnBehalfOf** pannello, copiare il valore per il **ID applicazione (client)** . Il valore è simile all'esempio seguente: `57c3c1c3-abf9-404e-8b2b-4652836c8c66`. Questo valore viene usato per il *WebAppId* parametro quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento futuro.

5. Sempre nella **AIPOnBehalfOf** pannello dal **Gestisci** dal menu **Authentication**.

6. Nel **AIPOnBehalfOf - autenticazione** pannello, nelle **impostazioni avanzate** selezionare il **i token ID** casella di controllo e quindi selezionare **salvare**.

7. Sempre nella **AIPOnBehalfOf - autenticazione** pannello dalle **Gestisci** dal menu **certificati e i segreti**.

8. Nel **AIPOnBehalfOf - i certificati e i segreti** pannello, nelle **i segreti Client** sezione, selezionare **+ nuovo segreto client**. 

9. Per la **aggiungere un segreto client**, specificare le informazioni seguenti e quindi selezionare **Add**:
    
    - **Descrizione**: `Azure Information Protection client`
    - **Scadenza**: Specificare la scelta della durata (1 anno, 2 anni o Nessuna scadenza)

9. Riaccenderle il **AIPOnBehalfOf - i certificati e i segreti** pannello nella **i segreti Client** sezione, copiare la stringa per il **valore**. Questa stringa è simile all'esempio seguente: `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`. Per assicurarsi di copiare tutti i caratteri, selezionare l'icona per **copia negli Appunti**. 
    
    È importante salvare la stringa, perché non verrà più visualizzata e non potrà essere recuperata. Come con qualsiasi informazione riservata in uso, archiviare il valore salvato in modo sicuro e limitare l'accesso a esso.

10. Sempre nella **AIPOnBehalfOf - i certificati e i segreti** pannello dalle **Gestisci** dal menu **esporre un'API**.

11. Nel **AIPOnBehalfOf - espongono un'API** pannello seleziona **impostare** per il **URI ID applicazione** opzione e nel **URI ID applicazione** valore, cambiare **api** al **http**. Questa stringa è simile all'esempio seguente: `http://d244e75e-870b-4491-b70d-65534953099e`. 
    
    Selezionare **Salva**.

12. Nella **AIPOnBehalfOf - espongono un'API** blade, selezionare **+ Aggiungi un ambito**.

13. Nel **aggiungere un ambito** blade, specificare quanto segue, usando le stringhe suggerite come esempi e quindi selezionare **Aggiungi ambito**:
    - **Nome dell'ambito**: `user-impersonation`
    - **Che può fornire il consenso?** : **Gli amministratori e utenti**
    - **Nome visualizzato di consenso dell'amministratore**: `Access Azure Information Protection scanner`
    - **Descrizione del consenso dell'amministratore**: `Allow the application to access the scanner for the signed-in user`
    - **Nome visualizzato dell'utente il consenso**: `Access Azure Information Protection scanner`
    - **Descrizione del consenso dell'utente**: `Allow the application to access the scanner for the signed-in user`
    - **stato**: **Abilitato** (predefinito)

14. Nella **AIPOnBehalfOf - espongono un'API** pannello, chiudere questo pannello.

15. Nel **registrazioni per l'App** blade, selezionare **+ registrazione nuova applicazione** per creare l'applicazione nativa.

16. Nel **registrare un'applicazione** blade, specificare le impostazioni seguenti e quindi selezionare **registrare**:
    - **Nome**: `AIPClient`
    - **Tipi di account supportati**: **Account in questa directory dell'organizzazione solo**
    - **(Facoltativo) URI di reindirizzamento**: **Un client pubblico (per dispositivi mobili e desktop)** e `http://localhost`

17. Nel **AIPClient** pannello, copiare il valore della **ID applicazione (client)** . Il valore è simile all'esempio seguente: `8ef1c873-9869-4bb1-9c11-8313f9d7f76f`. 
    
    Questo valore viene utilizzato per il parametro NativeAppId quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento futuro.

18. Sempre nella **AIPClient** pannello dal **Gestisci** dal menu **Authentication**.

19. Nel **AIPClient - autenticazione** blade, specificare le informazioni seguenti e quindi selezionare **salvare**:
    - Nel **impostazioni avanzate** sezione, selezionare **i token ID**.
    - Nel **tipo di client predefinito** sezione, selezionare **Yes**.

20. Sempre nella **AIPClient - autenticazione** pannello dalle **Gestisci** dal menu **autorizzazioni delle API**.

21. Nel **AIPClient - le autorizzazioni** blade, selezionare **+ Aggiungi un'autorizzazione**.

22. Nel **le autorizzazioni API Request** pannello seleziona **API My**.

23. Nel **selezionare un'API** , selezionare **APIOnBehalfOf**, quindi selezionare la casella di controllo **-rappresentazione dell'utente**, come l'autorizzazione. Selezionare **aggiungere autorizzazioni**. 

24. Riaccenderle il **autorizzazioni delle API** pannello nella **concedere il consenso** sezione, selezionare **concedere il consenso dell'amministratore per \< *il nome del tenant* >**  e selezionare **Sì** per la richiesta di conferma.

La configurazione delle due app è stata completata e i valori necessari per eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con i parametri *WebAppId*, *WebAppKey* e *NativeAppId* sono disponibili. Da questi esempi:

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

Eseguire questo comando nel contesto dell'account per l'assegnazione di etichette e la protezione di documenti in modalità non interattiva. Un esempio è un account utente per gli script di PowerShell o l'account del servizio per eseguire lo scanner di Azure Information Protection.

La prima volta che si esegue questo comando viene richiesto di eseguire l'accesso, creando e archiviando in modo sicuro il token di accesso per l'account in %localappdata%\Microsoft\MSIP. Dopo questo accesso iniziale è possibile assegnare etichette e proteggere i file in modalità non interattiva nel computer. Tuttavia, se si utilizza un account del servizio a etichetta e proteggere i file e l'account del servizio non è possibile accedere in modo interattivo, usare il *OnBehalfOf* parametro con Set-AIPAuthentication:

1. Creare una variabile per archiviare le credenziali di un account di Active Directory che viene concessa l'assegnazione di diritto utente di accedere in modo interattivo. Ad esempio:
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. Eseguire il cmdlet Set-AIPAuthentication, con la *OnBeHalfOf* parametro, che specifica come il rispettivo valore variabile appena creata. Ad esempio:
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>Passaggi successivi
Per il tipo di Guida dei cmdlet all'interno di una sessione di PowerShell `Get-Help <cmdlet name> -online`. Ad esempio: 

    Get-Help Set-AIPFileLabel -online

Per altre informazioni necessarie per supportare il client Azure Information Protection, vedere gli argomenti seguenti:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)
