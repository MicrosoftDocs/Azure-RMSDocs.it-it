---
title: Prezzi e restrizioni della modalità BYOK - Azure Information Protection
description: Informazioni sulle restrizioni quando si usano chiavi gestite dal cliente ("bring your own key" o BYOK) con Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/18/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c40e1b628c4a6160d6ab665293c37b9cefa3fe0c
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39375253"
---
# <a name="byok-pricing-and-restrictions"></a>Prezzi e restrizioni della modalità BYOK

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Le organizzazioni che hanno una sottoscrizione che include Azure Information Protection possono configurare il tenant di Azure Information Protection per usare una chiave gestita dal cliente (BYOK) e [registrarne l'utilizzo](../deploy-use/log-analyze-usage.md). 

La chiave deve essere archiviata in Azure Key Vault per il quale è necessaria una sottoscrizione di Azure. Per usare una chiave protetta dal modulo di protezione hardware, è necessario che il livello di servizio di Azure Key Vault sia Premium. L'uso di una chiave in Insieme di credenziali delle chiavi di Azure comporta l'addebito di una tariffa mensile. Per altre informazioni, vedere la [pagina dei prezzi di Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

Quando si usa l'Insieme di credenziali delle chiavi di Azure per la chiave del tenant Azure Information Protection, è consigliabile usare un insieme di credenziali delle chiavi dedicato per questa chiave per garantire che venga usata solo dal servizio Azure Rights Management. Questa configurazione assicura che le chiamate da altri servizi non comportino il superamento dei [limiti del servizio](/azure/key-vault/key-vault-service-limits) per l'insieme di credenziali delle chiavi che potrebbe limitare i tempi di risposta per il servizio di Azure Rights Management.  

Inoltre, poiché ogni servizio che usa l'insieme di credenziali delle chiavi di Azure presenta in genere requisiti di gestione delle chiavi diversi, è consigliabile usare una sottoscrizione di Azure separata per questo insieme di credenziali delle chiavi per evitare errori di configurazione. 

Tuttavia, se si vuole condividere una sottoscrizione di Azure con altri servizi che usano l'insieme di credenziali delle chiavi di Azure, assicurarsi che la sottoscrizione condivida un set di amministratori comune. In questo modo gli amministratori che usano la sottoscrizione avranno una buona conoscenza di tutte le chiavi cui hanno accesso limitando la possibilità di configurazioni errate. Usare ad esempio una sottoscrizione di Azure condivisa se gli amministratori per la chiave del tenant di Azure Information Protection sono le stesse persone che amministrano le chiavi per la chiave cliente di Office 365 e CRM Online. Se invece gli amministratori che gestiscono le chiavi per la chiave cliente o CRM Online non sono le stesse persone che amministrano la chiave del tenant di Azure Information Protection, è consigliabile non condividere la sottoscrizione di Azure per Azure Information Protection.

## <a name="benefits-of-using-azure-key-vault"></a>Vantaggi dell'uso di Insieme di credenziali delle chiavi di Azure

Oltre alla funzionalità di registrazione dell'utilizzo di Azure Information Protection, per una maggiore sicurezza è possibile creare riferimenti incrociati con la [registrazione di Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-logging/) per controllare in modo indipendente se la chiave viene usata solo dal servizio Azure Rights Management. Se necessario, è possibile revocare immediatamente l'accesso alla chiave rimuovendo le autorizzazioni per l'insieme di credenziali delle chiavi.

Altri vantaggi dell'uso di Insieme di credenziali delle chiavi di Azure per la chiave del tenant Azure Information Protection:

- Insieme di credenziali delle chiavi di Azure offre una soluzione di gestione centralizzata delle chiavi coerente per molti servizi basati su cloud o persino locali che usano la crittografia.

- Insieme di credenziali delle chiavi di Azure supporta un numero di interfacce predefinite per la gestione delle chiavi, tra cui PowerShell, l'interfaccia della riga di comando, API REST e il portale di Azure. Altri servizi e strumenti sono stati integrati nell'insieme di credenziali delle chiavi per fornire funzionalità ottimizzate per attività specifiche, ad esempio il monitoraggio. Ad esempio, è possibile analizzare i log di utilizzo delle chiavi con Log Analytics da Operations Management Suite, impostare avvisi quando vengono soddisfatti determinati criteri e così via.

- Insieme di credenziali delle chiavi di Azure fornisce la separazione dei ruoli, una procedura di sicurezza consigliata di comprovata efficacia. Gli amministratori di Azure Information Protection possono concentrarsi sulla gestione della protezione e della classificazione dei dati, mentre gli amministratori di Insieme di credenziali delle chiavi di Azure possono concentrarsi sulla gestione delle chiavi di crittografia e dei criteri speciali che potrebbero essere necessari per la sicurezza o la conformità.

- Alcune organizzazioni hanno restrizioni relative alla posizione della chiave master. Insieme di credenziali delle chiavi di Azure fornisce un alto livello di controllo sull'archiviazione della chiave master perché il servizio è disponibile in molte aree di Azure. Attualmente, è possibile scegliere tra 28 aree di Azure e si prevede di aumentare questo numero. Per altre informazioni, vedere la pagina [Prodotti disponibili in base all'area] (https://azure.microsoft.com/regions/services/) nel sito di Azure.

Oltre alla gestione delle chiavi, Insieme di credenziali delle chiavi di Azure offre agli amministratori della protezione la stessa esperienza di gestione per archiviare, accedere e gestire i certificati e i segreti, ad esempio le password, per altri servizi e applicazioni che usano la crittografia. 

Per altre informazioni su Insieme di credenziali delle chiavi di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](/azure/key-vault/key-vault-whatis) e visitare il [blog del team di Insieme di credenziali delle chiavi di Azure](https://cloudblogs.microsoft.com/kv/) per le informazioni più recenti e per scoprire come viene usata questa tecnologia dagli altri servizi.

## <a name="restrictions-when-using-byok"></a>Restrizioni per l'uso di BYOK

Il servizio BYOK e la registrazione dell'utilizzo possono essere usati facilmente con ogni applicazione che si integra con il servizio Azure Rights Management usato da Azure Information Protection, ad esempio servizi cloud come SharePoint Online, server locali che eseguono Exchange e SharePoint che usano il servizio Azure Rights Management tramite il connettore RMS e applicazioni client come Office 2016 e Office 2013. È possibile ottenere i log di utilizzo delle chiavi indipendentemente dall'applicazione che invia richieste al servizio Azure Rights Management.

Se IRM di Exchange Online è stato precedentemente abilitato importando il dominio di pubblicazione trusted (TPD) da Azure RMS, seguire le istruzioni in [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Impostare le nuove funzionalità di Office 365 Message Encryption basate su Azure Information Protection) per abilitare le nuove funzionalità di Exchange Online che supportano l'uso di BYOK per Azure Information Protection.

## <a name="next-steps"></a>Passaggi successivi

Se si è deciso di gestire la propria chiave, vedere [Implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

Se si è deciso di usare la configurazione predefinita in cui Microsoft gestisce la chiave del tenant, vedere la sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps) dell'articolo Pianificazione e implementazione della chiave del tenant di Azure Information Protection.

