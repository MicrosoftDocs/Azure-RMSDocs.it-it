---
title: Pianificazione e implementazione della chiave del tenant di Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a80866576dc7d6400bcebc2fc1c37bc0367bcdf3
ms.openlocfilehash: ee7b9b5f251856f102651f1e8f379f7bbacea77e


---

# Pianificazione e implementazione della chiave del tenant di Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

In questo argomento sono contenute informazioni per pianificare e gestire la chiave del tenant RMS (Rights Management Service) per Azure RMS. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita), per rispettare i criteri aziendali potrebbe essere necessario, ad esempio, gestire autonomamente la propria chiave del tenant  in base alla modalità BYOK (Bring Your Own Key).

> [!NOTE]
> La chiave del tenant RMS è nota anche come certificato concessore di licenze server (SLC, Server Licensor Certificate). Azure RMS gestisce una o più chiavi per ogni organizzazione che effettua una sottoscrizione a Azure RMS. Tutte le volte che in un'organizzazione si usa una chiave per RMS, ad esempio chiavi utente, chiavi computer o chiavi di crittografia documenti, la chiave si concatena a livello di crittografia alla chiave del tenant RMS dell'utente.

**Panoramica:** Usare la tabella seguente come guida rapida per la topologia consigliata delle chiavi del tenant. Per altre informazioni, vedere quindi la documentazione aggiuntiva.

Se si distribuisce Azure RMS con una chiave del tenant gestita da Microsoft, sarà possibile passare alla modalità BYOK in un secondo momento. Non è tuttavia attualmente possibile passare dalla modalità BYOK alla gestione da parte di Microsoft per la chiave del tenant di Azure RMS.

|Requisito aziendale|Topologia di chiave del tenant consigliata|
|------------------------|-----------------------------------|
|Distribuire Azure RMS rapidamente e senza che sia necessario hardware speciale|Gestita da Microsoft|
|Necessità di ottenere la funzionalità IRM completa in Exchange Online con Azure RMS|Gestita da Microsoft|
|Le chiavi vengono create dall'utente e protette in un modulo di protezione hardware|BYOK<br /><br />Questa configurazione darà attualmente come risultato una funzionalità IRM ridotta in Exchange Online. Per altre informazioni, vedere [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).|

## Scegliere la topologia di chiave del tenant: gestione di Microsoft (impostazione predefinita) o BYOK
È innanzitutto necessario decidere la topologia di chiave del tenant più adatta per l'organizzazione. Per impostazione predefinita, Azure RMS genera la chiave del tenant e gestisce la maggior parte degli aspetti del relativo ciclo di vita. Questa opzione è quella più semplice e prevede il sovraccarico amministrativo minore. Nella maggior parte dei casi non è nemmeno necessario disporre di una chiave del tenant, ma è sufficiente iscriversi ad Azure RMS e la parte rimanente del processo di gestione delle chiavi viene eseguita da Microsoft.

In alternativa, è possibile esercitare il controllo completo sulla chiave del tenant tramite [Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/services/key-vault/). Questo scenario implica la creazione della chiave del tenant e la conservazione della copia master in locale. Questo scenario viene spesso definito con il termine modalità BYOK e prevede lo schema seguente.

1.  Generazione della chiave del tenant in locale, in base ai criteri IT e ai criteri di sicurezza dell'organizzazione.

2.  Trasferimento sicuro della chiave del tenant da un modulo di protezione hardware di proprietà dell'utente a moduli di protezioni hardware di proprietà e gestiti da Microsoft tramite Insieme di credenziali delle chiavi di Azure. Grazie a questo processo, la chiave del tenant non oltrepassa mai i confini dell'ambiente hardware protetto.

3.  Quando si trasferisce la chiave del tenant a Microsoft, la protezione viene assicurata da Insieme di credenziali delle chiavi di Azure.

Anche se è facoltativo, i log di utilizzo di Azure RMS disponibili in tempo quasi reale sono utili per sapere esattamente come e quando viene usata la chiave del tenant.

