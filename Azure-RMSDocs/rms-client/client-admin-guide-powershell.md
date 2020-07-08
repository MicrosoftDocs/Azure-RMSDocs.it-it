---
title: Usare PowerShell con il client Azure Information Protection
description: Istruzioni e informazioni per amministratori per gestire il client Azure Information Protection tramite PowerShell.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/31/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.subservice: v1client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 32880671c46efb9cb82f13235f98ac42566b65fc
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048902"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-client"></a>Guida dell'amministratore: Uso di PowerShell con il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Quando si installa il client di Azure Information Protection, vengono installati automaticamente i comandi di PowerShell. Ciò consente di gestire il client eseguendo i comandi che è possibile inserire negli script per l'automazione.

I cmdlet vengono installati con il modulo **AzureInformationProtection** di PowerShell. Questo modulo include tutti i cmdlet per Rights Management dello strumento di protezione RMS (non più supportato). Sono inoltre disponibili cmdlet che usano Azure Information Protection per l'assegnazione di etichette. Ad esempio:

|Cmdlet per le etichette|Esempio di utilizzo|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Per una cartella condivisa, identifica tutti i file con un'etichetta specifica.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Per una cartella condivisa, esaminare il contenuto dei file e quindi etichettare automaticamente i file senza etichetta, in base alle condizioni specificate.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Per una cartella condivisa, applica un'etichetta specificata a tutti i file privi di etichetta.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Assegna etichette ai file in modo non interattivo, ad esempio tramite uno script che viene eseguito in base a una pianificazione.|

> [!TIP]
> Per usare cmdlet con percorsi di lunghezza superiore a 260 caratteri, usare l'[impostazione di Criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) seguente disponibile a partire da Windows 10 versione 1607:<br /> Criteri del computer **locale**  >  **Configurazione computer**  >  **Modelli amministrativi**  >  **Tutte le impostazioni**  >  **Abilita percorsi lunghi Win32** 
> 
> Per Windows Server 2016 è possibile usare la stessa impostazione di Criteri di gruppo quando si installano i modelli amministrativi più recenti (con estensione admx) per Windows 10.
>
> Per altre informazioni, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) della documentazione per sviluppatori di Windows 10.

Lo [scanner Azure Information Protection](../deploy-aip-scanner.md) usa i cmdlet dal modulo AzureInformationProtection per installare e configurare un servizio in Windows Server. Lo scanner consente quindi di individuare, classificare e proteggere i file negli archivi dati.

Per un elenco di tutti i cmdlet e le informazioni della guida corrispondenti, vedere [AzureInformationProtection Module](/powershell/module/azureinformationprotection) (Modulo AzureInformationProtection). All'interno di una sessione di PowerShell digitare `Get-Help <cmdlet name> -online` per visualizzare le informazioni della guida più recenti.  

Questo modulo viene installato in **\Programmi (x86)\Microsoft Azure Information Protection** e aggiunge questa cartella alla variabile di sistema **PSModulePath**. Il file DLL per questo modulo si chiama **AIP.dll**.

Attualmente, se si installa il modulo con un account utente e si eseguono i cmdlet nello stesso computer come un altro utente, è prima necessario eseguire il comando `Import-Module AzureInformationProtection`. In questo scenario, il modulo non viene caricato automaticamente alla prima esecuzione di un cmdlet.

La versione corrente del modulo AzureInformationProtection impone le limitazioni seguenti:

- È possibile rimuovere la protezione di cartelle personali di Outlook (file PST), ma non è attualmente possibile proteggere in modo nativo questi file o altri file contenitore tramite questo modulo di PowerShell.

- È possibile rimuovere la protezione dei messaggi di posta elettronica protetti di Outlook (file con estensione rpmsg) solo se i messaggi si trovano in una cartella personale di Outlook (con estensione pst).

Prima di iniziare a usare i cmdlet, vedere le istruzioni e i prerequisiti aggiuntivi corrispondenti alla distribuzione in uso:

