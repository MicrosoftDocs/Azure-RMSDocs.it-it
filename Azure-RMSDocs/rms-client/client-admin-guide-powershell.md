---
title: Usare PowerShell con il client Azure Information Protection
description: Istruzioni e informazioni per amministratori per gestire il client Azure Information Protection tramite PowerShell.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 865a30bb85c1e9e2f8331ae3a85960e005de5b07
ms.lasthandoff: 02/24/2017


---


# <a name="using-powershell-with-the-azure-information-protection-client"></a>Uso di PowerShell con il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Quando si installa il client Azure Information Protection, vengono automaticamente installati alcuni comandi di PowerShell con cui è possibile gestire il client e che possono essere inseriti in script per l'automazione.

I cmdlet vengono installati con il modulo di PowerShell **AzureInformationProtection**, che sostituisce il modulo RMSProtection, installato con lo strumento di protezione RMS. Se quando si installa il client Azure Information Protection è già installato lo strumento RMSProtection, questo viene automaticamente disinstallato.

Il modulo AzureInformationProtection include tutti i cmdlet per Rights Management dello strumento di protezione RMS e due nuovi cmdlet che usano il servizio Azure Information Protection (AIP) per le etichette:

|Cmdlet per le etichette|Esempio di utilizzo|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus)|Per una cartella condivisa, identifica tutti i file con un'etichetta specifica.|
|[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)|Per una cartella condivisa, applica un'etichetta specificata a tutti i file privi di etichetta.|


Questo modulo viene installato in **\Programmi (x86)\Microsoft Azure Information Protection** e aggiunge questa cartella alla variabile di sistema **PSModulePath**. Il file DLL per questo modulo si chiama **AIP.dll**.

Come per il modulo RMSProtection, la versione corrente del modulo AzureInformationProtection impone le limitazioni seguenti:

- È possibile rimuovere la protezione di cartelle personali di Outlook (file PST), ma non è attualmente possibile proteggere in modo nativo questi file o altri file contenitore tramite questo modulo di PowerShell.

- È possibile rimuovere la protezione di messaggi di posta elettronica protetti di Outlook (file RPMSG) quando si trovano in una cartella personale di Outlook (PST), ma non se si trovano esternamente a una cartella personale.

Prima di iniziare a usare i cmdlet, vedere le istruzioni e i prerequisiti aggiuntivi corrispondenti alla distribuzione in uso:

- [Servizio Azure Information Protection e servizio Azure Rights Management](#azure-information-protection-service-and-azure-rights-management-service)

    - Applicabile se si usa la modalità di sola classificazione o di classificazione con protezione con Rights Management: è necessaria una sottoscrizione che include Azure Information Protection, ad esempio Enterprise Mobility + Security.
    - Applicabile se si usa la modalità di sola protezione con il servizio Azure Rights Management: è necessaria una sottoscrizione che include il servizio Azure Rights Management, ad esempio Office 365 E3 e Office 365 E5.

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - Applicabile se si usa la modalità di sola protezione con la versione locale di Azure Rights Management, Active Directory Rights Management Services (AD RMS).


## <a name="azure-information-protection-service-and-azure-rights-management-service"></a>Servizio Azure Information Protection e servizio Azure Rights Management

Leggere questa sezione prima di iniziare a usare i comandi di PowerShell quando l'organizzazione usa Azure Information Protection e il servizio di protezione dei dati Azure Rights Management oppure solo il servizio Azure Rights Management.


### <a name="prerequisites-for-aip-and-azure-rms"></a>Prerequisiti per AIP e Azure RMS

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, è necessario soddisfare alcuni prerequisiti aggiuntivi per il servizio Azure Information Protection e il servizio di protezione dei dati Azure Rights Management:

1. Il servizio Azure Rights Management deve essere attivato.

2. Per rimuovere la protezione dai file per altri utenti tramite il proprio account: la funzionalità per utenti con privilegi avanzati deve essere abilitata per l'organizzazione e l'account deve essere configurato come account con privilegi avanzati per Azure Rights Management.

3. Per proteggere direttamente i file o rimuoverne la protezione senza interazione da parte dell'utente: creare un account di entità servizio, eseguire Set-RMSServerAuthentication e valutare se impostare questa entità servizio come utente con privilegi avanzati per Azure Rights Management.

4. Per le aree al di fuori dell'America del Nord: modificare il Registro di sistema per l'autenticazione al servizio.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prerequisito 1: il servizio Azure Rights Management deve essere attivato

Questo prerequisito è valido se la protezione dei dati viene applicata tramite etichette o connessione diretta al servizio Azure Rights Management. configurato per l'applicazione della protezione dei dati.

Se il tenant Azure Information Protection non è attivato, vedere le istruzioni in [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prerequisito 2: per rimuovere la protezione dai file per altri utenti tramite il proprio account

Gli scenari tipici per la rimozione della protezione dai file per altri utenti includono l'individuazione dei dati o il ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica protezione oppure rimuovendo l'etichetta. Tuttavia, è più probabile che si sceglierà di connettersi direttamente al servizio Azure Rights Management per rimuovere la protezione.

Per poter rimuovere la protezione dai file, è necessario avere autorizzazioni per Rights Management oppure essere un utente con privilegi avanzati. Per l'individuazione dei dati o il ripristino dei dati, viene in genere usata la funzionalità per utenti con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Prerequisito 3: per proteggere i file o rimuoverne la protezione senza interazione da parte dell'utente

Attualmente non è possibile applicare etichette in modo non interattivo, ma è possibile connettersi direttamente al servizio Azure Rights Management in modo non interattivo per proteggere i file o rimuoverne la protezione.

È necessario usare un'entità servizio per connettersi al servizio Azure Rights in modo non interattivo, usando il cmdlet `Set-RMSServerAuthentication`. È necessario eseguire questa operazione per ogni sessione di Windows PowerShell che esegue cmdlet che si connettono direttamente al servizio Azure Rights Management. Prima di eseguire il cmdlet, assicurarsi di aver ottenuto questi tre identificatori:

- BposTenantId

- AppPrincipalId

- Chiave simmetrica

Le sezioni seguenti descrivono come ottenere gli identificatori.

##### <a name="to-get-the-bpostenantid"></a>Per ottenere BposTenantId

Eseguire il cmdlet Get-AadrmConfiguration dal modulo di Windows PowerShell Azure per RMS:

1. Se questo modulo non è ancora installato nel computer, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md).

2. Avviare Windows PowerShell usando l'opzione **Esegui come amministratore**.

3. Usare il cmdlet `Connect-AadrmService` per connettersi al servizio Azure Rights Management:
    
        Connect-AadrmService
    
    Quando viene richiesto, immettere le credenziali di amministratore del tenant Azure Information Protection. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.
    
4. Eseguire `Get-AadrmConfiguration` ed eseguire una copia del valore di BPOSId.
    
    Di seguito è riportato un esempio dell'output di Get-AadrmConfiguration:
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. Disconnettersi dal servizio:
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>Per ottenere l'identificatore AppPrincipalId e la chiave simmetrica

Creare una nuova entità servizio eseguendo il cmdlet `New-MsolServicePrincipal` dal modulo di PowerShell MSOnline per Azure Active Directory oppure `New-AzureADServicePrincipal` dal nuovo modulo di PowerShell per Azure Active Directory versione 2. 

Le istruzioni seguenti sono per New-MsolServicePrincipal del modulo di PowerShell MSOnline per Azure Active Directory:

1. Se questo modulo non è ancora installato nel computer, vedere [Install the Azure AD Module](/powershell/azuread/#install-the-azure-ad-module) (Installare il modulo per Azure AD).

2. Avviare Windows PowerShell usando l'opzione **Esegui come amministratore**.

3. Usare il cmdlet **Connect-MsolService** per connettersi ad Azure AD:
    
        Connect-MsolService
    
    Quando viene richiesto, immettere le credenziali di amministratore del tenant Azure AD. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

4. Eseguire il cmdlet New-MsolServicePrincipal per creare una nuova entità servizio:
    
        New-MsolServicePrincipal
    
    Quando viene richiesto, immettere il nome visualizzato desiderato per l'entità servizio, che permetterà di identificarne lo scopo in seguito come account per la connessione al servizio Azure Rights Management, per poter proteggere i file o rimuoverne la protezione.
    
    Ecco un esempio dell'output di New-MsolServicePrincipal:
    
        Supply values for the following parameters:
        
        DisplayName: AzureRMSProtectionServicePrincipal
        The following symmetric key was created as one was not supplied
        zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=
        
        Display Name: AzureRMSProtectionServicePrincipal
        ServicePrincipalNames: (b5e3f7g1-b5c2-4c96-a594-a0807f65bba4)
        ObjectId: 23720996-593c-4122-bfc7-1abb5a0b5109
        AppPrincialId: b5e3f76a-b5c2-4c96-a594-a0807f65bba4
        TrustedForDelegation: False
        AccountEnabled: True
        Addresses: ()
        KeyType: Symmetric
        KeyId: 8ef61651-ca11-48ea-a350-25834a1ba17c
        StartDate: 3/7/2014 4:43:59 AM
        EndDate: 3/7/2014 4:43:59 AM
        Usage: Verify

5. Da questo output, annotare la chiave simmetrica e il valore di AppPrincialId.

    È particolarmente importante eseguire una copia della chiave simmetrica, perché successivamente non sarà possibile recuperarla completamente. Se si smarrisce questa chiave, sarà necessario creare una nuova entità servizio alla successiva autenticazione al servizio Azure Rights Management.

Da questi esempi e istruzioni sono stati ottenuti i tre identificatori necessari per eseguire Set-RMSServerAuthentication:

- ID tenant: **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Chiave simmetrica: **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId: **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

Il comando di esempio sarà simile al seguente:

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

Come mostrato nel comando precedente, è possibile specificare i valori con un singolo comando oppure digitare semplicemente Set-RMSServerAuthentication e specificare i valori uno per uno quando richiesto. Al termine dell'esecuzione del comando, verrà visualizzato un messaggio che indica che** **RmsServerAuthentication è attivato, ovvero è ora possibile proteggere i file o rimuoverne la protezione tramite l'entità servizio.

Valutare se impostare l'entità servizio come utente con privilegi avanzati: per garantire che l'entità servizio possa sempre rimuovere la protezione dei file per altri utenti, è possibile configurarla come utente con privilegi avanzati. Usare lo stesso cmdlet per Azure RMS, [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md), usato per configurare un account utente standard come utente con privilegi avanzati, ma specificare il parametro **-ServicePrincipalId** con il valore di AppPrincipalId.

Per altre informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

> [!NOTE]
> Per usare il proprio account per l'autenticazione al servizio Azure Rights Management, non è necessario eseguire Set-RMSServerAuthentication prima di proteggere i file o rimuoverne la protezione o di ottenere modelli.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Prerequisito 4: Per le aree al di fuori dell'America del Nord

Per l'autenticazione al di fuori dell'area America del Nord di Azure, è necessario modificare il Registro di sistema come indicato di seguito. Se il tenant Azure Information Protection si trova in America del Nord, ignorare questo passaggio:

1. Eseguire di nuovo il cmdlet Get-AadrmConfiguration e annotare i valori di **CertificationExtranetDistributionPointUrl** e **LicensingExtranetDistributionPointUrl**.

2. In ogni computer in cui si intende eseguire i cmdlet del modulo AzureInformationProtection aprire l'editor del Registro di sistema e passare a: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

3. Se la chiave **ServiceLocation** non è visibile, crearla, in modo che il percorso del Registro di sistema indichi **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation**

4. Per la chiave **ServiceLocation** creare due chiavi, se non esistono, chiamate **EnterpriseCertification** e **EnterprisePublishing**. 
    
    Quando si creano queste chiavi REG_SZ, non modificare il nome in "(predefinito)", ma modificarle in modo da impostare questi dati in Valore:

    - Per **EnterpriseCertification**, incollare il valore di CertificationExtranetDistributionPointUrl.
    
    - Per **EnterprisePublishing**, incollare il valore di LicensingExtranetDistributionPointUrl.

5. Chiudere l'editor del Registro di sistema. Non è necessario riavviare il computer. Tuttavia, se si usa un account di entità servizio invece del proprio account utente, è necessario eseguire il comando Set-RMSServerAuthentication dopo la modifica del Registro di sistema.

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Scenari di esempio per l'uso dei cmdlet per Azure Information Protection e il servizio Azure Rights Management

L'uso di etichette per classificare e proteggere i file è più efficiente, perché richiede solo due cmdlet, che possono essere eseguiti indipendentemente o insieme: [Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus) e [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel). Per altre informazioni ed esempi, usare la guida per questi due cmdlet.

Per proteggere i file o rimuoverne la protezione tramite la connessione diretta al servizio Azure Rights Management, tuttavia, è in genere necessario eseguire una serie di cmdlet, come descritto di seguito.

Innanzitutto, se è necessario eseguire l'autenticazione al servizio Azure Rights Management con un'entità servizio invece che con il proprio account, in una sessione di Powershell digitare:

    Set-RMSServerAuthentication

Quando viene richiesto, immettere i tre identificatori come descritto in [Prerequisito 3: per proteggere i file o rimuoverne la protezione senza interazione da parte dell'utente](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction).

Prima di proteggere i file, è necessario ottenere un elenco dei modelli di Rights Management per identificare quello da usare e l'ID corrispondente. Dall'output è quindi possibile copiare l'ID modello:

    Get-RMSTemplate
    
L'output potrebbe essere simile al seguente:

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Se non è stato eseguito il comando Set-RMSServerAuthentication, l'autenticazione al servizio Azure Rights Management verrà eseguita tramite il proprio account utente. Se si usa un computer aggiunto a un dominio, verranno sempre usate automaticamente le credenziali correnti. Se si usa il computer di un gruppo di lavoro, verrà richiesto di accedere ad Azure e queste credenziali verranno quindi memorizzate nella cache per i comandi successivi. Se in questo scenario successivamente sarà necessario accedere come utente diverso, usare il cmdlet `Clear-RMSAuthentication`.

Una volta identificato l'ID modello, è possibile usarlo con il cmdlet `Protect-RMSFile` per proteggere un singolo file o tutti i file in una cartella. Ad esempio, se si vuole proteggere un solo file e sovrascrivere l'originale, usando il modello "Contoso, Ltd - Confidential":

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

L'output potrebbe essere simile al seguente:

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

Per proteggere tutti i file in una cartella, usare il parametro **-Folder** con una lettera di unità e un percorso oppure un percorso UNC. Ad esempio:

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

L'output potrebbe essere simile al seguente:

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

Quando l'estensione del file non cambia dopo aver applicato la protezione, è sempre possibile usare il cmdlet `Get-RMSFileStatus` successivamente per controllare se il file è protetto. Ad esempio:

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

L'output potrebbe essere simile al seguente:

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

Per rimuovere la protezione di un file, è necessario avere gli stessi diritti di proprietario o di estrazione usati per la protezione del file oppure è necessario eseguire i cmdlet come utente con privilegi avanzati. Usare quindi il cmdlet Unprotect. Ad esempio:

    Unprotect-RMSFile C:\test.docx -InPlace

L'output potrebbe essere simile al seguente:

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx


## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management Services

Leggere questa sezione prima di iniziare a usare i comandi di PowerShell per la protezione o la rimozione della protezione dei file quando l'organizzazione usa solo Active Directory Rights Management Services.


### <a name="prerequisites-for-ad-rms"></a>Prerequisiti per AD RMS

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, l'account deve avere autorizzazioni di lettura ed esecuzione per accedere a ServerCertification.asmx:

1. Accedere a un server AD RMS.

2. Fare clic su **Start**, quindi su **Computer**.

3. In Esplora file passare a %systemdrive%\Initpub\wwwroot\_wmsc\Certification.

4. Fare clic con il pulsante destro del mouse su **ServerCertification.asmx** e quindi scegliere **Proprietà**.

5. Nella finestra di dialogo **Proprietà - ServerCertification.asmx** fare clic sulla scheda **Sicurezza**. 

6. Fare clic sul pulsante **Continua** o sul pulsante **Modifica**. 

7. Nella finestra di dialogo **Autorizzazioni per ServerCertification.asmx** fare clic su **Aggiungi**. 

8. Aggiungere il nome dell'account. Se altri amministratori di AD RMS useranno questi cmdlet per la protezione o la rimozione della protezione dei file, aggiungere anche i loro nomi.

9. Nella colonna **Consenti** assicurarsi che siano selezionate le caselle di controllo **Lettura/esecuzione** e **Lettura**.

10. Fare clic su **OK** due volte.

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Scenari di esempio per l'uso di cmdlet per Active Directory Rights Management Services

Uno scenario tipico per questi cmdlet consiste nella protezione di tutti i file in una cartella tramite un modello di criteri di diritti oppure nella rimozione della protezione di un file. 

Innanzitutto, nel caso di più distribuzioni di AD RMS, saranno necessari i nomi dei server AD RMS e a questo scopo sarà possibile usare il cmdlet Get-RMSServer per visualizzare un elenco dei server disponibili:

    Get-RMSServer

L'output potrebbe essere simile al seguente:

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

Prima di proteggere i file, è necessario ottenere un elenco dei modelli di RMS per identificare quello da usare e l'ID corrispondente. Solo nel caso di più distribuzioni di AD RMS sarà necessario specificare anche il server RMS. 

Dall'output è quindi possibile copiare l'ID modello:

    Get-RMSTemplate -RMSServer RmsContoso

L'output potrebbe essere simile al seguente:

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Una volta identificato l'ID modello, è possibile usarlo con il cmdlet Protect-RMSFile per proteggere un singolo file o tutti i file in una cartella. Ad esempio, se si vuole proteggere solo un singolo file e sostituire l'originale, usando il modello "Contoso, Ltd - Confidential":

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

L'output potrebbe essere simile al seguente:

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

Per proteggere tutti i file in una cartella, usare il parametro -Folder con una lettera di unità e un percorso oppure un percorso UNC. Ad esempio:

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

L'output potrebbe essere simile al seguente:

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

Quando l'estensione del file non cambia dopo aver applicato la protezione con RMS, è sempre possibile usare il cmdlet Get-RMSFileStatus successivamente per controllare se il file è protetto. Ad esempio: 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

L'output potrebbe essere simile al seguente:

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

Per rimuovere la protezione di un file, è necessario avere gli stessi diritti di proprietario o di estrazione usati per la protezione del file oppure essere un utente con privilegi avanzati per AD RMS. Usare quindi il cmdlet Unprotect. Ad esempio:

    Unprotect-RMSFile C:\test.docx -InPlace

L'output potrebbe essere simile al seguente:

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx


## <a name="next-steps"></a>Passaggi successivi
Per informazioni sui cmdlet durante una sessione di PowerShell, usare il cmdlet <cmdlet name>, dove <cmdlet name> è il nome del cmdlet che si vuole cercare. Ad esempio: 

    Get-Help Get-RMSTemplate

Per altre informazioni necessarie per supportare il client Azure Information Protection, vedere gli argomenti seguenti:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

