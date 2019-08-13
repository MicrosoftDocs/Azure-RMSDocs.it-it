---
title: Usare PowerShell con il client di etichettatura unificato Azure Information Protection
description: Istruzioni e informazioni per gli amministratori per la gestione del client Azure Information Protection Unified Labeling usando PowerShell.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ee514720cf13e819f3d64e77635ae96a26e4d0ed
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793201"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guida dell'amministratore: Uso di PowerShell con il client unificato Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Quando si installa il client Azure Information Protection Unified Labeling, i comandi di PowerShell vengono installati automaticamente. Ciò consente di gestire il client eseguendo i comandi che è possibile inserire negli script per l'automazione.

I cmdlet vengono installati con il modulo di PowerShell **AzureInformationProtection**, che include i cmdlet per l'assegnazione di etichette. Ad esempio:

|Cmdlet per le etichette|Esempio di utilizzo|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Per una cartella condivisa, identifica tutti i file con un'etichetta specifica.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Per una cartella condivisa, esaminare il contenuto dei file e quindi etichettare automaticamente i file senza etichetta, in base alle condizioni specificate.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Per una cartella condivisa, applica un'etichetta specificata a tutti i file privi di etichetta.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Etichettare i file in modo interattivo, usando un account utente diverso.|

> [!TIP]
> Per usare cmdlet con percorsi di lunghezza superiore a 260 caratteri, usare l'[impostazione di Criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) seguente disponibile a partire da Windows 10 versione 1607:<br />  > **Configurazione computer criteri**computer locale modelli amministrativi**tutte le impostazioni Abilita percorsi** **lunghi Win32**  >  >  >  
> 
> Per Windows Server 2016 è possibile usare la stessa impostazione di Criteri di gruppo quando si installano i modelli amministrativi più recenti (con estensione admx) per Windows 10.
>
> Per altre informazioni, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) della documentazione per sviluppatori di Windows 10.

Questo modulo viene installato in **\Programmi (x86)\Microsoft Azure Information Protection** e aggiunge questa cartella alla variabile di sistema **PSModulePath**. Il file DLL per questo modulo si chiama **AIP.dll**.

> [!IMPORTANT]
> Il modulo AzureInformationProtection non supporta la configurazione delle impostazioni avanzate per le etichette o i criteri di etichetta. Per queste impostazioni, è necessario Office 365 Centro sicurezza e conformità PowerShell. Per ulteriori informazioni, vedere [Configurazioni personalizzate per il client di Unified Labelling di Azure Information Protection](clientv2-admin-guide-customizations.md).

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Prerequisiti per l'uso del modulo AzureInformationProtection

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, esistono prerequisiti aggiuntivi per l'uso dei cmdlet di assegnazione di etichette per Azure Information Protection:

1. Il servizio Azure Rights Management deve essere attivato.

2. Per rimuovere la protezione dai file per altri utenti tramite il proprio account: 

    - La funzionalità relativa agli utenti con privilegi avanzati deve essere abilitata per l'organizzazione e l'account deve essere configurato come account con privilegi avanzati per Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prerequisito 1: il servizio Azure Rights Management deve essere attivato

Se il tenant di Azure Information Protection non è attivato per applicare la protezione, vedere le istruzioni per l' [attivazione di Azure Rights Management](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prerequisito 2: per rimuovere la protezione dai file per altri utenti usando il proprio account

Gli scenari tipici per la rimozione della protezione dai file per altri utenti includono l'individuazione dei dati o il ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica protezione oppure rimuovendo l'etichetta.

Per poter rimuovere la protezione dai file, è necessario avere diritti di utilizzo per Rights Management oppure un account utente con privilegi avanzati. Per l'individuazione dei dati o il ripristino dei dati, viene in genere usata la funzionalità per utenti con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../configure-super-users.md).

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection

È possibile eseguire i cmdlet per l'assegnazione delle etichette in modo non interattivo tramite il cmdlet **Set-AIPAuthentication**.

Per impostazione predefinita, quando si eseguono i cmdlet per l'assegnazione di etichette, i comandi vengono eseguiti nel contesto utente personale in una sessione interattiva di PowerShell. Per eseguirli senza interventi da parte dell'utente, creare un nuovo account utente di Azure AD per questo scopo. Nel contesto di tale utente, quindi, eseguire il cmdlet Set-AIPAuthentication per impostare e archiviare le credenziali usando un token di accesso da Azure AD. Questo account utente viene quindi autenticato e avviato per il servizio di protezione da Azure Information Protection. L'account Scarica i criteri di Azure Information Protection e tutti i modelli di protezione usati dalle etichette.

