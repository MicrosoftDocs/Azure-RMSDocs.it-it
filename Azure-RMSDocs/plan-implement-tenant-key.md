---
title: Chiave del tenant di Azure Information Protection
description: Anziché Microsoft gestire la chiave radice per Azure Information Protection, è possibile creare e gestire questa chiave (denominata "Bring your own key" o BYOK) per il tenant, per conformarsi a normative specifiche.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5490122285549d3fd21ce63b8951cb09a1310f84
ms.sourcegitcommit: 6ae7844205506786e09937f663457572bc8f71c4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2019
ms.locfileid: "70800838"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Pianificazione e implementazione della chiave del tenant di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni presenti in questo articolo per pianificare e gestire la chiave del tenant di Azure Information Protection. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita), per rispettare i criteri aziendali potrebbe essere necessario, ad esempio, gestire autonomamente la propria chiave del tenant in base alla modalità BYOK (Bring Your Own Key).

Che cos'è la chiave del tenant di Azure Information Protection?

- La chiave del tenant di Azure Information Protection è una chiave radice per l'organizzazione. Le altre chiavi possono essere derivate dalla chiave radice, ad esempio le chiavi utente, le chiavi computer e le chiavi di crittografia dei documenti. Ogni volta che Azure Information Protection usa queste chiavi per l'organizzazione, le chiavi vengono concatenate a livello di crittografia alla chiave del tenant di Azure Information Protection.

- La chiave del tenant di Azure Information Protection è l'equivalente online della chiave del certificato concessore di licenze server (SLC) di Active Directory Rights Management Services (AD RMS). 

**Panoramica:** Usare la tabella seguente come guida rapida per la topologia di chiave del tenant consigliata. Per altre informazioni, vedere quindi la documentazione aggiuntiva.

|Requisito aziendale|Topologia di chiave del tenant consigliata|
|------------------------|-----------------------------------|
|Distribuire Azure Information Protection in modo rapido e senza hardware speciali, software aggiuntivo o una sottoscrizione di Azure.<br /><br />Ad esempio:  Esecuzione del test degli ambienti e quando l'organizzazione non ha i requisiti normativi per la gestione delle chiavi.|Gestita da Microsoft|
|Normative di conformità e controllo su tutte le operazioni del ciclo di vita. <br /><br />Esempio: La chiave deve essere protetta da un modulo di protezione hardware (HSM).|BYOK|


Se necessario, è possibile modificare la topologia della chiave del tenant dopo la distribuzione, usando il cmdlet [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) .


## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>Scegliere la topologia della chiave del tenant: Gestito da Microsoft (impostazione predefinita) o gestito dall'utente (BYOK)

Individuare la topologia di chiave del tenant più adatta per l'organizzazione:

- **Gestita da Microsoft**: Microsoft genera automaticamente una chiave del tenant per l'organizzazione e questa chiave viene usata esclusivamente per Microsoft Azure Information Protection. Per impostazione predefinita, Microsoft usa questa chiave per il tenant e gestisce la maggior parte degli aspetti del ciclo di vita della chiave del tenant. 
    
    Questa opzione è quella più semplice e prevede il sovraccarico amministrativo minore. Nella maggior parte dei casi non è nemmeno necessario disporre di una chiave del tenant, ma è sufficiente iscriversi ad Azure Information Protection e la parte rimanente del processo di gestione delle chiavi viene eseguita da Microsoft.

- **Gestita dall'utente (BYOK)** : per il controllo completo sulla chiave del tenant, usare [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) con Azure Information Protection. Per questa topologia di chiave del tenant, la chiave viene creata direttamente in Key Vault o in locale. Se la chiave viene creata in locale, la chiave viene successivamente trasferita o importata in Key Vault. Viene quindi configurato Azure Information Protection per l'uso della chiave che viene gestita in Azure Key Vault.
    

### <a name="more-information-about-byok"></a>Altre informazioni su BYOK
Per creare la chiave, sono disponibili le opzioni seguenti:

- **Una chiave creata in locale e trasferita o importata in Key Vault**:
    
    - Una chiave protetta dal modulo di protezione hardware creata in locale e trasferita in Key Vault come chiave protetta dal modulo di protezione hardware.
    
    - Una chiave protetta da software creata in locale, convertita e quindi trasferita in Key Vault come chiave protetta dal modulo di protezione hardware. Questa opzione è supportata solo quando si [esegue la migrazione da Active Directory Rights Management Services (AD RMS)](migrate-from-ad-rms-to-azure-rms.md).
    
    - Una chiave protetta da software creata in locale e importata in Key Vault come chiave protetta da software. Questa opzione richiede un file di certificato PFX.
    
- **Una chiave creata in Key Vault**:
    
    - Una chiave protetta dal modulo di protezione hardware creata in Key Vault.
    
    - Una chiave protetta da software creata in Key Vault.

Tra queste opzioni BYOK, l'opzione usata più di frequente è rappresentata da una chiave protetta dal modulo di protezione hardware creata in locale e trasferita in Key Vault come chiave protetta dal modulo di protezione hardware. Sebbene preveda il maggior sovraccarico amministrativo, questa opzione potrebbe essere necessaria per consentire all'organizzazione di essere conforme a normative specifiche. I moduli di protezione hardware usati da Azure Key Vault hanno la convalida FIPS 140-2 Livello 2.

e prevede lo schema seguente.

1. Generazione della chiave del tenant in locale, in base ai criteri IT e ai criteri di sicurezza dell'organizzazione. Questa chiave è la copia master. Rimane in locale e l'utente è responsabile dell'esecuzione del backup.

2. Creare una copia della chiave e trasferirla dal modulo di protezione hardware ad Azure Key Vault. Durante il processo, la copia master della chiave non oltrepassa mai la protezione hardware.

3. La copia della chiave è protetta da Azure Key Vault.

> [!NOTE]
> 
> Come misura di protezione aggiuntiva, Azure Key Vault usa domini di sicurezza separati per i propri data center in aree quali America del Nord, EMEA (Europa, Medio Oriente e Africa) e Asia. Azure Key Vault usa anche istanze diverse di Azure, ad esempio Microsoft Azure Germania e Azure per enti pubblici. 

Anche se facoltativo, può essere utile usare i log di utilizzo di Azure Information Protection disponibili in tempo quasi reale per sapere esattamente come e quando viene usata la chiave del tenant.

Quando si usa BYOK per la chiave del tenant Azure Information Protection, non è possibile esportare il dominio di pubblicazione trusted. Il file di pubblicazione trusted è necessario se si decide di non usare più Azure Information Protection ma deve comunque essere in grado di decrittografare il contenuto protetto da Azure Information Protection. Per prepararsi a questo scenario creando in anticipo un valore di pubblicazione trusted appropriato, vedere le istruzioni seguenti [come preparare un Azure Information Protection piano di "cloud Exit"](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631).

### <a name="when-you-have-decided-your-tenant-key-topology"></a>Dopo aver scelto la topologia della chiave del tenant

Se si decide di affidare a Microsoft la gestione della chiave del tenant: 

- Se non si sta eseguendo una migrazione da AD RMS, non è necessaria alcuna azione aggiuntiva per generare la chiave per il tenant ed è possibile passare direttamente alla sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps).

- Se si usa AD RMS e si vuole passare ad Azure Information Protection, usare le istruzioni per la migrazione riportate in: [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). 

Se invece si decide di gestire in modo autonomo la propria chiave del tenant, leggere le sezioni seguenti per ottenere altre informazioni.

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Implementazione di BYOK per la chiave del tenant di Azure Information Protection

Usare le informazioni e le procedure descritte in questa sezione se si è deciso di generare e gestire la propria chiave del tenant in base allo schema BYOK.

> [!NOTE]
> Se si è iniziato a usare Azure Information Protection con una chiave del tenant gestita da Microsoft e si vuole gestire la chiave del tenant autonomamente (passare alla modalità BYOK), i documenti e i messaggi di posta elettronica precedentemente protetti saranno comunque accessibili tramite una chiave archiviata. 

