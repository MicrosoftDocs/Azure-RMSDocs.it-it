---
title: Pianificazione e implementazione della chiave del tenant di Azure Rights Management | Azure Information Protection
description: "Informazioni per pianificare e gestire la chiave del tenant di Azure Information Protection. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita), per rispettare specifici criteri dell&quot;organizzazione può essere necessario gestire autonomamente la propria chiave del tenant. in base alla modalità BYOK (Bring Your Own Key)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 433a655870556ed045273713f6773f36c3d86fc1


---

# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Pianificazione e implementazione della chiave del tenant di Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Usare le informazioni presenti in questo articolo per pianificare e gestire la chiave del tenant di Azure Information Protection. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita), per rispettare i criteri aziendali potrebbe essere necessario, ad esempio, gestire autonomamente la propria chiave del tenant in base alla modalità BYOK (Bring Your Own Key).

> [!NOTE]
> L'equivalente locale della chiave del tenant di Azure Information Protection è noto come chiave del certificato concessore di licenze server (SLC). Azure Information Protection gestisce una o più chiavi per ogni organizzazione che ha una sottoscrizione di Azure Information Protection. Tutte le volte che in un'organizzazione si usa una chiave per Azure Information Protection, ad esempio chiavi utente, chiavi computer o chiavi di crittografia documenti, la chiave si concatena a livello di crittografia alla chiave del tenant di Azure Information Protection dell'utente.

**Panoramica:** Usare la tabella seguente come guida rapida per la topologia consigliata delle chiavi del tenant. Per altre informazioni, vedere quindi la documentazione aggiuntiva.

Se si distribuisce Azure Information Protection con una chiave del tenant gestita da Microsoft, sarà possibile passare alla modalità BYOK in un secondo momento. Non è tuttavia attualmente possibile passare dalla modalità BYOK alla gestione da parte di Microsoft per la chiave del tenant di Azure Information Protection.

|Requisito aziendale|Topologia di chiave del tenant consigliata|
|------------------------|-----------------------------------|
|Distribuire Azure Information Protection rapidamente e senza ricorrere a hardware speciale|Gestita da Microsoft|
|Ottenere la funzionalità IRM completa in Exchange Online con il servizio Azure Rights Management|Gestita da Microsoft|
|Le chiavi vengono create dall'utente e protette in un modulo di protezione hardware|BYOK<br /><br />Questa configurazione darà attualmente come risultato una funzionalità IRM ridotta in Exchange Online. Per altre informazioni, vedere [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).|

## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>Scegliere la topologia di chiave del tenant: gestione di Microsoft (impostazione predefinita) o BYOK
È innanzitutto necessario decidere la topologia di chiave del tenant più adatta per l'organizzazione. Per impostazione predefinita, Azure Information Protection genera la chiave del tenant e gestisce la maggior parte degli aspetti del relativo ciclo di vita. Questa opzione è quella più semplice e prevede il sovraccarico amministrativo minore. Nella maggior parte dei casi non è nemmeno necessario disporre di una chiave del tenant, ma è sufficiente iscriversi ad Azure Information Protection e la parte rimanente del processo di gestione delle chiavi viene eseguita da Microsoft.

In alternativa, è possibile esercitare il controllo completo sulla chiave del tenant tramite [Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/services/key-vault/). Questo scenario implica la creazione della chiave del tenant e la conservazione della copia master in locale. Questo scenario viene spesso definito con il termine modalità BYOK e prevede lo schema seguente.

1.  Generazione della chiave del tenant in locale, in base ai criteri IT e ai criteri di sicurezza dell'organizzazione.

2.  Trasferimento sicuro della chiave del tenant da un modulo di protezione hardware di proprietà dell'utente a moduli di protezioni hardware di proprietà e gestiti da Microsoft tramite Insieme di credenziali delle chiavi di Azure. Grazie a questo processo, la chiave del tenant non oltrepassa mai i confini dell'ambiente hardware protetto.

3.  Quando si trasferisce la chiave del tenant a Microsoft, la protezione viene assicurata da Insieme di credenziali delle chiavi di Azure.

Anche se facoltativo, può essere utile usare i log di utilizzo di Azure Information Protection disponibili in tempo quasi reale per sapere esattamente come e quando viene usata la chiave del tenant.

> [!NOTE]
> Come misura di protezione aggiuntiva, Insieme di credenziali delle chiavi di Azure usa domini di sicurezza separati per i propri data center in aree quali America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, nonché nelle diverse istanze di Azure, ad esempio Microsoft Azure Germania e Azure per enti pubblici. Quando si gestisce la propria chiave del tenant, quest'ultima è associata al dominio di sicurezza della regione o dell'istanza in cui è registrato il tenant di Azure Information Protection. Una chiave del tenant di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.