> [!NOTE]
> Se si usano [criteri con ambito](../configure-policy-scope.md) tenere presente che potrebbe essere necessario aggiungere questo account ai criteri con ambito.

La prima volta che si esegue questo cmdlet viene richiesto di accedere ad Azure Information Protection. Specificare il nome dell'account utente e la password creati per l'account automatico. Successivamente, questo account potrà quindi eseguire i cmdlet di assegnazione di etichette in modo non interattivo fino alla scadenza del token di autenticazione in Azure AD. 

Per consentire all'account utente di accedere in modo interattivo per la prima volta, l'account deve disporre dell'assegnazione diritto utente **accesso locale** . Questo diritto è standard per gli account utente, ma i criteri aziendali potrebbero non consentire questa configurazione per gli account del servizio. In tal caso, è possibile eseguire set-AIPAuthentication con il parametro *OnBehalfOf* in modo che l'autenticazione venga completata senza la richiesta di accesso.

Quando il token Azure AD scade, eseguire di nuovo il cmdlet per acquisire un nuovo token.

Se si esegue questo cmdlet senza parametri, l'account acquisisce un token di accesso valido per 90 giorni o fino alla scadenza della password.  

Per determinare la scadenza del token di accesso, eseguire questo cmdlet con parametri. Questa configurazione consente di configurare il token di accesso in Azure AD per un anno, due anni o non scadere mai. Sono necessarie due applicazioni registrate in Azure Active Directory: un'applicazione **app Web/API** e un'**applicazione nativa**. I parametri per set-AIPAuthentication utilizzano i valori di queste applicazioni.

Dopo aver eseguito questo cmdlet, è possibile eseguire i cmdlet di assegnazione di etichette nel contesto dell'account del servizio creato.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Per creare e configurare le applicazioni di Azure AD per Set-AIPAuthentication

