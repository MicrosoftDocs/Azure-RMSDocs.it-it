---
title: Dettagli BYOK-Azure Information Protection
description: Comprendere i dettagli e le restrizioni quando si usano chiavi gestite dal cliente (note come "Bring your own key" o BYOK) con Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d94783b491dd9ff0b099a68e009809cd7ec965fb
ms.sourcegitcommit: 479b3aaea7011750ff85a217298e5ae9185c1dd1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82224564"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>Dettagli di Bring your own key (BYOK) per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Le organizzazioni che dispongono di una sottoscrizione che include Azure Information Protection possono configurare il tenant Azure Information Protection per utilizzare una chiave gestita dal cliente e [registrarne l'utilizzo](log-analyze-usage.md). La configurazione della chiave gestita dal cliente è spesso definita "Bring your own key" o BYOK.

Questa chiave gestita dal cliente deve essere archiviata in Azure Key Vault, che richiede una sottoscrizione di Azure. Per usare una chiave protetta dal modulo di protezione hardware, è necessario che il livello di servizio di Azure Key Vault sia Premium. L'uso di una chiave in Insieme di credenziali delle chiavi di Azure comporta l'addebito di una tariffa mensile. Per ulteriori informazioni, vedere la [pagina relativa ai prezzi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

Quando si usa l'Insieme di credenziali delle chiavi di Azure per la chiave del tenant Azure Information Protection, è consigliabile usare un insieme di credenziali delle chiavi dedicato per questa chiave per garantire che venga usata solo dal servizio Azure Rights Management. Questa configurazione assicura che le chiamate da altri servizi non comportino il superamento dei [limiti del servizio](/azure/key-vault/key-vault-service-limits) per l'insieme di credenziali delle chiavi che potrebbe limitare i tempi di risposta per il servizio di Azure Rights Management.  

Inoltre, poiché ogni servizio che usa l'insieme di credenziali delle chiavi di Azure presenta in genere requisiti di gestione delle chiavi diversi, è consigliabile usare una sottoscrizione di Azure separata per questo insieme di credenziali delle chiavi per evitare errori di configurazione. 

Tuttavia, se si vuole condividere una sottoscrizione di Azure con altri servizi che usano l'insieme di credenziali delle chiavi di Azure, assicurarsi che la sottoscrizione condivida un set di amministratori comune. In questo modo gli amministratori che usano la sottoscrizione avranno una buona conoscenza di tutte le chiavi cui hanno accesso limitando la possibilità di configurazioni errate. 

Usare ad esempio una sottoscrizione di Azure condivisa se gli amministratori per la chiave del tenant di Azure Information Protection sono le stesse persone che amministrano le chiavi per la chiave cliente di Office 365 e CRM Online. 

In alternativa, se gli amministratori che gestiscono le chiavi per la chiave cliente o CRM online non sono le stesse persone che amministrano la chiave del tenant di Azure Information Protection, è consigliabile non condividere la sottoscrizione di Azure per Azure Information Protection.

## <a name="benefits-of-using-azure-key-vault"></a>Vantaggi dell'uso di Insieme di credenziali delle chiavi di Azure

Per una maggiore sicurezza, è possibile fare riferimento incrociato al Azure Information Protection la registrazione dell'utilizzo con [Azure Key Vault la registrazione](/azure/key-vault/key-vault-logging). I log Key Vault forniscono un metodo per monitorare in modo indipendente che solo il servizio Azure Rights Management usa la chiave. Se necessario, è possibile revocare immediatamente l'accesso alla chiave rimuovendo le autorizzazioni per l'insieme di credenziali delle chiavi.

Altri vantaggi dell'uso di Azure Key Vault per la chiave del tenant di Azure Information Protection includono:

- Insieme di credenziali delle chiavi di Azure offre una soluzione di gestione centralizzata delle chiavi coerente per molti servizi basati su cloud o persino locali che usano la crittografia.

- Insieme di credenziali delle chiavi di Azure supporta un numero di interfacce predefinite per la gestione delle chiavi, tra cui PowerShell, l'interfaccia della riga di comando, API REST e il portale di Azure. Altri servizi e strumenti sono stati integrati nell'insieme di credenziali delle chiavi per fornire funzionalità ottimizzate per attività specifiche, ad esempio il monitoraggio. Ad esempio, è possibile analizzare i log di utilizzo delle chiavi con Log Analytics da Operations Management Suite, impostare avvisi quando vengono soddisfatti determinati criteri e così via.

- Insieme di credenziali delle chiavi di Azure fornisce la separazione dei ruoli, una procedura di sicurezza consigliata di comprovata efficacia. Gli amministratori di Azure Information Protection possono concentrarsi sulla gestione della protezione e della classificazione dei dati, mentre gli amministratori di Insieme di credenziali delle chiavi di Azure possono concentrarsi sulla gestione delle chiavi di crittografia e dei criteri speciali che potrebbero essere necessari per la sicurezza o la conformità.

- Alcune organizzazioni hanno restrizioni relative alla posizione della chiave master. Insieme di credenziali delle chiavi di Azure fornisce un alto livello di controllo sull'archiviazione della chiave master perché il servizio è disponibile in molte aree di Azure. È possibile scegliere tra diverse aree di Azure ed è possibile che questo numero aumenti. Per altre informazioni, vedere la pagina [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/) nel sito di Azure.

Oltre alla gestione delle chiavi, Insieme di credenziali delle chiavi di Azure offre agli amministratori della protezione la stessa esperienza di gestione per archiviare, accedere e gestire i certificati e i segreti, ad esempio le password, per altri servizi e applicazioni che usano la crittografia. 

Per altre informazioni su Insieme di credenziali delle chiavi di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](/azure/key-vault/key-vault-whatis) e visitare il [blog del team di Insieme di credenziali delle chiavi di Azure](https://blogs.technet.microsoft.com/kv/) per le informazioni più recenti e per scoprire come viene usata questa tecnologia dagli altri servizi.

## <a name="byok-support-for-services-and-clients"></a>Supporto di BYOK per servizi e client

BYOK e la [registrazione dell'utilizzo](log-analyze-usage.md) interagiscono perfettamente con tutte le applicazioni che si integrano con il servizio Azure Rights Management usato da Azure Information Protection per proteggere i dati. ad esempio servizi cloud come SharePoint Online, server locali che eseguono Exchange e SharePoint che usano il servizio Azure Rights Management tramite il connettore RMS e applicazioni client come Office 2019, Office 2016 e Office 2013. 

È possibile ottenere i log di utilizzo delle chiavi, indipendentemente dall'applicazione che esegue richieste al servizio Rights Management di Azure.

## <a name="next-steps"></a>Passaggi successivi

Se si è deciso di gestire la propria chiave, vedere [Implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

Se si è deciso di usare la configurazione predefinita in cui Microsoft gestisce la chiave del tenant, vedere la sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps) dell'articolo Pianificazione e implementazione della chiave del tenant di Azure Information Protection.