### <a name="prerequisites-for-byok"></a>Prerequisiti per la modalità BYOK
Nella tabella seguente sono elencati i prerequisiti per la modalità BYOK.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Il tenant di Azure Information Protection deve avere una sottoscrizione di Azure. Se non è disponibile una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/). <br /><br /> Per usare una chiave protetta dal modulo di protezione hardware, è necessario avere un piano tariffario Premium di Azure Key Vault.|La sottoscrizione gratuita di Azure, che fornisce l'accesso per configurare Azure Active Directory e i modelli personalizzati di Azure Rights Management (**Accesso ad Azure Active Directory**), non è sufficiente per usare Insieme di credenziali delle chiavi di Azure. Per confermare di avere una sottoscrizione di Azure che è possibile usare per BYOK, usare i cmdlet di [Azure PowerShell](/powershell/azure/overview) : <br /><br /> 1. Avviare una sessione di Azure PowerShell con l'opzione **Esegui come amministratore** e accedere come amministratore globale per il tenant di Azure Information Protection usando `Connect-AzAccount` , quindi copiare e incollare la stringa del token risultante in `https://microsoft.com/devicelogin`usando un Browser. <br /><br /> Per altre informazioni, vedere [accedere con Azure PowerShell](/powershell/azure/authenticate-azureps). <br /><br />2. Digitare il comando seguente e verificare che siano visualizzati valori per il nome e l'ID della sottoscrizione e per l'ID del tenant di Azure Information Protection e che lo stato sia abilitato: `Get-AzSubscription`<br /><br />Se non viene visualizzato alcun valore e viene solo restituito il prompt, non si dispone di una sottoscrizione di Azure utilizzabile per la modalità BYOK. <br /><br />**Nota**: Oltre ai prerequisiti di BYOK, se si esegue la migrazione da AD RMS a Azure Information Protection tramite la chiave software a chiave hardware, è necessario avere una versione minima di 11,62 se si usa il firmware Thales per il modulo di protezione hardware.|
|Per usare una chiave protetta dal modulo di protezione hardware creata in locale: <br /><br />- Tutti i prerequisiti elencati per la modalità BYOK in Key Vault. |Vedere [Prerequisiti per la modalità BYOK](/azure/key-vault/key-vault-hsm-protected-keys#prerequisites-for-byok) nella documentazione relativa ad Insieme di credenziali delle chiavi di Azure. <br /><br /> **Nota**: Oltre ai prerequisiti di BYOK, se si esegue la migrazione da AD RMS a Azure Information Protection tramite la chiave software a chiave hardware, è necessario avere una versione minima di 11,62 se si usa il firmware Thales per il modulo di protezione hardware.|
|Se l'insieme di credenziali delle chiavi per contenere la chiave del tenant usa gli endpoint servizio di rete virtuale per Azure Key Vault: <br /><br />- Consentire ai servizi Microsoft considerati attendibili di ignorare il firewall.|Per altre informazioni, vedere [Endpoint servizio di rete virtuale per Azure Key Vault](/azure/key-vault/key-vault-overview-vnet-service-endpoints).|
|Il modulo AIPService di PowerShell per Azure Information Protection.|Per le istruzioni di installazione, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).|