> [!NOTE]
> Come misura di protezione aggiuntiva, Insieme di credenziali delle chiavi di Azure usa domini di sicurezza separati per i propri data center in aree quali America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, nonché nelle diverse istanze di Azure, ad esempio Microsoft Azure Germania e Azure per enti pubblici. Quando si gestisce la propria chiave del tenant, quest'ultima è associata al dominio di sicurezza della regione o dell'istanza in cui è registrato il tenant RMS. Una chiave del tenant di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.

## Ciclo di vita della chiave del tenant
Se si decide di affidare a Microsoft la gestione della chiave del tenant, Microsoft gestisce la maggior parte delle operazioni del ciclo di vita della chiave. Se invece l'utente decide di gestire in modo autonomo la propria chiave del tenant, è responsabile di molte operazioni del ciclo di vita della chiave e di alcune procedure aggiuntive in Insieme di credenziali delle chiavi di Azure.

Nei diagrammi seguenti vengono illustrate e confrontate le due opzioni. Nel primo diagramma viene illustrato il minor sovraccarico amministrativo che l'utente deve sostenere nella configurazione predefinita quando Microsoft gestisce la chiave del tenant.

![Ciclo di vita della chiave del tenant di Azure RMS: chiave gestita da Microsoft, impostazione predefinita](../media/RMS_BYOK_cloud.png)

Nel secondo diagramma vengono illustrati i passaggi aggiuntivi necessari quando l'utente gestisce la propria chiave del tenant.

![Ciclo di vita della chiave del tenant di Azure RMS: chiave gestita dall'utente, BYOK](../media/RMS_BYOK_onprem4.png)

Se si decide di affidare a Microsoft la gestione della chiave del tenant, non è necessaria alcuna azione aggiuntiva per generare la chiave ed è possibile passare direttamente alla sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps).

Se invece si decide di gestire in modo autonomo la propria chiave del tenant, leggere le sezioni seguenti per ottenere altre informazioni.

## Implementazione della chiave del tenant di Azure Rights Management

Usare le informazioni e le procedure descritte in questa sezione se si è deciso di generare e gestire la propria chiave del tenant in base allo schema BYOK.


> [!IMPORTANT]
> Se si è già iniziato a usare [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (il servizio è attivo) e sono presenti utenti che eseguono Office 2010, [contattare il supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) prima di eseguire queste procedure. A seconda dello scenario e dei requisiti, è comunque possibile usare la modalità BYOK con alcune limitazioni o con passaggi aggiuntivi.
> 
> [Contattare il supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) anche quando l'organizzazione prevede criteri specifici per la gestione delle chiavi.

### Prerequisiti per la modalità BYOK
Nella tabella seguente sono elencati i prerequisiti per la modalità BYOK.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Sottoscrizione che supporta Azure RMS.|Per altre informazioni sulle sottoscrizioni disponibili, vedere [Sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md).|
|Non si usa RMS per singoli utenti o per Exchange Online. Se si usa Exchange Online, si conoscono e si accettano le limitazioni relative all'uso della modalità BYOK con questa configurazione.|Per altre informazioni sulle restrizioni per la modalità BYOK e sulle limitazioni attuali, vedere [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).<br /><br />**Importante**: attualmente, la modalità BYOK non è compatibile con Exchange Online.|
|Tutti i prerequisiti elencati per la modalità BYOK nell'insieme di credenziali delle chiavi.|Vedere [Prerequisiti per la modalità BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok) dalla documentazione di Insieme di credenziali delle chiavi di Azure. <br /><br />**Nota**: se si esegue la migrazione da AD RMS ad Azure RMS, passando da una chiave software a una chiave hardware, sarà necessaria almeno la versione 11.62 del firmware Thales.|
|Il modulo di amministrazione di Azure RMS per Windows PowerShell.|Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md). <br /><br />Se il modulo Windows PowerShell è stato installato in precedenza, eseguire il comando seguente per verificare che il numero di versione in uso sia almeno **2.5.0.0**: `(Get-Module aadrm -ListAvailable).Version`|