1. In una nuova finestra del browser accedere al [Portale di Azure](https://portal.azure.com/).

2. Per il tenant Azure ad usato con Azure Information Protection, passare a **Azure Active Directory** > **Gestisci** > **registrazioni app**. 

3. Selezionare **+ nuova registrazione**per creare l'applicazione/API dell'app Web. Nel pannello **registra un'applicazione** specificare i valori seguenti e quindi fare clic su **registra**:

   - **Nome**:`AIPOnBehalfOf`
        
        Se preferibile, specificare un nome diverso. Deve essere univoco per ogni tenant.
    
    - **Tipi di account supportati**: **Solo account in questa directory organizzativa**
    
    - **URI di reindirizzamento (facoltativo)** : **Web** e`http://localhost`

4. Nel pannello **AIPOnBehalfOf** copiare il valore per l' **ID applicazione (client)** . Il valore è simile all'esempio seguente: `57c3c1c3-abf9-404e-8b2b-4652836c8c66`. Questo valore viene usato per il parametro webappid quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento successivo.

5. Sempre nel pannello **AIPOnBehalfOf** selezionare **autenticazione**dal menu **Gestisci** .

6. Nel pannello **AIPOnBehalfOf-Authentication** , nella sezione **Impostazioni avanzate** , selezionare la casella di controllo **token ID** , quindi selezionare **Salva**.

7. Sempre nel pannello **AIPOnBehalfOf-Authentication** scegliere **certificati & segreti**dal menu **Gestisci** .

8. Nel pannello **AIPOnBehalfOf-certificates & Secrets** , nella sezione **client Secrets** Selezionare **+ New client Secret**. 

9. Per **Aggiungi un segreto client**, specificare quanto segue e quindi selezionare **Aggiungi**:
    
    - **Descrizione**:`Azure Information Protection client`
    - **Scadenza**: Specificare la durata scelta (1 anno, 2 anni o nessuna scadenza)

9. Tornare al pannello **AIPOnBehalfOf-certificates & Secrets** , nella sezione **client Secrets** , copiare la stringa per il **valore**. Questa stringa ha un aspetto simile all'esempio seguente `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`:. Per assicurarsi di copiare tutti i caratteri, selezionare l'icona da **copiare negli Appunti**. 
    
    È importante salvare la stringa, perché non verrà più visualizzata e non potrà essere recuperata. Come per le informazioni riservate utilizzate, archiviare il valore salvato in modo sicuro e limitarne l'accesso.

10. Sempre nel pannello **AIPOnBehalfOf-certificates & Secrets** selezionare **expose an API**dal menu **Gestisci** .

11. Nel pannello **AIPOnBehalfOf-esporre un'API** selezionare **imposta** per l'opzione **URI ID applicazione** e nel valore **URI ID applicazione** , modificare **API** in **http**. Questa stringa ha un aspetto simile all'esempio seguente `http://d244e75e-870b-4491-b70d-65534953099e`:. 
    
    Selezionare **Salva**.

12. Tornare al pannello **AIPOnBehalfOf-esporre un'API** , selezionare **+ Aggiungi un ambito**.

13. Nel pannello **Aggiungi ambito** , specificare quanto segue, usando le stringhe suggerite come esempi, quindi selezionare **Aggiungi ambito**:
    - **Nome ambito**:`user-impersonation`
    - **Chi può acconsentire?** : **Amministratori e utenti**
    - **Nome visualizzato del consenso dell'amministratore**:`Access Azure Information Protection scanner`
    - **Descrizione del consenso dell'amministratore**:`Allow the application to access the scanner for the signed-in user`
    - **Nome visualizzato del consenso dell'utente**:`Access Azure Information Protection scanner`
    - **Descrizione del consenso dell'utente**:`Allow the application to access the scanner for the signed-in user`
    - **Stato**: **Abilitato** (impostazione predefinita)

14. Tornare al pannello **AIPOnBehalfOf-esporre un'API** . chiudere il pannello.

15. Nel pannello **registrazioni app** selezionare **+ registrazione nuova applicazione** per creare ora l'applicazione nativa.

16. Nel pannello **registra un'applicazione** specificare le impostazioni seguenti e quindi selezionare **registra**:
    - **Nome**:`AIPClient`
    - **Tipi di account supportati**: **Solo account in questa directory organizzativa**
    - **URI di reindirizzamento (facoltativo)** : **Client pubblico (mobile & desktop)** e`http://localhost`

17. Nel pannello **AIPClient** copiare il valore dell' **ID applicazione (client)** . Il valore è simile all'esempio seguente: `8ef1c873-9869-4bb1-9c11-8313f9d7f76f`. 
    
    Questo valore viene usato per il parametro NativeAppId quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento successivo.

18. Sempre nel pannello **AIPClient** selezionare **autenticazione**dal menu **Gestisci** .

19. Nel pannello **AIPClient-Authentication** specificare gli elementi seguenti e quindi selezionare Save ( **Salva**):
    - Nella sezione **Impostazioni avanzate** selezionare **token ID**.
    - Nella sezione **tipo di client predefinito** selezionare **Sì**.

20. Sempre nel pannello **AIPClient-Authentication** scegliere **autorizzazioni API**dal menu Gestisci.

21. Nel pannello **AIPClient-Permissions (autorizzazioni** ) selezionare **+ Aggiungi un'autorizzazione**.

22. Nel pannello **autorizzazioni richiesta API** selezionare **API personali**.

23. Nella sezione **selezionare un'API** selezionare **APIOnBehalfOf**, quindi selezionare la casella di controllo per la **rappresentazione utente**come autorizzazione. Selezionare **Aggiungi autorizzazioni**. 

24. Tornare al pannello **autorizzazioni API** , nella sezione **consenso della concessione** Selezionare Concedi il **consenso dell'amministratore per \< *il nome* > del tenant** e selezionare **Sì** per la richiesta di conferma.

La configurazione delle due app è stata completata e i valori necessari per eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con i parametri *WebAppId*, *WebAppKey* e *NativeAppId* sono disponibili. Dagli esempi seguenti:

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

Eseguire questo comando nel contesto dell'account per l'assegnazione di etichette e la protezione di documenti in modalità non interattiva. Un esempio è un account utente per gli script di PowerShell o l'account del servizio per eseguire lo scanner di Azure Information Protection.

La prima volta che si esegue questo comando viene richiesto di eseguire l'accesso, creando e archiviando in modo sicuro il token di accesso per l'account in %localappdata%\Microsoft\MSIP. Dopo questo accesso iniziale è possibile assegnare etichette e proteggere i file in modalità non interattiva nel computer. Tuttavia, se si usa un account del servizio per etichettare e proteggere i file e questo account del servizio non è in grado di eseguire l'accesso in modo interattivo, usare il parametro *OnBehalfOf* con set-AIPAuthentication:

1. Creare una variabile per archiviare le credenziali di un account Active Directory a cui viene concessa l'assegnazione a destra dell'utente per l'accesso interattivo. Ad esempio:
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. Eseguire il cmdlet Set-AIPAuthentication con il parametro *OnBeHalfOf* , specificando come valore la variabile appena creata. Ad esempio:
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>Passaggi successivi
Per la guida del cmdlet quando ci si trova in una sessione `Get-Help <cmdlet name> -online`di PowerShell, digitare. Ad esempio: 

    Get-Help Set-AIPFileLabel -online

Per altre informazioni necessarie per supportare il client Azure Information Protection, vedere gli argomenti seguenti:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)