## <a name="the-tenant-key-lifecycle"></a>Ciclo di vita della chiave del tenant
Se si decide di affidare a Microsoft la gestione della chiave del tenant, Microsoft gestisce la maggior parte delle operazioni del ciclo di vita della chiave. Se invece l'utente decide di gestire in modo autonomo la propria chiave del tenant, è responsabile di molte operazioni del ciclo di vita della chiave e di alcune procedure aggiuntive in Insieme di credenziali delle chiavi di Azure.

Nei diagrammi seguenti vengono illustrate e confrontate le due opzioni. Nel primo diagramma viene illustrato il minor sovraccarico amministrativo che l'utente deve sostenere nella configurazione predefinita quando Microsoft gestisce la chiave del tenant.

![Ciclo di vita della chiave del tenant di Azure Information Protection: chiave gestita da Microsoft, impostazione predefinita](../media/RMS_BYOK_cloud.png)

Nel secondo diagramma vengono illustrati i passaggi aggiuntivi necessari quando l'utente gestisce la propria chiave del tenant.

![Ciclo di vita della chiave del tenant di Azure Information Protection: chiave gestita dall'utente, BYOK](../media/RMS_BYOK_onprem4.png)

Se si decide di affidare a Microsoft la gestione della chiave del tenant, non è necessaria alcuna azione aggiuntiva per generare la chiave ed è possibile passare direttamente alla sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps).  

Se invece si decide di gestire in modo autonomo la propria chiave del tenant, leggere le sezioni seguenti per ottenere altre informazioni.

## <a name="implementing-your-azure-information-protection-tenant-key"></a>Implementazione della chiave del tenant di Azure Information Protection

Usare le informazioni e le procedure descritte in questa sezione se si è deciso di generare e gestire la propria chiave del tenant in base allo schema BYOK.


> [!IMPORTANT]
> Se si è iniziato a usare Azure Information Protection con una chiave del tenant gestita da Microsoft e si vuole gestire la chiave del tenant autonomamente (passare alla modalità BYOK), i documenti e i messaggi di posta elettronica precedentemente protetti saranno comunque accessibili tramite una chiave archiviata. Tuttavia, se sono presenti utenti che eseguono Office 2010, [contattare il supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) prima di eseguire queste procedure. Questi computer necessiteranno di alcuni passaggi di configurazione aggiuntivi.
> 
> [Contattare il supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) anche quando l'organizzazione prevede criteri specifici per la gestione delle chiavi.