- [Servizio Azure Information Protection e servizio Azure Rights Management](#azure-information-protection-and-azure-rights-management-service)

    - Applicabile se si usa la modalità di sola classificazione o di classificazione con protezione con Rights Management: è necessaria una sottoscrizione che include Azure Information Protection, ad esempio Enterprise Mobility + Security.
    - Applicabile se si usa la modalità di sola protezione con il servizio Azure Rights Management: è necessaria una sottoscrizione che include il servizio Azure Rights Management, ad esempio Office 365 E3 e Office 365 E5.

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - Applicabile se si usa la modalità di sola protezione con la versione locale di Azure Rights Management, Active Directory Rights Management Services (AD RMS).


## <a name="azure-information-protection-and-azure-rights-management-service"></a>Servizio Azure Information Protection e servizio Azure Rights Management

Se l'organizzazione usa Azure Information Protection per classificazione e protezione oppure solo il servizio Azure Rights Management, leggere questa sezione prima di iniziare a usare i comandi di PowerShell.


### <a name="prerequisites"></a>Prerequisiti

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, è necessario soddisfare alcuni prerequisiti aggiuntivi per l'etichettatura Azure Information Protection e per il servizio di protezione dati Azure Rights Management:

1. Il servizio Azure Rights Management deve essere attivato.

2. Per rimuovere la protezione dai file per altri utenti tramite il proprio account: 

    - La funzionalità relativa agli utenti con privilegi avanzati deve essere abilitata per l'organizzazione e l'account deve essere configurato come account con privilegi avanzati per Azure Rights Management.

3. Per proteggere i file o rimuoverne la protezione direttamente, senza alcuna interazione da parte dell'utente: 

    - Creare un account di entità servizio, eseguire Set-RMSServerAuthentication e valutare se impostare questa entità servizio come utente con privilegi avanzati per Azure Rights Management.

4. Per le aree al di fuori dell'America del Nord: 

    - Modificare il Registro di sistema per l'individuazione del servizio.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prerequisito 1: il servizio Azure Rights Management deve essere attivato

Questo prerequisito è valido se la protezione dei dati viene applicata tramite etichette o connessione diretta al servizio Azure Rights Management.

Se il tenant di Azure Information Protection non è attivato, vedere le istruzioni per l' [attivazione del servizio di protezione da Azure Information Protection](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prerequisito 2: per rimuovere la protezione dai file per altri utenti tramite il proprio account

Gli scenari tipici per la rimozione della protezione dai file per altri utenti includono l'individuazione dei dati o il ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica protezione oppure rimuovendo l'etichetta. Tuttavia, è più probabile che si sceglierà di connettersi direttamente al servizio Azure Rights Management per rimuovere la protezione.

Per poter rimuovere la protezione dai file, è necessario avere diritti di utilizzo per Rights Management oppure un account utente con privilegi avanzati. Per l'individuazione dei dati o il ripristino dei dati, viene in genere usata la funzionalità per utenti con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Prerequisito 3: per proteggere i file o rimuoverne la protezione senza interazione da parte dell'utente

È possibile connettersi direttamente al servizio Azure Rights Management in modo non interattivo per proteggere i file o rimuoverne la protezione.

È necessario usare l'account di un'entità servizio per connettersi al servizio Azure Rights Management in modo non interattivo, usando il cmdlet `Set-RMSServerAuthentication`. È necessario eseguire questa operazione per ogni sessione di Windows PowerShell che esegue cmdlet che si connettono direttamente al servizio Azure Rights Management. Prima di eseguire il cmdlet, assicurarsi di aver ottenuto questi tre identificatori:

- BposTenantId

- AppPrincipalId

- Chiave simmetrica

È possibile usare i seguenti comandi di PowerShell e le istruzioni commentate per ottenere automaticamente i valori per gli identificatori ed eseguire il cmdlet Set-RMSServerAuthentication. In alternativa, è possibile ottenere e specificare i valori manualmente.

Per ottenere i valori ed eseguire Set-RMSServerAuthentication automaticamente:

```ps
# Make sure that you have the AIPService and MSOnline modules installed

$ServicePrincipalName="<new service principal name>"
Connect-AipService
$bposTenantID=(Get-AipServiceConfiguration).BPOSId
Disconnect-AipService
Connect-MsolService
New-MsolServicePrincipal -DisplayName $ServicePrincipalName

# Copy the value of the generated symmetric key

$symmetricKey="<value from the display of the New-MsolServicePrincipal command>"
$appPrincipalID=(Get-MsolServicePrincipal | Where { $_.DisplayName -eq $ServicePrincipalName }).AppPrincipalId
Set-RMSServerAuthentication -Key $symmetricKey -AppPrincipalId $appPrincipalID -BposTenantId $bposTenantID
```

Nelle sezioni successive viene illustrato come ottenere e specificare manualmente questi valori, con altre informazioni su ciascuno di essi.

##### <a name="to-get-the-bpostenantid"></a>Per ottenere BposTenantId

Eseguire il cmdlet Get-AipServiceConfiguration dal modulo Azure RMS Windows PowerShell:

1. Se questo modulo non è già installato nel computer, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

2. Avviare Windows PowerShell con l'opzione **Esegui come amministratore** .

3. Usare il cmdlet `Connect-AipService` per connettersi al servizio Azure Rights Management:
   ```ps 
    Connect-AipService
    ```

    Quando richiesto, immettere le credenziali di amministratore del tenant di Azure Information Protection. In genere si usa un account che sia un amministratore globale per Azure Active Directory o Office 365.
    
4. Eseguire `Get-AipServiceConfiguration` ed eseguire una copia del valore di BPOSId.
    
    Esempio di output di Get-AipServiceConfiguration:

    ```ps    
    BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
    RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
    LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
    LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
    CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
    CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
    ```

5. Disconnettersi dal servizio:

    ```
    Disconnect-AipService
    ```

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>Per ottenere l'identificatore AppPrincipalId e la chiave simmetrica

Creare una nuova entità servizio eseguendo il cmdlet `New-MsolServicePrincipal` dal modulo di PowerShell MSOnline per Azure Active Directory e seguire le istruzioni riportate di seguito. 

> [!IMPORTANT]
> Per creare l'entità servizio non usare il cmdlet PowerShell di Azure AD più recente, New-AzureADServicePrincipal. Il servizio Azure Rights Management non supporta New-AzureADServicePrincipal. 

1. Se il modulo MSOnline non è ancora installato nel computer in uso, eseguire `Install-Module MSOnline`.

2. Avviare Windows PowerShell con l'opzione **Esegui come amministratore** .

3. Usare il cmdlet **Connect-MsolService** per connettersi ad Azure AD:

    ```ps
    Connect-MsolService
    ```

    Quando viene richiesto, immettere le credenziali di amministratore del tenant Azure AD. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

4. Eseguire il cmdlet New-MsolServicePrincipal per creare una nuova entità servizio:

    ```ps
    New-MsolServicePrincipal
    ```

    Quando richiesto, immettere il nome visualizzato scelto per l'entità servizio, che consentirà di identificarne lo scopo in seguito come account per la connessione al servizio Azure Rights Management, per proteggere i file o rimuoverne la protezione.

    Ecco un esempio dell'output di New-MsolServicePrincipal:

    ```ps
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
    ```

5. Da questo output, annotare la chiave simmetrica e il valore di AppPrincialId.

    È importante effettuare subito una copia della chiave simmetrica. Non sarà possibile recuperare la chiave in un secondo momento; pertanto, se non la si conosce, al momento dell'autenticazione al servizio di Azure Rights Management sarà necessario creare una nuova entità servizio.

Da questi esempi e istruzioni sono stati ottenuti i tre identificatori necessari per eseguire Set-RMSServerAuthentication:

- ID tenant: **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Chiave simmetrica: **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId: **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

Il comando di esempio sarà simile al seguente:

```ps
Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42
```

Come illustrato nel comando precedente, è possibile specificare i valori con un singolo comando, usando uno script da eseguire in modo non interattivo. A scopo di test è tuttavia possibile digitare solo Set-RMSServerAuthentication e indicare i valori uno alla volta quando vengono richiesti. Al termine dell'esecuzione del comando il client funziona in "modalità server", adatta per l'uso non interattivo, ad esempio per gli script e l'infrastruttura di classificazione file per Windows Server.

Valutare se impostare l'account dell'entità servizio come utente con privilegi avanzati: per garantire che l'account dell'entità servizio possa sempre rimuovere la protezione dei file per altri utenti, è possibile configurarlo come utente con privilegi avanzati. Nello stesso modo in cui si configura un account utente standard come utente con privilegi avanzati, si usa lo stesso cmdlet Azure RMS, [Add-AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser), ma si specifica il parametro **ServicePrincipalId** con il valore AppPrincipalId.

Per ulteriori informazioni sugli utenti con privilegi avanzati, vedere [configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](../configure-super-users.md).

> [!NOTE]
> Per usare il proprio account per l'autenticazione al servizio Azure Rights Management, non è necessario eseguire Set-RMSServerAuthentication prima di proteggere i file o rimuoverne la protezione o di ottenere modelli.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Prerequisito 4: Per le aree al di fuori dell'America del Nord

Quando si usa un account dell'entità di sicurezza del servizio per proteggere i file e scaricare i modelli al di fuori dell'area America del Nord di Azure, è necessario modificare il Registro di sistema: 

1. Eseguire di nuovo il cmdlet Get-AipServiceConfiguration e prendere nota dei valori di **CertificationExtranetDistributionPointUrl** e **LicensingExtranetDistributionPointUrl**.

2. In ogni computer in cui si eseguiranno i cmdlet di AzureInformationProtection aprire l'editor del Registro di sistema.

3. Andare al percorso seguente: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation`. 

    Se la chiave **MSIPC** o **ServiceLocation** non viene visualizzata, crearla.

4. Per la chiave **ServiceLocation** creare due chiavi, se non esistono, chiamate **EnterpriseCertification** e **EnterprisePublishing**. 

    Per il valore stringa che viene creato automaticamente per queste chiavi non modificare il nome del "(predefinito)", ma modificare la stringa per impostare i dati di Valore:

   - Per **EnterpriseCertification**, incollare il valore di CertificationExtranetDistributionPointUrl.

   - Per **EnterprisePublishing**, incollare il valore di LicensingExtranetDistributionPointUrl.

     Ad esempio, la voce del Registro di sistema per EnterpriseCertification dovrebbe essere simile alla seguente:

     ![Modifica del Registro di sistema per il modulo PowerShell di Azure Information Protection per le aree al di fuori dell'America del Nord](../media/registry-example-rmsprotection.png)

5. Chiudere l'editor del Registro di sistema. Non è necessario riavviare il computer. Tuttavia, se si usa un account di entità servizio invece del proprio account utente, è necessario eseguire il comando Set-RMSServerAuthentication dopo la modifica del Registro di sistema.

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Scenari di esempio per l'uso dei cmdlet per Azure Information Protection e il servizio Azure Rights Management

È più efficiente usare le etichette per classificare e proteggere i file, perché sono necessari solo due cmdlet, che possono essere eseguiti da soli o insieme: [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) e [set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel). Per altre informazioni ed esempi, usare la guida per questi due cmdlet.

Per proteggere i file o rimuoverne la protezione tramite la connessione diretta al servizio Azure Rights Management, tuttavia, è in genere necessario eseguire una serie di cmdlet, come descritto di seguito.

Innanzitutto, se è necessario eseguire l'autenticazione al servizio Azure Rights Management con l'account di un'entità servizio invece che con il proprio account, in una sessione di PowerShell digitare:

```ps
Set-RMSServerAuthentication
```

Quando viene richiesto, immettere i tre identificatori come descritto in [Prerequisito 3: per proteggere i file o rimuoverne la protezione senza interazione da parte dell'utente](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction).

Per proteggere i file, è prima necessario scaricare i modelli di Rights Management sul computer per identificare quello da usare e l'ID corrispondente. Dall'output è quindi possibile copiare l'ID modello:

```ps
Get-RMSTemplate
```
L'output potrebbe essere simile al seguente:

```ps
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
```

Se non è stato eseguito il comando Set-RMSServerAuthentication, l'autenticazione al servizio Azure Rights Management viene eseguita tramite l'account utente personale. Se si usa un computer aggiunto a un dominio, vengono sempre usate automaticamente le credenziali correnti. Se si usa il computer di un gruppo di lavoro, viene richiesto di accedere ad Azure. Le credenziali specificate per l'accesso vengono quindi memorizzate nella cache per i comandi successivi. Se in questo scenario successivamente sarà necessario accedere come utente diverso, usare il cmdlet `Clear-RMSAuthentication`.

Una volta identificato l'ID modello, è possibile usarlo con il cmdlet `Protect-RMSFile` per proteggere un singolo file o tutti i file in una cartella. Ad esempio, se si vuole proteggere un solo file e sovrascrivere l'originale, usando il modello "Contoso, Ltd - Confidential":

```ps
Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

L'output potrebbe essere simile al seguente:

```ps
InputFile             EncryptedFile
---------             -------------
C:\Test.docx          C:\Test.docx
```

Per proteggere tutti i file in una cartella, usare il parametro **-Folder** con una lettera di unità e un percorso oppure un percorso UNC. Ad esempio:

```ps
Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

L'output potrebbe essere simile al seguente:

```ps
InputFile                          EncryptedFile
---------                          -------------
\Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
\Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
\Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
\Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx
```

Quando l'estensione del file non cambia dopo aver applicato la protezione, è sempre possibile usare il cmdlet `Get-RMSFileStatus` successivamente per controllare se il file è protetto. Ad esempio:

```ps
Get-RMSFileStatus -File \Server1\Documents\Test1.docx
```

L'output potrebbe essere simile al seguente:

```ps
FileName                              Status
--------                              ------
\Server1\Documents\Test1.docx         Protected
```

Per rimuovere la protezione di un file, è necessario avere gli stessi diritti di proprietario o di estrazione usati per la protezione del file oppure essere un utente con privilegi avanzati per i cmdlet. Usare quindi il cmdlet Unprotect. Ad esempio:

```ps
Unprotect-RMSFile C:\test.docx -InPlace
```

L'output potrebbe essere simile al seguente:

```ps
InputFile                             DecryptedFile
---------                             -------------
C:\Test.docx                          C:\Test.docx
```

Si tenga presente che, se i modelli di Rights Management sono stati modificati, sarà necessario scaricarli di nuovo con `Get-RMSTemplate -force`. 

## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management Services

Leggere questa sezione prima di iniziare a usare i comandi di PowerShell per la protezione o la rimozione della protezione dei file quando l'organizzazione usa solo Active Directory Rights Management Services.


### <a name="prerequisites"></a>Prerequisiti

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, l'account usato per proteggere o rimuovere la protezione dei file deve avere autorizzazioni di lettura ed esecuzione per accedere a ServerCertification.asmx:

1. Accedere a un server AD RMS.

2. Fare clic su **Start**, quindi su **Computer**.

3. In Esplora file passare a %systemdrive%\Initpub\wwwroot\_wmsc\Certification.

4. Fare clic con il pulsante destro del mouse su **ServerCertification.asmx** e quindi scegliere **Proprietà**.

5. Nella finestra di dialogo **Proprietà - ServerCertification.asmx** fare clic sulla scheda **Sicurezza**. 

6. Fare clic sul pulsante **Continua** o sul pulsante **Modifica**. 

7. Nella finestra di dialogo **Autorizzazioni per ServerCertification.asmx** fare clic su **Aggiungi**. 

8. Aggiungere il nome dell'account. Se altri amministratori di AD RMS o account del servizio useranno questi cmdlet per la protezione o la rimozione della protezione dei file, aggiungere anche tali account. 

    Per proteggere o rimuovere la protezione dei file in modo non interattivo, aggiungere gli account computer rilevanti. Ad esempio, aggiungere l'account computer del computer Windows Server che è configurato per Infrastruttura di classificazione file e che userà uno script di PowerShell per proteggere i file.

9. Nella colonna **Consenti** assicurarsi che siano selezionate le caselle di controllo **Lettura/esecuzione** e **Lettura**.

10. Fare clic su **OK** due volte.

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Scenari di esempio per l'uso di cmdlet per Active Directory Rights Management Services

Uno scenario tipico per questi cmdlet consiste nella protezione di tutti i file in una cartella tramite un modello di criteri di diritti oppure nella rimozione della protezione di un file. 

Nel caso di più distribuzioni di AD RMS, sono prima necessari i nomi dei server AD RMS. A questo scopo è possibile usare il cmdlet Get-RMSServer per visualizzare un elenco dei server disponibili:

```ps
Get-RMSServer
```
L'output potrebbe essere simile al seguente:

```ps
Number of RMS Servers that can provide templates: 2 
ConnectionInfo             DisplayName          AllowFromScratch
--------------             -------------        ----------------
Microsoft.InformationAnd…  RmsContoso                       True
Microsoft.InformationAnd…  RmsFabrikam                      True
```

Prima di proteggere i file, è necessario ottenere un elenco dei modelli di RMS per identificare quello da usare e l'ID corrispondente. Solo nel caso di più distribuzioni di AD RMS è necessario specificare anche il server RMS. 

Dall'output è quindi possibile copiare l'ID modello:

```ps
Get-RMSTemplate -RMSServer RmsContoso
```

L'output potrebbe essere simile al seguente:

```ps
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
```

Una volta identificato l'ID modello, è possibile usarlo con il cmdlet Protect-RMSFile per proteggere un singolo file o tutti i file in una cartella. Ad esempio, se si vuole proteggere solo un singolo file e sostituire l'originale, usando il modello "Contoso, Ltd - Confidential":

```ps
Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

L'output potrebbe essere simile al seguente:

```ps
InputFile             EncryptedFile
---------             -------------
C:\Test.docx          C:\Test.docx   
```

Per proteggere tutti i file in una cartella, usare il parametro -Folder con una lettera di unità e un percorso oppure un percorso UNC. Ad esempio:

```ps
Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

L'output potrebbe essere simile al seguente:

```ps
InputFile                          EncryptedFile
---------                          -------------
\\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
\\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
\\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
\\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   
```

Quando l'estensione del file non cambia dopo aver applicato la protezione, è sempre possibile usare il cmdlet Get-RMSFileStatus successivamente per controllare se il file è protetto. Ad esempio: 

```ps
Get-RMSFileStatus -File \\Server1\Documents\Test1.docx
```

L'output potrebbe essere simile al seguente:

```ps
FileName                              Status
--------                              ------
\\Server1\Documents\Test1.docx        Protected
```

Per rimuovere la protezione di un file, è necessario avere gli stessi diritti di utilizzo di proprietario o di estrazione usati per la protezione del file oppure essere un utente con privilegi avanzati per AD RMS. Usare quindi il cmdlet Unprotect. Ad esempio:

```ps
Unprotect-RMSFile C:\test.docx -InPlace
```

L'output potrebbe essere simile al seguente:

```ps
InputFile                             DecryptedFile
---------                             -------------
C:\Test.docx                          C:\Test.docx
```

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection

È possibile eseguire i cmdlet per l'assegnazione delle etichette in modo non interattivo tramite il cmdlet **Set-AIPAuthentication**. È necessario un intervento non interattivo anche per lo scanner di Azure Information Protection.

Per impostazione predefinita, quando si eseguono i cmdlet per l'assegnazione di etichette, i comandi vengono eseguiti nel contesto utente personale in una sessione interattiva di PowerShell. Per eseguirli senza interventi da parte dell'utente, creare un nuovo account utente di Azure AD per questo scopo. Nel contesto di tale utente, quindi, eseguire il cmdlet Set-AIPAuthentication per impostare e archiviare le credenziali usando un token di accesso da Azure AD. Questo account utente viene quindi autenticato e avviato per il servizio Azure Rights Management. L'account scarica i criteri di Azure Information Protection ed eventuali modelli di Rights Management usati dalle etichette.

> [!NOTE]
> Se si usano [criteri con ambito](../configure-policy-scope.md) tenere presente che potrebbe essere necessario aggiungere questo account ai criteri con ambito.

La prima volta che si esegue questo cmdlet viene richiesto di accedere ad Azure Information Protection. Specificare il nome e la password dell'account utente creato per l'esecuzione senza intervento dell'utente. Questo account può quindi eseguire i cmdlet di assegnazione di etichette in modo non interattivo fino alla scadenza del token di autenticazione. 

Per eseguire il primo accesso interattivo, l'account utente deve disporre del diritto di **accesso locale**. Questo diritto è standard per gli account utente, ma i criteri aziendali potrebbero non consentire questa configurazione per gli account del servizio. In questo caso è possibile eseguire Set-AIPAuthentication con il parametro *Token* per completare l'autenticazione senza che venga richiesto di eseguire l'accesso. È possibile eseguire questo comando come attività pianificata e concedere all'account il diritto di livello inferiore **Accesso come processo batch**. Per altre informazioni, vedere le sezioni seguenti. 

Quando il token scade, eseguire nuovamente il cmdlet per acquisire un nuovo token.

Se si esegue questo cmdlet senza parametri, l'account acquisisce un token di accesso valido per 90 giorni o fino alla scadenza della password.  

Per determinare la scadenza del token di accesso, eseguire questo cmdlet con parametri. Il cmdlet consente di configurare il token di accesso per un anno, due anni o senza alcuna scadenza. Per questa configurazione sono necessarie due applicazioni registrate in Azure Active Directory: **un'app Web o un'applicazione API** e un'**applicazione nativa**. I parametri del cmdlet usano valori provenienti da queste applicazioni.

Dopo aver eseguito il cmdlet, è possibile eseguire i cmdlet di assegnazione di etichette nel contesto dell'account utente creato.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Per creare e configurare le applicazioni di Azure AD per Set-AIPAuthentication

1. In una nuova finestra del browser accedere al [Portale di Azure](https://portal.azure.com/).

2. Per il tenant Azure ad usato con Azure Information Protection, passare a **Azure Active Directory**  >  **Gestisci**  >  **registrazioni app**. 

3. Selezionare **+ nuova registrazione**per creare l'applicazione/API dell'app Web. Nel riquadro **registra un'applicazione** specificare i valori seguenti e quindi fare clic su **registra**:

   - **Nome**:`AIPOnBehalfOf`
        
        Se preferibile, specificare un nome diverso. Deve essere univoco per ogni tenant.
    
    - **Tipi di account supportati**: **solo account in questa directory organizzativa**
    
    - **URI di reindirizzamento (facoltativo)**: **Web** e`http://localhost`

4. Nel riquadro **AIPOnBehalfOf** , copiare il valore per l' **ID applicazione (client)**. Il valore è simile all'esempio seguente: `57c3c1c3-abf9-404e-8b2b-4652836c8c66` . Questo valore viene usato per il parametro *webappid* quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento successivo.

5. Sempre nel riquadro **AIPOnBehalfOf** scegliere **autenticazione**dal menu **Gestisci** .

6. Nel riquadro **AIPOnBehalfOf-Authentication** , nella sezione **Impostazioni avanzate** , selezionare la casella di controllo **token ID** , quindi selezionare **Salva**.

7. Sempre nel riquadro **AIPOnBehalfOf-Authentication** scegliere **certificati & segreti**dal menu **Gestisci** .

8. Nella sezione **segreti client** del riquadro **AIPOnBehalfOf-Certificates & Secrets** selezionare **+ New client Secret**. 

9. Per **Aggiungi un segreto client**, specificare quanto segue e quindi selezionare **Aggiungi**:
    
    - **Descrizione**:`Azure Information Protection client`
    - **Scadenza**: specificare la scelta della durata (1 anno, 2 anni o nessuna scadenza)

9. Tornare al riquadro **AIPOnBehalfOf-certificates & Secrets** , nella sezione **client Secrets** , copiare la stringa per il **valore**. Questa stringa ha un aspetto simile all'esempio seguente: `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn` . Per assicurarsi di copiare tutti i caratteri, selezionare l'icona da **copiare negli Appunti**. 
    
    È importante salvare la stringa, perché non verrà più visualizzata e non potrà essere recuperata. Come per le informazioni riservate utilizzate, archiviare il valore salvato in modo sicuro e limitarne l'accesso.

10. Sempre nel riquadro **AIPOnBehalfOf-certificates & Secrets** selezionare **expose an API**dal menu **Gestisci** .

11. Nel riquadro **AIPOnBehalfOf-esporre un'API** selezionare **imposta** per l'opzione **URI ID applicazione** e nel valore **URI ID applicazione** , modificare **API** in **http**. Questa stringa ha un aspetto simile all'esempio seguente: `http://d244e75e-870b-4491-b70d-65534953099e` . 
    
    Selezionare **Salva**.

12. Tornare al riquadro **AIPOnBehalfOf-esporre un'API** , selezionare **+ Aggiungi un ambito**.

13. Nel riquadro **Aggiungi ambito** , specificare quanto segue, usando le stringhe suggerite come esempi, quindi selezionare **Aggiungi ambito**:
    - **Nome ambito**: `user-impersonation`
    - **Chi può acconsentire?**: **amministratori e utenti**
    - **Nome visualizzato per il consenso amministratore**: `Access Azure Information Protection scanner`
    - **Descrizione del consenso amministratore**: `Allow the application to access the scanner for the signed-in user`
    - **Nome visualizzato del consenso dell'utente**:`Access Azure Information Protection scanner`
    - **Descrizione del consenso dell'utente**:`Allow the application to access the scanner for the signed-in user`
    - **Stato**: **abilitato** (impostazione predefinita)


14. Tornare al riquadro **AIPOnBehalfOf-esporre un'API** , chiudere il riquadro.

15. Selezionare **Autorizzazioni API**.

16. Nel riquadro **AIPOnBehalfOf**  |  **autorizzazioni API** AIPOnBehalfOf selezionare **+ Aggiungi un'autorizzazione**.

17. Scegliere **gestione di Azure right**, selezionare **autorizzazioni delegate** e quindi selezionare **Crea e accedi a contenuto protetto per gli utenti**.

18. Fare clic su **Aggiungi un'autorizzazione**.

19. Tornare al riquadro **autorizzazioni API** , nella sezione **consenso della concessione** , selezionare Concedi il **consenso dell'amministratore <your tenant name> per** e selezionare **Sì** per la richiesta di conferma.

20. Nel riquadro **registrazioni app** selezionare **+ registrazione nuova applicazione** per creare ora l'applicazione nativa.

21. Nel riquadro **registra un'applicazione** specificare le impostazioni seguenti e quindi selezionare **registra**:
    - **Nome**:`AIPClient`
    - **Tipi di account supportati**: **solo account in questa directory organizzativa**
    - **URI di reindirizzamento (facoltativo)**: **client pubblico (mobile & desktop)** e`http://localhost`

22. Nel riquadro **AIPClient** , copiare il valore dell' **ID applicazione (client)**. Il valore è simile all'esempio seguente: `8ef1c873-9869-4bb1-9c11-8313f9d7f76f` . 
    
    Questo valore viene usato per il parametro NativeAppId quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento successivo.

23. Sempre nel riquadro **AIPClient** scegliere **autenticazione**dal menu **Gestisci** .

24. Nel riquadro **AIPClient-Authentication** scegliere **autorizzazioni API**dal menu **Gestisci** .

25. Nel riquadro **AIPClient-autorizzazioni** selezionare **+ Aggiungi un'autorizzazione**.

26. Nel riquadro **autorizzazioni API richiesta** selezionare **API personali**.

27. Nella sezione **selezionare un'API** selezionare **APIOnBehalfOf**, quindi selezionare la casella di controllo per la **rappresentazione utente**come autorizzazione. Selezionare **Aggiungi autorizzazioni**. 

28. Tornare al riquadro **autorizzazioni API** , nella sezione **consenso della concessione** , selezionare Concedi il **consenso dell'amministratore \<*your tenant name*> per** e selezionare **Sì** per la richiesta di conferma.

A questo punto è stata completata la configurazione delle due app e sono disponibili i valori necessari per eseguire [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con i parametri *webappid*, *WebAppKey* e *NativeAppId*. Dagli esempi seguenti:

```ps
Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"
```

Eseguire questo comando nel contesto dell'account per l'assegnazione di etichette e la protezione di documenti in modalità non interattiva. Un esempio è un account utente per gli script di PowerShell o l'account del servizio per eseguire lo scanner di Azure Information Protection.  

La prima volta che si esegue questo comando viene richiesto di eseguire l'accesso, creando e archiviando in modo sicuro il token di accesso per l'account in %localappdata%\Microsoft\MSIP. Dopo questo accesso iniziale è possibile assegnare etichette e proteggere i file in modalità non interattiva nel computer. Tuttavia, se si usa un account del servizio per l'assegnazione di etichette e la protezione di file che non è in grado di accedere in modo interattivo, seguire le istruzioni nella sezione seguente per consentire all'account del servizio di eseguire l'autenticazione tramite un token.

### <a name="specify-and-use-the-token-parameter-for-set-aipauthentication"></a>Specificare e usare il parametro Token per Set-AIPAuthentication

Per non eseguire l'accesso interattivo iniziale per un account che assegna etichette e protegge i file, seguire i passaggi e le istruzioni seguenti. In genere, questi passaggi aggiuntivi sono necessari solo se a questo account non è possibile concedere il diritto di **accesso locale**, ma è stato concesso il diritto **Accesso come processo batch**. Ad esempio, ciò potrebbe verificarsi con l'account del servizio personale che esegue lo scanner di Azure Information Protection.

Procedure generali:

1. Creare uno script di PowerShell nel computer locale.

2. Eseguire Set-AIPAuthentication per ottenere un token di accesso e copiarlo negli Appunti.

3. Modificare lo script di PowerShell in modo da includere il token.

4. Creare un'attività che esegua lo script di PowerShell nel contesto dell'account del servizio per l'assegnazione di etichette e la protezione di file.

5. Confermare che il token è stato salvato per l'account del servizio ed eliminare lo script di PowerShell.

#### <a name="step-1-create-a-powershell-script-on-your-local-computer"></a>Passaggio 1: Creare uno script di PowerShell nel computer locale

1. Nel computer in uso creare un nuovo script di PowerShell denominato Aipauthentication.ps1.

2. Copiare e incollare il comando seguente nello script:

    ```ps
    Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application> -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application > -Token <token value>
    ```

3. Seguendo le istruzioni nella sezione precedente modificare questo comando specificando i valori personalizzati per i parametri **WebAppId**, **WebAppkey** e **NativeAppId**. In questo momento non è disponibile il valore per il parametro **Token** che si specificherà in seguito. 

    Ad esempio: 

    ```ps
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f -Token <token value>
    ```

#### <a name="step-2-run-set-aipauthentication-to-get-an-access-token-and-copy-it-to-the-clipboard"></a>Passaggio 2: Eseguire Set-AIPAuthentication per ottenere un token di accesso e copiarlo negli Appunti

1. Aprire una sessione di Windows PowerShell.

2. Usando gli stessi valori specificati nello script, eseguire il comando seguente:

    ```ps
    (Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application>  -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application >).token | clip
    ```

    Ad esempio: 

    ```ps
    (Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip`
    ```

#### <a name="step-3-modify-the-powershell-script-to-supply-the-token"></a>Passaggio 3: Modificare lo script di PowerShell in modo da fornire il token

1. Nello script di PowerShell specificare il valore del token incollando la stringa dagli Appunti e salvare il file.

2. Firmare lo script. Se non si firma lo script (condizione più sicura), è necessario configurare Windows PowerShell nel computer che eseguirà i comandi di assegnazione di etichette. Eseguire, ad esempio, la sessione di Windows PowerShell con l'opzione **Esegui come amministratore** e digitare: `Set-ExecutionPolicy RemoteSigned`. Questa configurazione, tuttavia, consente l'esecuzione di tutti gli script non firmati quando sono archiviati in questo computer (condizione meno sicura).

    Per altre informazioni sulla firma degli script di Windows PowerShell, vedere [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing) nella raccolta documenti di PowerShell.

3. Copiare questo script di PowerShell nel computer che assegnerà le etichette e proteggerà i file ed eliminerà l'originale nel computer in uso. Ad esempio, lo script di PowerShell viene copiato in **C:\Scripts\Aipauthentication.ps1** in un computer Windows Server.

#### <a name="step-4-create-a-task-that-runs-the-powershell-script"></a>Passaggio 4: Creare un'attività che esegua lo script di PowerShell

1. Assicurarsi che l'account del servizio per l'assegnazione di etichette e la protezione di file disponga del diritto **Accesso come processo batch**.

2. Nel computer che assegnerà le etichette e proteggerà i file aprire l'Utilità di pianificazione e creare una nuova attività. Configurare questa attività per l'esecuzione come account del servizio per l'assegnazione di etichette e la protezione di file, quindi configurare i valori seguenti per **Azioni**:

   - **Azione**:`Start a program`
   - **Programma/script**:`Powershell.exe`
   - **Aggiungere argomenti (facoltativo)**:`-NoProfile -WindowStyle Hidden -command "&{C:\Scripts\Aipauthentication.ps1}"` 

     Per la riga dell'argomento specificare il percorso e il nome file, se sono diversi da quelli indicati nell'esempio.

3. Eseguire manualmente questa attività.

#### <a name="step-5-confirm-that-the-token-is-saved-and-delete-the-powershell-script"></a>Passaggio 5: confermare che il token è stato salvato ed eliminare lo script di PowerShell

1. Verificare che il token sia ora archiviato nella cartella **%LocalAppData%\Microsoft\MSIP** per il profilo dell'account del servizio. Questo valore è protetto dall'account del servizio.

2. Eliminare lo script di PowerShell che contiene il valore del token, ad esempio **Aipauthentication.ps1.**

    Facoltativamente, eliminare l'attività. Se il token scade, è necessario ripetere questa procedura; in questo caso, potrebbe essere più opportuno uscire dall'attività configurata in modo che sia pronta per una nuova esecuzione quando si copia il nuovo script di PowerShell con il nuovo valore del token.

## <a name="next-steps"></a>Passaggi successivi
Per le informazioni della Guida sui cmdlet, all'interno di una sessione di PowerShell digitare `Get-Help <cmdlet name> cmdlet`. Per ottenere le informazioni più aggiornate, usare il parametro -online. Ad esempio: 

```ps
Get-Help Get-RMSTemplate -online
```

Per altre informazioni necessarie per supportare il client Azure Information Protection, vedere gli argomenti seguenti:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)