Per altre informazioni sui moduli di protezione hardware Thales e su come vengono usati con Insieme di credenziali delle chiavi di Azure, vedere il [sito Web Thales](https://www.thales-esecurity.com/msrms/cloud).

Per generare e trasferire la propria chiave del tenant in Insieme di credenziali delle chiavi di Azure, seguire le procedure descritte in [Come generare e trasferire chiavi HSM protette per l'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/) dalla documentazione di Insieme di credenziali delle chiavi di Azure.

Quando la chiave viene trasferita all'insieme di credenziali delle chiavi, le viene assegnato un ID, ovvero un URL contenente il nome dell'insieme di credenziali, il contenitore delle chiavi, il nome della chiave e la versione della chiave. Ad esempio: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. È necessario indicare ad Azure RMS di usare questa chiave, specificando l'URL.

Ma prima che Azure RMS possa usare la chiave, deve essere autorizzato all'uso della chiave nell'insieme di credenziali delle chiavi dell'organizzazione. A tale scopo, l'amministratore di Insieme di credenziali delle chiavi di Azure usa il cmdlet PowerShell dell'insieme di credenziali delle chiavi, [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx) e concede le autorizzazioni all'entità di servizio **Microsoft.Azure.RMS** di Azure RMS. Ad esempio:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign 

A questo punto è possibile configurare Azure RMS per l'uso di questa chiave come chiave del tenant di Azure RMS dell'organizzazione. Tramite i cmdlet di Azure RMS, è innanzitutto possibile la connessione e l'accesso ad Azure RMS:

    Connect-AadrmService

Successivamente, è necessario eseguire il cmdlet [Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx), specificando l'URL della chiave. Ad esempio:

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

Se è necessario confermare che l'URL della chiave viene impostato correttamente in Azure RMS, in Insieme di credenziali delle chiavi di Azure è possibile eseguire [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) per visualizzare l'URL della chiave.


## Passaggi successivi

Dopo la pianificazione e, se necessario, la generazione della chiave del tenant, effettuare le operazioni seguenti:

1.  Iniziare a usare la chiave del tenant.

    -   Se non è ancora stato fatto, è ora necessario attivare Rights Management in modo che l'organizzazione possa iniziare a usare RMS. In questo caso, gli utenti iniziano immediatamente a usare la chiave del tenant (gestita da Microsoft o gestita in modo autonomo in Insieme di credenziali delle chiavi di Azure).

        Per altre informazioni, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

    -   Se Rights Management è già stato attivato e si è deciso di gestire la propria chiave del tenant, gli utenti passano gradualmente dalla chiave del tenant precedente a quella nuova e questa transizione in fasi successive può richiedere alcune settimane per essere completata. I documenti e i file protetti con la chiave del tenant precedente rimangono accessibili agli utenti autorizzati.

2.  Valutare l'opportunità di usare la registrazione dei dati di utilizzo per tenere traccia di ogni transazione eseguita da Azure Rights Management.

    Se si è deciso di gestire la propria chiave del tenant, la registrazione include informazioni sull'uso della chiave stessa. Vedere il frammento seguente di un file di log visualizzato in Excel in cui i tipi di richiesta **KeyVaultDecryptRequest** e **KeyVaultSignRequest** dimostrano che la chiave del tenant è attualmente in uso.

    ![file di log visualizzato in Excel in cui è attualmente usata la chiave del tenant](../media/RMS_Logging.png)

    Per ulteriori informazioni sulla registrazione dei dati di utilizzo, vedere [Registrazione e analisi dell'utilizzo di Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Gestire la propria chiave del tenant.

    Per altre informazioni, vedere [Operazioni relative alla chiave del tenant di Azure Rights Management](../deploy-use/operations-tenant-key.md).




<!--HONumber=Aug16_HO3-->


