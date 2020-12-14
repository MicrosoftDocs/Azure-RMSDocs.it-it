---
title: Dettagli Bring Your Own Key (BYOK)-Azure Information Protection
description: Comprendere i dettagli e le restrizioni quando si usano chiavi gestite dal cliente (note come "Bring your own key" o BYOK) con Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 53c5edea2593a653eec82ec5a61efed58ae76c1f
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383925"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>Dettagli di Bring your own key (BYOK) per Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Le organizzazioni con una sottoscrizione Azure Information Protection possono scegliere di configurare il tenant con la propria chiave, anziché una chiave predefinita generata da Microsoft. Questa configurazione è spesso definita Bring Your Own Key (BYOK).

BYOK e la [registrazione dell'utilizzo](log-analyze-usage.md) funzionano senza interruzioni con le applicazioni che si integrano con il servizio Azure Rights Management usato da Azure Information Protection.

Le applicazioni supportate includono:

- **Servizi cloud**, ad esempio Microsoft SharePoint o Microsoft 365

- **Servizi locali** che eseguono applicazioni Exchange e SharePoint che usano il servizio Azure Rights Management tramite il connettore RMS

- **Applicazioni client**, ad esempio Office 2019, Office 2016 e Office 2013

> [!TIP]
> Se necessario, applicare ulteriore sicurezza a documenti specifici usando una chiave locale aggiuntiva. Per altre informazioni, vedere [protezione con crittografia a chiave doppia (DKE)](plan-implement-tenant-key.md#double-key-encryption-dke) (solo client di etichetta unificata).
>
> Se si dispone del client classico ed è necessaria una protezione aggiuntiva, locale, implementare invece la protezione della [protezione HYOK](configure-adrms-restrictions.md) .
> 

## <a name="azure-key-vault-key-storage"></a>Archiviazione chiavi Azure Key Vault

Le chiavi generate dal cliente devono essere archiviate nel Azure Key Vault per la protezione BYOK.

> [!NOTE]
> L'uso di chiavi protette da HSM nella Azure Key Vault richiede un [livello di servizio Azure Key Vault Premium](https://azure.microsoft.com/pricing/details/key-vault/), che comporta una tariffa di sottoscrizione mensile aggiuntiva.

### <a name="sharing-key-vaults-and-subscriptions"></a>Condivisione di insiemi di credenziali delle chiavi e sottoscrizioni

È consigliabile usare un insieme di credenziali delle **chiavi dedicato** per la chiave del tenant. Gli insiemi di credenziali delle chiavi dedicati consentono di garantire che le chiamate da altri servizi non provochino il superamento dei [limiti del servizio](/azure/key-vault/general/service-limits) . Il superamento dei limiti di servizio nell'insieme di credenziali delle chiavi in cui è archiviata la chiave del tenant può causare la limitazione del tempo di risposta per il servizio Azure Rights Management.

Poiché i diversi servizi presentano requisiti di gestione delle chiavi variabili, Microsoft consiglia anche di usare **una sottoscrizione di Azure dedicata** per l'insieme di credenziali delle chiavi. Sottoscrizioni di Azure dedicate:

- Proteggi da configurazioni errate

- Sono più sicure quando servizi diversi hanno amministratori diversi

Per condividere una sottoscrizione di Azure con altri servizi che usano Azure Key Vault, assicurarsi che la sottoscrizione condivida un insieme comune di amministratori. Conferma che tutti gli amministratori che usano la sottoscrizione hanno una conoscenza approfondita di tutte le chiavi a cui possono accedere, significa che è meno probabile che configurino correttamente le chiavi.

**Esempio**: uso di una sottoscrizione di Azure condivisa quando gli amministratori per la chiave del tenant Azure Information Protection sono gli stessi utenti che amministrano le chiavi per la chiave cliente di Office 365 e CRM online. Se gli amministratori chiave per questi servizi sono diversi, è consigliabile usare sottoscrizioni dedicate.

### <a name="benefits-of-using-azure-key-vault"></a>Vantaggi dell'uso di Insieme di credenziali delle chiavi di Azure

Azure Key Vault offre una soluzione di gestione delle chiavi centralizzata e coerente per molti servizi basati su cloud e locali che usano la crittografia.

Oltre alla gestione delle chiavi, Insieme di credenziali delle chiavi di Azure offre agli amministratori della protezione la stessa esperienza di gestione per archiviare, accedere e gestire i certificati e i segreti, ad esempio le password, per altri servizi e applicazioni che usano la crittografia.

L'archiviazione della chiave del tenant nell'Azure Key Vault offre i vantaggi seguenti:

|Vantaggio  |Descrizione  |
|---------|---------|
|**Interfacce predefinite**| Insieme di credenziali delle chiavi di Azure supporta un numero di interfacce predefinite per la gestione delle chiavi, tra cui PowerShell, l'interfaccia della riga di comando, API REST e il portale di Azure. <br /><br />Altri servizi e strumenti sono integrati con Key Vault per le funzionalità ottimizzate per attività specifiche, ad esempio il monitoraggio. <br /><br />Ad esempio, analizzare i log di utilizzo delle chiavi con Operations Management Suite log Analytics, impostare avvisi quando vengono soddisfatti i criteri specificati e così via.        |
|**Separazione dei ruoli**| Azure Key Vault fornisce la separazione dei ruoli come procedura consigliata di sicurezza riconosciuta. <br /><br />La separazione dei ruoli garantisce che gli amministratori Azure Information Protection possano concentrarsi sulle priorità più elevate, tra cui la gestione della classificazione e della protezione dei dati, nonché le chiavi e i criteri di crittografia per requisiti di sicurezza o conformità specifici. |
|**Posizione della chiave master**| Azure Key Vault è disponibile in diverse posizioni e supporta le organizzazioni con restrizioni in cui è possibile vivere le chiavi master. <br /><br />Per altre informazioni, vedere la pagina [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/) nel sito di Azure.|
|**Domini di sicurezza separati**|Azure Key Vault USA domini di sicurezza distinti per i Data Center in aree quali America del Nord, EMEA (Europa, Medio Oriente e Africa) e Asia. <br /><br />Azure Key Vault usa anche istanze diverse di Azure, ad esempio Microsoft Azure Germania e Azure per enti pubblici. |
|**Esperienza unificata**| Azure Key Vault consente inoltre agli amministratori della sicurezza di archiviare, accedere e gestire i certificati e i segreti, ad esempio le password, per altri servizi che usano la crittografia. <br><br />L'uso di Azure Key Vault per le chiavi del tenant offre un'esperienza utente uniforme per gli amministratori che gestiscono tutti questi elementi.|
| | |

Per gli aggiornamenti più recenti e per informazioni sull'uso di altri servizi  [Azure Key Vault](/azure/key-vault/general/basic-concepts), visitare il [Blog del team di Azure Key Vault](/archive/blogs/kv/).

## <a name="usage-logging-for-byok"></a>Registrazione dell'utilizzo per BYOK

I log di utilizzo vengono generati da tutte le applicazioni che effettuano richieste al servizio Rights Management di Azure.

Anche se la registrazione dell'utilizzo è facoltativa, è consigliabile usare i log di utilizzo quasi in tempo reale da Azure Information Protection per vedere esattamente come e quando viene usata la chiave del tenant.

Per ulteriori informazioni sulla registrazione dell'utilizzo delle chiavi per BYOK, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](log-analyze-usage.md).

> [!TIP]
> Per una maggiore sicurezza, Azure Information Protection la registrazione dell'utilizzo può essere a cui viene fatto riferimento con [Azure Key Vault la registrazione](/azure/key-vault/general/logging). I log Key Vault forniscono un metodo affidabile per monitorare in modo indipendente che la chiave venga usata solo dal servizio Rights Management di Azure.
>
> Se necessario, revocare immediatamente l'accesso alla chiave rimuovendo le autorizzazioni per l'insieme di credenziali delle chiavi.

## <a name="options-for-creating-and-storing-your-key"></a>Opzioni per la creazione e l'archiviazione della chiave

> [!NOTE]
> Il Azure Information Protection Azure Key Vault supporto HSM gestito, per l'uso solo con tenant non di produzione, è attualmente in fase di anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
>
> Per ulteriori informazioni sull'offerta HSM gestita e su come configurare un insieme di credenziali e una chiave, vedere la [documentazione Azure Key Vault](/azure/key-vault/). 
>
> Di seguito vengono descritte le istruzioni aggiuntive sulla concessione dell'autorizzazione chiave.
>

BYOK supporta le chiavi create in Azure Key Vault o in locale.

Se si crea la chiave in locale, è necessario trasferirla o importarla nel Key Vault e configurare Azure Information Protection per usare la chiave. Eseguire eventuali altre operazioni di gestione delle chiavi dall'interno Azure Key Vault.

Opzioni per creare e archiviare una chiave personalizzata:

- **Creato in Azure Key Vault**. Creare e archiviare la chiave in Azure Key Vault come una chiave protetta dal modulo di protezione hardware o una chiave protetta tramite software.

- **Creato in locale**. Creare la chiave in locale e trasferirla a Azure Key Vault usando una delle opzioni seguenti:

    - **Chiave protetta dal modulo di protezione hardware, trasferita come chiave protetta dal modulo di protezione hardware**. Metodo più comune scelto.

        Sebbene questo metodo abbia il sovraccarico amministrativo, potrebbe essere necessario che l'organizzazione segua normative specifiche. I HSM usati da Azure Key Vault sono FIPS 140-2 livello 2 convalidati.

    - **Chiave protetta da software convertita e trasferita a Azure Key Vault come chiave protetta dal modulo di protezione hardware**. Questo metodo è supportato solo quando si [esegue la migrazione da Active Directory Rights Management Services (ad RMS)](migrate-from-ad-rms-to-azure-rms.md).

    - **Creato in locale come chiave protetta tramite software e trasferito a Azure Key Vault come chiave protetta da software**. Questo metodo richiede un oggetto. File di certificato PFX.

Ad esempio, per usare una chiave creata in locale, eseguire le operazioni seguenti:

1. Genera la tua chiave del tenant in locale, in linea con i criteri IT e di sicurezza dell'organizzazione. Questa chiave è la copia master. Rimane in locale ed è necessario per il backup.

1. Creare una copia della chiave master e trasferirla in modo sicuro dal modulo di protezione hardware per Azure Key Vault. Durante questo processo, la copia master della chiave non lascia mai il limite di protezione hardware.

Una volta trasferita, la copia della chiave viene protetta da Azure Key Vault.

## <a name="exporting-your-trusted-publishing-domain"></a>Esportazione del dominio di pubblicazione trusted

Se si decide di interrompere l'uso di Azure Information Protection, è necessario un dominio di pubblicazione trusted per decrittografare il contenuto protetto da Azure Information Protection.

Tuttavia, l'esportazione del codice di pubblicazione trusted non è supportata se si usa BYOK per la chiave Azure Information Protection.

Per prepararsi a questo scenario, assicurarsi di creare in anticipo un valore di pubblicazione trusted appropriato. Per ulteriori informazioni, vedere [How to prepare an Azure Information Protection "cloud Exit" Plan](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631).

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Implementazione di BYOK per la chiave del tenant di Azure Information Protection

Per implementare BYOK, attenersi alla procedura seguente:

1. [Verificare i prerequisiti di BYOK](#prerequisites-for-byok)
1. [Scegliere un percorso di Key Vault](#choosing-your-key-vault-location)
1. [Creare e configurare la chiave](#create-and-configure-your-key)

### <a name="prerequisites-for-byok"></a>Prerequisiti per la modalità BYOK

I prerequisiti di BYOK variano a seconda della configurazione del sistema. Verificare che il sistema soddisfi i prerequisiti seguenti, se necessario:

|Requisito  |Descrizione  |
|---------|---------|
|**Sottoscrizione di Azure**     |Obbligatorio per tutte le configurazioni. <br />Per altre informazioni, vedere [Verifica della presenza di una sottoscrizione di Azure compatibile con BYOK](#verifying-that-you-have-a-byok-compatible-azure-subscription).         |
|**Modulo AIPService di PowerShell per Azure Information Protection**|Obbligatorio per tutte le configurazioni. <br />Per altre informazioni, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).|
|**Prerequisiti Azure Key Vault per BYOK** | Se si usa una chiave protetta dal modulo di protezione hardware creata in locale, assicurarsi di rispettare anche i [prerequisiti per BYOK](/azure/key-vault/keys/hsm-protected-keys-byok#prerequisites) elencati nella documentazione di Azure Key Vault.         |
|**Firmware Thales versione 11,62**    |È necessario avere una versione del firmware Thales 11,62 se si esegue la migrazione da AD RMS a Azure Information Protection usando la chiave software per la chiave hardware e si usa il firmware Thales per il modulo di protezione hardware.
|**Bypass del firewall per i servizi Microsoft attendibili** |Se l'insieme di credenziali delle chiavi che contiene la chiave del tenant usa gli endpoint di servizio della rete virtuale per Azure Key Vault, è necessario consentire ai servizi Microsoft attendibili di ignorare il firewall. <br />Per altre informazioni, vedere [Endpoint servizio di rete virtuale per Azure Key Vault](/azure/key-vault/general/overview-vnet-service-endpoints).       |
| | |

#### <a name="verifying-that-you-have-a-byok-compatible-azure-subscription"></a>Verifica della presenza di una sottoscrizione di Azure compatibile con BYOK

Il tenant di Azure Information Protection deve avere una sottoscrizione di Azure. Se non si ha ancora un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/). Tuttavia, per usare una chiave protetta dal modulo di protezione hardware, è necessario disporre del livello di servizio Azure Key Vault Premium.

La sottoscrizione gratuita di Azure che fornisce l'accesso alla configurazione di Azure Active Directory e alla configurazione dei modelli personalizzati di Azure Rights Management *non* è sufficiente per l'uso di Azure Key Vault.

Per verificare se si dispone di una sottoscrizione di Azure compatibile con BYOK, eseguire le operazioni seguenti per verificare, usando [Azure PowerShell](/powershell/azure/) cmdlet:

1. Avviare un Azure PowerShell sessione come amministratore.

1. Accedere come amministratore globale per il tenant di Azure Information Protection usando `Connect-AzAccount` .

1. Copiare il token visualizzato negli Appunti. Quindi, in un browser, passare a https://microsoft.com/devicelogin e immettere il token copiato.

    Per altre informazioni, vedere [accedere con Azure PowerShell](/powershell/azure/authenticate-azureps).

1. Nella sessione di PowerShell immettere `Get-AzSubscription` e verificare che siano visualizzati i valori seguenti:

    - Nome e ID della sottoscrizione
    - ID tenant di Azure Information Protection
    - Conferma che lo stato è abilitato

    Se non viene visualizzato alcun valore e si torna al prompt, non è disponibile una sottoscrizione di Azure che può essere usata per BYOK.

### <a name="choosing-your-key-vault-location"></a>Scelta del percorso dell'insieme di credenziali delle chiavi

Quando si crea un insieme di credenziali delle chiavi che dovrà contenere la chiave da usare come chiave del tenant per Azure Information Protection è necessario specificare un percorso. Il percorso di trova in un'area di Azure o un'istanza di Azure.

Scegliere un'opzione innanzitutto per ragioni di conformità e quindi per ridurre al minimo la latenza di rete:

- Se è stato scelto il metodo della chiave BYOK per motivi di conformità, i requisiti di conformità possono anche richiedere quale area o istanza di Azure può essere usata per archiviare la chiave del tenant Azure Information Protection.

- Tutte le chiamate crittografiche per la catena di protezione alla chiave Azure Information Protection. Pertanto, è possibile ridurre al minimo la latenza di rete richiesta dalle chiamate creando l'insieme di credenziali delle chiavi nella stessa area o istanza di Azure del tenant Azure Information Protection.

Per identificare il percorso del tenant di Azure Information Protection, usare il cmdlet di PowerShell [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) e identificare l'area dagli URL. ad esempio:

```PowerShell
LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing
```
    
L'area è identificabile da **rms.na.aadrm.com** e, nell'esempio, si trova in America del Nord.

La tabella seguente elenca le aree e le istanze di Azure consigliate per ridurre al minimo la latenza di rete:

|Area o istanza di Azure|Percorso dell'insieme di credenziali delle chiavi consigliato|
|---------------|--------------------|
|rms.**na**.aadrm.com|**Stati Uniti centro-settentrionali** o **Stati Uniti orientali**|
|rms.**eu**.aadrm.com|**Europa settentrionale** o **Europa occidentale**|
|rms.**ap**.aadrm.com|**Asia orientale** o **Asia sud-orientale**|
|rms.**sa**.aadrm.com|**Stati Uniti occidentali** o **Stati Uniti orientali**|
|rms.**govus**.aadrm.com|**Stati Uniti centrali** o **Stati Uniti orientali 2**|
|RMS.**AADRM.US**|**US gov Virginia** o **US gov Arizona**|
|RMS.**AADRM.cn**|**Cina orientale 2** o **Cina settentrionale 2**|
| | |

### <a name="create-and-configure-your-key"></a>Creare e configurare la chiave

>[!IMPORTANT]
> Per informazioni specifiche per HSM gestiti, vedere [Abilitazione dell'autorizzazione chiave per chiavi HSM gestite tramite l'interfaccia della riga di comando di Azure](#enabling-key-authorization-for-managed-hsm-keys-via-azure-cli).

Creare una Azure Key Vault e la chiave che si vuole usare per Azure Information Protection. Per ulteriori informazioni, vedere la [documentazione Azure Key Vault](/azure/key-vault/).

Per configurare il Azure Key Vault e la chiave per BYOK, tenere presente quanto segue:

- [Requisiti per la lunghezza della chiave](#key-length-requirements)
- [Creazione di una chiave protetta dal modulo di protezione hardware in locale e trasferimento all'insieme di credenziali delle chiavi](#creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault)
- [Configurazione di Azure Information Protection con l'ID chiave](#configuring-azure-information-protection-with-your-key-id)
- [Autorizzazione del servizio Azure Rights Management per l'uso della chiave](#authorizing-the-azure-rights-management-service-to-use-your-key)

#### <a name="key-length-requirements"></a>Requisiti per la lunghezza della chiave

Quando si crea la chiave, verificare che la lunghezza della chiave sia 2048 bit (scelta consigliata) o 1024 bit. Altre lunghezze di chiave non sono supportate da Azure Information Protection.

> [!NOTE]
> non vengono considerate chiavi a 1024 bit per offrire un livello di protezione adeguato per le chiavi del tenant attive.
>
>Microsoft non approva l'utilizzo di lunghezze di chiave inferiori, ad esempio chiavi RSA a 1024 bit, e l'utilizzo associato di protocolli che offrono livelli di protezione inadeguati, ad esempio SHA-1.
>

#### <a name="creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault"></a>Creazione di una chiave protetta dal modulo di protezione hardware in locale e trasferimento all'insieme di credenziali delle chiavi

Per creare una chiave protetta da HSM in locale e trasferirla nell'insieme di credenziali delle chiavi come chiave protetta dal modulo di protezione hardware, seguire le procedure riportate nella documentazione Azure Key Vault: [come generare e trasferire chiavi HSM protette per Azure Key Vault](/azure/key-vault/keys/hsm-protected-keys-byok).

Per Azure Information Protection usare la chiave trasferita, è necessario che tutte le operazioni di Key Vault siano consentite per la chiave, ad esempio:

- encrypt
- decrypt
- wrapKey
- unwrapKey
- segno
- verify

Per impostazione predefinita, sono consentite tutte le operazioni Key Vault.

Per controllare le operazioni consentite per una chiave specifica, eseguire il comando PowerShell seguente:

```PowerShell
(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps
```

Se necessario, aggiungere le operazioni consentite usando [Update-AzKeyVaultKey](/powershell/module/az.keyvault/update-azkeyvaultkey) e il parametro *KeyOps* .

#### <a name="configuring-azure-information-protection-with-your-key-id"></a>Configurazione di Azure Information Protection con l'ID chiave

Le chiavi archiviate nel Azure Key Vault hanno ogni ID chiave.

L'ID chiave è un URL che contiene il nome dell'insieme di credenziali delle chiavi, il contenitore delle chiavi, il nome della chiave e la versione della chiave. ad esempio:

**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**.

Configurare Azure Information Protection per usare la chiave specificando l'URL dell'insieme di credenziali delle chiavi.

#### <a name="authorizing-the-azure-rights-management-service-to-use-your-key"></a>Autorizzazione del servizio Azure Rights Management per l'uso della chiave

Il servizio Rights Management di Azure deve essere autorizzato a usare la chiave. Azure Key Vault gli amministratori possono abilitare questa autorizzazione utilizzando portale di Azure o Azure PowerShell.

##### <a name="enabling-key-authorization-using-the-azure-portal"></a>Abilitazione dell'autorizzazione chiave tramite il portale di Azure

1. Accedere al portale di Azure e passare a **Key Vaults**  >  **\<*your key vault name*>**  >  **Access Policy**(  >  **Aggiungi nuovo**).

1. Dal riquadro **Aggiungi criteri di accesso** selezionare **Azure Information Protection BYOK** nella casella di riepilogo **Configura da modello (facoltativo)** , quindi fare clic su **OK**.

    Il modello selezionato ha la configurazione seguente:

    - Il valore dell' **entità Select** è impostato su **Microsoft Rights Management Services**.
    - Le **autorizzazioni per chiavi** selezionate includono **Get**, **Decrypt** e **Sign**.

##### <a name="enabling-key-authorization-using-powershell"></a>Abilitazione dell'autorizzazione chiave tramite PowerShell

Eseguire il cmdlet Key Vault PowerShell, [set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy), e concedere le autorizzazioni all'entità servizio di Azure Rights Management usando il GUID **00000012-0000-0000-C000-000000000000**.

ad esempio:

```PowerShell
Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get
```

##### <a name="enabling-key-authorization-for-managed-hsm-keys-via-azure-cli"></a>Attivazione dell'autorizzazione chiave per chiavi HSM gestite tramite l'interfaccia della riga di comando di Azure

Per concedere le autorizzazioni utente dell'entità servizio Rights Management di Azure come utente **crittografico HSM gestito** , eseguire il comando seguente:

```PowerShell
az keyvault role assignment create --hsm-name "ContosoMHSM" --role "Managed HSM Crypto User" --assignee 00000012-0000-0000-c000-000000000000 --scope /keys/contosomhsmkey
```

Dove:
- **00000012-0000-0000-C000-000000000000** è il GUID da usare in questo comando
- **ContosoMHSM** è un nome di modulo di protezione hardware di esempio. Quando si esegue questo comando, sostituire questo valore con il proprio nome HSM.

Il ruolo utente di **crittografia HSM gestito** consente all'utente di decrittografare, firmare e ottenere le autorizzazioni per la chiave, che sono tutte necessarie per la funzionalità di HSM gestito. 

> [!NOTE]
> Mentre il modulo HSM gestito è in anteprima pubblica, la concessione del ruolo **utente di crittografia HSM gestita** è supportata solo tramite l'interfaccia della riga di comando di Azure.
> 

### <a name="configure-azure-information-protection-to-use-your-key"></a>Configurare Azure Information Protection per l'uso della chiave

Una volta completati tutti i passaggi precedenti, si è pronti per configurare Azure Information Protection per usare questa chiave come chiave del tenant dell'organizzazione.

Usando i cmdlet di Azure RMS, eseguire i comandi seguenti:

1. Connettersi al servizio Rights Management di Azure ed eseguire l'accesso:

    ```PowerShell
    Connect-AipService
    ```

1. Eseguire il [cmdlet Use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey), specificando l'URL della chiave. ad esempio:

    ```PowerShell
    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/<key-version>"
    ```

    > [!IMPORTANT]
    > In questo esempio `<key-version>` è la versione della chiave che si vuole usare. Se non si specifica la versione, per impostazione predefinita viene usata la versione corrente della chiave e il comando potrebbe sembrare funzionante. Tuttavia, se la chiave viene aggiornata o rinnovata in un secondo momento, il servizio Rights Management di Azure smetterà di funzionare per il tenant, anche se si esegue di nuovo il comando **use-AipServiceKeyVaultKey** .
    >
    > Usare il comando [Get-AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) in base alle esigenze per ottenere il numero di versione della chiave corrente.
    >
    > ad esempio `Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

    Per confermare che l'URL della chiave è impostato correttamente per Azure Information Protection, eseguire il comando [Get-AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) nella Azure Key Vault per visualizzare l'URL della chiave.

1. Se il servizio Azure Rights Management è già attivato, eseguire [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) per indicare Azure Information Protection per usare questa chiave come chiave del tenant attiva per il servizio Azure Rights Management.

Azure Information Protection è ora configurato per usare la chiave invece della chiave predefinita creata da Microsoft creata automaticamente per il tenant.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato la protezione BYOK, continuare [con la chiave radice del tenant](get-started-tenant-root-keys.md) per altre informazioni sull'uso e sulla gestione della chiave.