### <a name="prerequisites-for-byok"></a>Prerequisiti per la modalità BYOK
Nella tabella seguente sono elencati i prerequisiti per la modalità BYOK.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una sottoscrizione che supporta Azure Information Protection.|Per altre informazioni sulle sottoscrizioni disponibili, vedere la [pagina dei piani tariffari](https://go.microsoft.com/fwlink/?LinkId=827589) di Azure Information Protection.|
|Non si usa RMS per singoli utenti o per Exchange Online. Se si usa Exchange Online, si conoscono e si accettano le limitazioni relative all'uso della modalità BYOK con questa configurazione.|Per altre informazioni sulle restrizioni per la modalità BYOK e sulle limitazioni attuali, vedere [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).<br /><br />**Importante**: attualmente, la modalità BYOK non è compatibile con Exchange Online.|
|Tutti i prerequisiti elencati per la modalità BYOK nell'insieme di credenziali delle chiavi, inclusa una sottoscrizione di Azure a pagamento o di valutazione. |Vedere [Prerequisiti per la modalità BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok) nella documentazione relativa ad Insieme di credenziali delle chiavi di Azure. <br /><br /> La sottoscrizione gratuita di Azure, che fornisce l'accesso per configurare Azure Active Directory e i modelli personalizzati di Azure Rights Management (**Accesso ad Azure Active Directory**), non è sufficiente per usare Insieme di credenziali delle chiavi di Azure. Per verificare se la propria sottoscrizione di Azure può essere utilizzata per la modalità BYOK, usare i cmdlet di PowerShell per [Azure Resource Manager](https://msdn.microsoft.com/library/azure/mt786812\(v=azure.300\).aspx): <br /><br /> 1. Avviare una sessione di Azure PowerShell e accedere al proprio account Azure con il comando seguente: `Login-AzureRmAccount`<br /><br />2. Digitare il comando seguente e verificare che siano visualizzati valori per il nome e l'ID della sottoscrizione e per l'ID del tenant e che lo stato sia attivato: `Get-AzureRmSubscription`<br /><br />Se non viene visualizzato alcun valore e viene semplicemente restituito il prompt, non si dispone di una sottoscrizione di Azure che può essere usata per la modalità BYOK. <br /><br />**Nota**: oltre ai prerequisiti per la modalità BYOK, se si esegue la migrazione da AD RMS ad Azure Information Protection passando da una chiave software a una chiave hardware, sarà necessaria almeno la versione 11.62 del firmware Thales.|
|Il modulo di amministrazione di Azure Rights Management per Windows PowerShell.|Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md). <br /><br />Se il modulo Windows PowerShell è stato installato in precedenza, eseguire il comando seguente per verificare che il numero della versione in uso sia almeno **2.5.0.0**: `(Get-Module aadrm -ListAvailable).Version`|

Per altre informazioni sui moduli di protezione hardware Thales e su come vengono usati con Insieme di credenziali delle chiavi di Azure, vedere il [sito Web Thales](https://www.thales-esecurity.com/msrms/cloud).

### <a name="instructions-for-byok"></a>Istruzioni per BYOK

Per generare e trasferire la propria chiave del tenant in Insieme di credenziali delle chiavi di Azure, seguire le procedure descritte in [Come generare e trasferire chiavi HSM protette per l'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/) dalla documentazione di Insieme di credenziali delle chiavi di Azure.

Quando la chiave viene trasferita all'insieme di credenziali delle chiavi, le viene assegnato un ID, ovvero un URL contenente il nome dell'insieme di credenziali delle chiavi, il contenitore delle chiavi, il nome della chiave e la versione della chiave. Ad esempio: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. È necessario indicare al servizio Azure Rights Management di Azure Information Protection di usare questa chiave, specificando l'URL.

Affinché Azure Information Protection possa usare la chiave, il servizio Azure Rights Management deve essere prima autorizzato a usare la chiave nell'insieme di credenziali delle chiavi dell'organizzazione. A tale scopo, l'amministratore dell'insieme di credenziali delle chiavi di Azure usa il cmdlet di PowerShell appropriato [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/en-us/library/mt603625(v=azure.300\).aspx) e concede le autorizzazioni all'entità servizio Azure Rights Management usando il GUID 00000012-0000-0000-c000-000000000000. Ad esempio:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

A questo punto è possibile configurare Azure Information Protection per l'uso di questa chiave come chiave del tenant di Azure Information Protection dell'organizzazione. Tramite i cmdlet di Azure RMS, connettersi al servizio Azure Rights Management e accedere:

    Connect-AadrmService

Successivamente, è necessario eseguire il cmdlet [Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx), specificando l'URL della chiave. Ad esempio:

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> In questo esempio, "aaaabbbbcccc111122223333" è la versione della chiave da usare. Se non si specifica la versione, viene usata la versione corrente della chiave senza avviso e il comando sembra funzionare. Tuttavia, se la chiave nell'insieme di credenziali delle chiavi viene aggiornata in un secondo momento (rinnovo), il servizio Azure Rights Management smetterà di funzionare per il tenant, anche se si esegue nuovamente il comando Use-AadrmKeyVaultKey.
>
>Assicurarsi di specificare la versione e il nome della chiave quando si esegue questo comando. È possibile usare il comando [Get-AzureKeyVaultKey](https://docs.microsoft.com/powershell/resourcemanager/azurerm.keyvault\/v2.3.0\/get-azurekeyvaultkey) dell'insieme di credenziali delle chiavi di Azure per ottenere il numero di versione della chiave corrente. Ad esempio: `Get-AzureKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

Se è necessario verificare che l'URL della chiave sia impostato correttamente nel servizio Azure RMS, è possibile eseguire [Get-AzureKeyVaultKey](https://msdn.microsoft.com/en-us/library/dn868053(v=azure.300\).aspx) nell'insieme di credenziali delle chiavi di Azure per visualizzare l'URL della chiave.


## <a name="next-steps"></a>Passaggi successivi

Dopo la pianificazione e, se necessario, la generazione della chiave del tenant, effettuare le operazioni seguenti:

1.  Iniziare a usare la chiave del tenant.

    -   Se non è ancora stato fatto, è ora necessario attivare il servizio Rights Management in modo che l'organizzazione possa iniziare a usare Azure Information Protection. In questo caso, gli utenti iniziano immediatamente a usare la chiave del tenant (gestita da Microsoft o gestita in modo autonomo in Insieme di credenziali delle chiavi di Azure).

        Per altre informazioni, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

    -   Se il servizio Rights Management è già stato attivato e si è deciso di gestire la propria chiave del tenant, gli utenti passano gradualmente dalla chiave del tenant precedente a quella nuova e il completamento di questa transizione in fasi successive può richiedere alcune settimane. I documenti e i file protetti con la chiave del tenant precedente rimangono accessibili agli utenti autorizzati.

2.  Valutare l'opportunità di usare la registrazione dei dati di utilizzo per tenere traccia di ogni transazione eseguita dal servizio Azure Rights Management.

    Se si è deciso di gestire la propria chiave del tenant, la registrazione include informazioni sull'uso della chiave stessa. Vedere il frammento seguente di un file di log visualizzato in Excel in cui i tipi di richiesta **KeyVaultDecryptRequest** e **KeyVaultSignRequest** dimostrano che la chiave del tenant è attualmente in uso.

    ![file di log visualizzato in Excel in cui è attualmente usata la chiave del tenant](../media/RMS_Logging.png)

    Per altre informazioni sulla registrazione dell'utilizzo, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Gestire la propria chiave del tenant.

    Per altre informazioni, vedere [Operazioni relative alla chiave del tenant di Azure Rights Management](../deploy-use/operations-tenant-key.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