Per ulteriori informazioni sul modulo di protezione hardware (HSM) nCipher nShield e sul relativo utilizzo con Azure Key Vault, vedere il [sito Web nCipher](https://www.ncipher.com/products/key-management/cloud-microsoft-azure/how-to-buy).

### <a name="choosing-your-key-vault-location"></a>Scelta del percorso dell'insieme di credenziali delle chiavi

Quando si crea un insieme di credenziali delle chiavi che dovrà contenere la chiave da usare come chiave del tenant per Azure Information Protection è necessario specificare un percorso. Il percorso di trova in un'area di Azure o un'istanza di Azure.

Scegliere un'opzione innanzitutto per ragioni di conformità e quindi per ridurre al minimo la latenza di rete:

- Se è stata scelta la topologia di chiave BYOK per ragioni di conformità, i requisiti di conformità potrebbero richiedere l'area di Azure o l'istanza di Azure in cui è archiviata la chiave del tenant di Azure Information Protection.

- Poiché tutte le chiamate alle funzioni di crittografia per la protezione vengono collegate alla chiave del tenant di Azure Information Protection, si vuole ridurre al minimo la latenza di rete causata dalla chiamate. A tale scopo, creare l'insieme di credenziali delle chiavi nella stessa area o istanza di Azure del tenant di Azure Information Protection.

Per identificare il percorso del tenant di Azure Information Protection, usare il cmdlet di PowerShell [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) e identificare l'area dagli URL. Ad esempio:

    LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

L'area è identificabile da **rms.na.aadrm.com** e, nell'esempio, si trova in America del Nord.

Usare la tabella seguente per identificare l'area o l'istanza di Azure consigliata per ridurre al minimo la latenza di rete.

|Area o istanza di Azure|Percorso dell'insieme di credenziali delle chiavi consigliato|
|---------------|--------------------|
|rms.**na**.aadrm.com|**Stati Uniti centro-settentrionali** o **Stati Uniti orientali**|
|rms.**eu**.aadrm.com|**Europa settentrionale** o **Europa occidentale**|
|rms.**ap**.aadrm.com|**Asia orientale** o **Asia sud-orientale**|
|rms.**sa**.aadrm.com|**Stati Uniti occidentali** o **Stati Uniti orientali**|
|rms.**govus**.aadrm.com|**Stati Uniti centrali** o **Stati Uniti orientali 2**|
|RMS.**AADRM.US**|**US gov Virginia** o **US gov Arizona**|
|RMS.**AADRM.cn**|**Cina orientale 2** o **Cina settentrionale 2**|


### <a name="instructions-for-byok"></a>Istruzioni per BYOK

Usare la documentazione di Azure Key Vault per creare un insieme di credenziali delle chiavi e la chiave che si vuole usare per Azure Information Protection. Ad esempio, vedere [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started).

Assicurarsi che la lunghezza della chiave sia 2048 bit (consigliata) o 1024 bit. Altre lunghezze di chiave non sono supportate da Azure Information Protection. 

Non usare una chiave a 1024 bit come chiave del tenant attiva perché viene considerata come un livello di protezione inadeguato. Microsoft non approva l'uso di lunghezze di chiave inferiori, ad esempio chiavi RSA a 1024 bit e l'utilizzo associato di protocolli che offrono livelli di protezione inadeguati, ad esempio SHA-1. Si consiglia di procedere con una lunghezza di chiave superiore.

Per creare una chiave protetta dal modulo di protezione hardware in locale e trasferirla nell'insieme di credenziali delle chiavi come chiave protetta dal modulo di protezione hardware, seguire le procedure descritte in [Come generare e trasferire chiavi protette dal modulo di protezione hardware per Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys).

Per consentire ad Azure Information Protection di usare la chiave, è necessario autorizzare tutte le operazioni di Key Vault per la chiave. Questa è la configurazione predefinita e le operazioni sono Encrypt, Decrypt, wrapKey, unwrapKey, Sign e verify. È possibile controllare le operazioni consentite di una chiave usando il comando di PowerShell `(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps`seguente:. Se necessario, aggiungere le operazioni consentite usando [Update-AzKeyVaultKey](/powershell/module/az.keyvault/update-azkeyvaultkey) e il parametro *KeyOps* .

Le chiavi archiviate in Key Vault hanno un ID chiave. L'ID chiave è un URL che contiene il nome dell'insieme di credenziali delle chiavi, il contenitore delle chiavi e il nome e la versione della chiave. Ad esempio: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** . È necessario configurare Azure Information Protection per l'uso della chiave specificando l'URL dell'insieme di credenziali delle chiavi.

Affinché Azure Information Protection possa usare la chiave, il servizio Azure Rights Management deve essere autorizzato a usare la chiave nell'insieme di credenziali delle chiavi dell'organizzazione. A tale scopo, l'amministratore di Azure Key Vault può usare il portale di Azure o Azure PowerShell:

Configurazione mediante il portale di Azure:

1. Passare a **Insiemi di credenziali delle chiavi** >  **\<*nome dell'insieme di credenziali delle chiavi*>**  > **Criteri di accesso** > **Aggiungi nuovo**.

2. Nel pannello **Aggiungi criterio di accesso** selezionare **Azure Information Protection BYOK** dalla casella di riepilogo **Configure from template (optional)** (Configura da modello - Facoltativo) e fare clic su **OK**.
    
    Il modello selezionato ha la configurazione seguente:
    
    - **Microsoft Rights Management Services** viene assegnato automaticamente per **Selezionare un'entità**.
    - **Get**, **Decrypt** e **Sign** vengono selezionati automaticamente per le autorizzazioni delle chiavi. 

Configurazione mediante PowerShell:

- Eseguire il cmdlet Key Vault PowerShell, [set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy), e concedere le autorizzazioni all'entità servizio Rights Management di Azure, usando il GUID **00000012-0000-0000-C000-000000000000**. Ad esempio:
    
        Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get

A questo punto è possibile configurare Azure Information Protection per l'uso di questa chiave come chiave del tenant di Azure Information Protection dell'organizzazione. Tramite i cmdlet di Azure RMS, connettersi al servizio Azure Rights Management e accedere:

    Connect-AipService

Eseguire quindi il [cmdlet Use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey), specificando l'URL della chiave. Ad esempio:

    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> In questo esempio, "aaaabbbbcccc111122223333" è la versione della chiave da usare. Se non si specifica la versione, viene usata la versione corrente della chiave senza avviso e il comando sembra funzionare. Tuttavia, se la chiave in Key Vault viene aggiornata in un secondo momento (rinnovato), il servizio Azure Rights Management smetterà di funzionare per il tenant, anche se si esegue di nuovo il comando use-AipServiceKeyVaultKey.
> 
> Assicurarsi di specificare la versione e il nome della chiave quando si esegue questo comando. È possibile usare il comando Azure Key Vault cmd [Get-AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey)per ottenere il numero di versione della chiave corrente. Ad esempio: `Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

Se è necessario verificare se l'URL della chiave è impostato correttamente per Azure Information Protection: In Azure Key Vault eseguire [Get-AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) per visualizzare l'URL della chiave.

Infine, se il servizio Azure Rights Management è già attivato, eseguire [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) per indicare Azure Information Protection per usare questa chiave come chiave del tenant attiva per il servizio Rights Management di Azure. Se non si esegue questo passaggio, Azure Information Protection continuerà a usare la chiave gestita da Microsoft predefinita creata automaticamente per il tenant.


## <a name="next-steps"></a>Passaggi successivi

Dopo aver eseguito la pianificazione e, se necessario, creato e configurato la chiave del tenant, eseguire queste operazioni:

1.  Iniziare a usare la chiave del tenant.
    
    - Se il servizio di protezione non è già attivato, è ora necessario attivare il servizio Rights Management in modo che l'organizzazione possa iniziare a usare Azure Information Protection. Gli utenti iniziano immediatamente a usare la chiave del tenant (gestita da Microsoft o gestita dall'utente in Azure Key Vault).
    
        Per ulteriori informazioni sull'attivazione, vedere [attivazione del servizio di protezione da Azure Information Protection](./activate-service.md).
        
    - Se il servizio Rights Management è già stato attivato e si è deciso di gestire la propria chiave del tenant, gli utenti passano gradualmente dalla chiave del tenant precedente a quella nuova. Il completamento di questa transizione in fasi successive può richiedere alcune settimane. I documenti e i file protetti con la chiave del tenant precedente rimangono accessibili agli utenti autorizzati.
        
2. Valutare l'opportunità di usare la registrazione dei dati di utilizzo per tenere traccia di ogni transazione eseguita dal servizio Azure Rights Management.
    
    Se si è deciso di gestire la propria chiave del tenant, la registrazione include informazioni sull'uso della chiave stessa. Vedere il frammento seguente di un file di log visualizzato in Excel in cui i tipi di richiesta **KeyVaultDecryptRequest** e **KeyVaultSignRequest** dimostrano che la chiave del tenant è attualmente in uso.
    
    ![file di log visualizzato in Excel in cui è attualmente usata la chiave del tenant](./media/RMS_Logging.png)
    
    Per ulteriori informazioni sulla registrazione dell'utilizzo, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).
    
3.  Gestire la chiave del tenant.
    
    Per altre informazioni sulle operazioni del ciclo di vita della chiave del tenant, vedere [Operazioni relative alla chiave del tenant di Azure Information Protection](./operations-tenant-key.md).
