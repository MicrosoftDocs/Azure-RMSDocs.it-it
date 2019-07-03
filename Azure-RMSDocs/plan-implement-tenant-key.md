---
title: Chiave del tenant di Azure Information Protection
description: Anziché affidare a Microsoft la gestione della chiave radice per Azure Information Protection, è possibile creare e gestire questa chiave (noti come "bring your own key" o BYOK) per il tenant, per assicurare la conformità alle normative specifiche.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 099d82892cefd36ef1cd8b6e0f2c224b5d0c1c49
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521952"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Pianificazione e implementazione della chiave del tenant di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni presenti in questo articolo per pianificare e gestire la chiave del tenant di Azure Information Protection. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita), per rispettare i criteri aziendali potrebbe essere necessario, ad esempio, gestire autonomamente la propria chiave del tenant in base alla modalità BYOK (Bring Your Own Key).

Che cos'è la chiave del tenant di Azure Information Protection?

- La chiave del tenant di Azure Information Protection è una chiave radice per l'organizzazione. Le altre chiavi possono essere derivate dalla chiave radice, ad esempio le chiavi utente, le chiavi computer e le chiavi di crittografia dei documenti. Ogni volta che Azure Information Protection usa queste chiavi per l'organizzazione, le chiavi vengono concatenate a livello di crittografia alla chiave del tenant di Azure Information Protection.

- La chiave del tenant di Azure Information Protection è l'equivalente online della chiave del certificato concessore di licenze server (SLC) di Active Directory Rights Management Services (AD RMS). 

**Panoramica:** Usare la tabella seguente come Guida rapida alla topologia di chiave del tenant consigliata. Per altre informazioni, vedere quindi la documentazione aggiuntiva.

|Requisito aziendale|Topologia di chiave del tenant consigliata|
|------------------------|-----------------------------------|
|Distribuire Azure Information Protection in modo rapido e senza hardware speciali, software aggiuntivo o una sottoscrizione di Azure.<br /><br />Ad esempio:  Esecuzione del test degli ambienti e quando l'organizzazione non ha i requisiti normativi per la gestione delle chiavi.|Gestita da Microsoft|
|Normative di conformità e controllo su tutte le operazioni del ciclo di vita. <br /><br />Ad esempio:  La chiave deve essere protetta da un modulo di protezione hardware (HSM).|BYOK|


Se necessario, è possibile modificare la topologia della chiave tenant dopo la distribuzione, usando il [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) cmdlet.


## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>Scegliere il tenant di topologia di chiave: Gestita da Microsoft (impostazione predefinita) o gestita dall'utente (BYOK)

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
|Il tenant di Azure Information Protection deve avere una sottoscrizione di Azure. Se non è disponibile una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/). <br /><br /> Per usare una chiave protetta dal modulo di protezione hardware, è necessario avere un piano tariffario Premium di Azure Key Vault.|La sottoscrizione gratuita di Azure, che fornisce l'accesso per configurare Azure Active Directory e i modelli personalizzati di Azure Rights Management (**Accesso ad Azure Active Directory**), non è sufficiente per usare Insieme di credenziali delle chiavi di Azure. Per verificare di avere una sottoscrizione di Azure che è possibile usare per la modalità BYOK, usare [Azure PowerShell](/powershell/azure/overview) cmdlet: <br /><br /> 1. Avviare una sessione di PowerShell di Azure con il **Esegui come amministratore** opzione e accedere come amministratore globale per il tenant di Azure Information Protection tramite `Connect-AzAccount` e quindi copiare e incollare la stringa del token risulta `https://microsoft.com/devicelogin`usando un browser. <br /><br /> Per altre informazioni, vedere [Accedi con Azure PowerShell](/powershell/azure/authenticate-azureps). <br /><br />2. Digitare il comando seguente e verificare che siano visualizzati valori per il nome e l'ID della sottoscrizione e per l'ID del tenant di Azure Information Protection e che lo stato sia abilitato: `Get-AzSubscription`<br /><br />Se non viene visualizzato alcun valore e viene solo restituito il prompt, non si dispone di una sottoscrizione di Azure utilizzabile per la modalità BYOK. <br /><br />**Nota**: Oltre ai prerequisiti BYOK, se si esegue la migrazione da AD RMS ad Azure Information Protection con chiave software a chiave hardware, è necessario disporre almeno la versione 11.62 o successive se si utilizza il firmware Thales per modulo di protezione hardware.|
|Per usare una chiave protetta dal modulo di protezione hardware creata in locale: <br /><br />- Tutti i prerequisiti elencati per la modalità BYOK in Key Vault. |Vedere [Prerequisiti per la modalità BYOK](/azure/key-vault/key-vault-hsm-protected-keys#prerequisites-for-byok) nella documentazione relativa ad Insieme di credenziali delle chiavi di Azure. <br /><br /> **Nota**: Oltre ai prerequisiti BYOK, se si esegue la migrazione da AD RMS ad Azure Information Protection con chiave software a chiave hardware, è necessario disporre almeno la versione 11.62 o successive se si utilizza il firmware Thales per modulo di protezione hardware.|
|Se l'insieme di credenziali delle chiavi per contenere la chiave del tenant usa gli endpoint servizio di rete virtuale per Azure Key Vault: <br /><br />- Consentire ai servizi Microsoft considerati attendibili di ignorare il firewall.|Per altre informazioni, vedere [Endpoint servizio di rete virtuale per Azure Key Vault](/azure/key-vault/key-vault-overview-vnet-service-endpoints).|
|Il modulo PowerShell di AIPService per Azure Information Protection.|Per istruzioni sull'installazione, vedere [installazione del modulo AIPService PowerShell](./install-powershell.md).|

Per altre informazioni sul modulo di protezione hardware nShield nCipher (HSM) e su come vengono usati con Azure Key Vault, vedere la [sito Web nCipher](https://www.ncipher.com/products/key-management/cloud-microsoft-azure/how-to-buy).

### <a name="choosing-your-key-vault-location"></a>Scelta del percorso dell'insieme di credenziali delle chiavi

Quando si crea un insieme di credenziali delle chiavi che dovrà contenere la chiave da usare come chiave del tenant per Azure Information Protection è necessario specificare un percorso. Il percorso di trova in un'area di Azure o un'istanza di Azure.

Scegliere un'opzione innanzitutto per ragioni di conformità e quindi per ridurre al minimo la latenza di rete:

- Se è stata scelta la topologia di chiave BYOK per ragioni di conformità, i requisiti di conformità potrebbero richiedere l'area di Azure o l'istanza di Azure in cui è archiviata la chiave del tenant di Azure Information Protection.

- Poiché tutte le chiamate alle funzioni di crittografia per la protezione vengono collegate alla chiave del tenant di Azure Information Protection, si vuole ridurre al minimo la latenza di rete causata dalla chiamate. A tale scopo, creare l'insieme di credenziali delle chiavi nella stessa area o istanza di Azure del tenant di Azure Information Protection.

Per identificare la posizione del tenant di Azure Information Protection, usare il [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) cmdlet di PowerShell e identificare l'area dagli URL. Ad esempio:

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


### <a name="instructions-for-byok"></a>Istruzioni per BYOK

Usare la documentazione di Azure Key Vault per creare un insieme di credenziali delle chiavi e la chiave che si vuole usare per Azure Information Protection. Ad esempio, vedere [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started).

Assicurarsi che la lunghezza della chiave sia 2048 bit (consigliata) o 1024 bit. Altre lunghezze di chiave non sono supportate da Azure Information Protection. 

Non usare una chiave a 1024 bit come chiave attiva del tenant perché viene considerato per offrire un livello di protezione inadeguato. Microsoft non approva né fornisce dichiarazioni l'uso di lunghezze di chiave inferiore, ad esempio le chiavi RSA di 1024 bit e l'uso dei protocolli che offrono livelli non adeguati di protezione, ad esempio SHA-1 associata. È consigliabile spostare in una lunghezza di chiave superiore.

Per creare una chiave protetta dal modulo di protezione hardware in locale e trasferirla nell'insieme di credenziali delle chiavi come chiave protetta dal modulo di protezione hardware, seguire le procedure descritte in [Come generare e trasferire chiavi protette dal modulo di protezione hardware per Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys).

Per consentire ad Azure Information Protection di usare la chiave, è necessario autorizzare tutte le operazioni di Key Vault per la chiave. Questa è la configurazione predefinita e le operazioni sono crittografare e decrittografare, wrapKey, unwrapKey, sign e verificano. È possibile controllare le operazioni consentite di una chiave usando il comando PowerShell seguente: `(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps`. Se necessario, aggiungere operazioni consentite usando [Update-AzKeyVaultKey](/powershell/module/az.keyvault/update-azkeyvaultkey) e il *KeyOps* parametro.

Le chiavi archiviate in Key Vault hanno un ID chiave. L'ID chiave è un URL che contiene il nome dell'insieme di credenziali delle chiavi, il contenitore delle chiavi e il nome e la versione della chiave. Ad esempio: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** . È necessario configurare Azure Information Protection per l'uso della chiave specificando l'URL dell'insieme di credenziali delle chiavi.

Affinché Azure Information Protection possa usare la chiave, il servizio Azure Rights Management deve essere autorizzato a usare la chiave nell'insieme di credenziali delle chiavi dell'organizzazione. A tale scopo, l'amministratore di Azure Key Vault può usare il portale di Azure o Azure PowerShell:

Configurazione mediante il portale di Azure:

1. Passare a **Insiemi di credenziali delle chiavi** >  **\<*nome dell'insieme di credenziali delle chiavi*>**  > **Criteri di accesso** > **Aggiungi nuovo**.

2. Nel pannello **Aggiungi criterio di accesso** selezionare **Azure Information Protection BYOK** dalla casella di riepilogo **Configure from template (optional)** (Configura da modello - Facoltativo) e fare clic su **OK**.
    
    Il modello selezionato ha la configurazione seguente:
    
    - **Microsoft Rights Management Services** viene assegnato automaticamente per **Selezionare un'entità**.
    - **Get**, **Decrypt** e **Sign** vengono selezionati automaticamente per le autorizzazioni delle chiavi. 

Configurazione mediante PowerShell:

- Eseguire il cmdlet di PowerShell di insieme di credenziali delle chiavi [Set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)e concedere le autorizzazioni all'entità servizio Azure Rights Management, usando il GUID **00000012-0000-0000-C000-000000000000**. Ad esempio:
    
        Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get

A questo punto è possibile configurare Azure Information Protection per l'uso di questa chiave come chiave del tenant di Azure Information Protection dell'organizzazione. Tramite i cmdlet di Azure RMS, connettersi al servizio Azure Rights Management e accedere:

    Connect-AipService

Quindi eseguire la [cmdlet di uso AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey), specificando la chiave di URL. Ad esempio:

    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> In questo esempio, "aaaabbbbcccc111122223333" è la versione della chiave da usare. Se non si specifica la versione, viene usata la versione corrente della chiave senza avviso e il comando sembra funzionare. Tuttavia, se la chiave nell'insieme di credenziali delle chiavi viene aggiornata in un secondo momento (rinnovo), il servizio Azure Rights Management smetterà di funzionare per il tenant, anche se si esegue il comando Usa AipServiceKeyVaultKey nuovamente.
> 
> Assicurarsi di specificare la versione e il nome della chiave quando si esegue questo comando. È possibile usare il comando, Azure Key Vault [Get-AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey), per ottenere il numero di versione della chiave corrente. ad esempio `Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

Se è necessario verificare se l'URL della chiave è impostato correttamente per Azure Information Protection: In Azure Key Vault, eseguire [Get-AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) per visualizzare la chiave di URL.

Infine, se il servizio Azure Rights Management è già attivato, eseguire [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) per indicare a Azure Information Protection per usare questa chiave come chiave del tenant attivo per il servizio Azure Rights Management. Se non si esegue questo passaggio, Azure Information Protection continuerà a usare la chiave gestita da Microsoft predefinita creata automaticamente per il tenant.


## <a name="next-steps"></a>Passaggi successivi

Dopo aver eseguito la pianificazione e, se necessario, creato e configurato la chiave del tenant, eseguire queste operazioni:

1.  Iniziare a usare la chiave del tenant.
    
    - Se il servizio di protezione non è già attivato, è ora necessario attivare il servizio Rights Management in modo che l'organizzazione possa iniziare a usare Azure Information Protection. Gli utenti iniziano immediatamente a usare la chiave del tenant (gestita da Microsoft o gestita dall'utente in Azure Key Vault).
    
        Per altre informazioni, vedere [attivazione del servizio di protezione di Azure Information Protection](./activate-service.md).
        
    - Se il servizio Rights Management è già stato attivato e si è deciso di gestire la propria chiave del tenant, gli utenti passano gradualmente dalla chiave del tenant precedente a quella nuova. Il completamento di questa transizione in fasi successive può richiedere alcune settimane. I documenti e i file protetti con la chiave del tenant precedente rimangono accessibili agli utenti autorizzati.
        
2. Valutare l'opportunità di usare la registrazione dei dati di utilizzo per tenere traccia di ogni transazione eseguita dal servizio Azure Rights Management.
    
    Se si è deciso di gestire la propria chiave del tenant, la registrazione include informazioni sull'uso della chiave stessa. Vedere il frammento seguente di un file di log visualizzato in Excel in cui i tipi di richiesta **KeyVaultDecryptRequest** e **KeyVaultSignRequest** dimostrano che la chiave del tenant è attualmente in uso.
    
    ![file di log visualizzato in Excel in cui è attualmente usata la chiave del tenant](./media/RMS_Logging.png)
    
    Per altre informazioni sulla registrazione dell'utilizzo, vedere [la registrazione e analisi dell'utilizzo di protezione di Azure Information Protection](./log-analyze-usage.md).
    
3.  Gestire la chiave del tenant.
    
    Per altre informazioni sulle operazioni del ciclo di vita della chiave del tenant, vedere [Operazioni relative alla chiave del tenant di Azure Information Protection](./operations-tenant-key.md).
