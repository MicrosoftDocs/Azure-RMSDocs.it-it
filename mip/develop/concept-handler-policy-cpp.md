---
title: Concetti - Gestori di criteri in MIP SDK.
description: Questo articolo illustra le modalità di creazione e uso dei gestori dell'API Criteri per la chiamata di operazioni.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: c1e150de6096e070f46232e77a4749081fe0bb9f
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297820"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft Information Protection SDK - Concetti relativi ai gestori di criteri

Nell'API Criteri `mip::PolicyHandler` espone le varie operazioni che possono essere usate per calcolare le azioni dei criteri e inviare gli eventi di controllo.

## <a name="policy-handler-functions"></a>Funzioni di gestione criteri

`mip::PolicyHandler` espone i metodi per la lettura, scrittura e rimozione sia delle etichette che delle informazioni sulla protezione. Per un elenco completo, vedere le [informazioni di riferimento sull'API](reference/class_mip_PolicyHandler.md).

In questo articolo verranno descritti i metodi seguenti:

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>Requisiti

La creazione di un elemento `PolicyHandler` richiede:

- Un elemento `PolicyProfile`
- Un elemento `PolicyEngine` aggiunto a `PolicyProfile`
- Una classe che eredita `mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>Creare un gestore di criteri

Il primo passaggio necessario per ottenere le azioni dei criteri consiste nella creazione di un oggetto `PolicyHandler`. Questa classe implementa la funzionalità necessaria per ottenere l'elenco di azioni che devono essere intraprese da una specifica etichetta e la funzione che consente di attivare un evento di controllo.

Per creare `PolicyHandler` è sufficiente chiamare la funzione `CreatePolicyHandlerAsync` di `PolicyEngine` usando il modello promise/future.

`CreatePolicyHandlerAsync` accetta un singolo parametro: **isAuditDiscoveryEnabled**. Impostare questo valore su **true** se si vuole che l'applicazione segnali gli eventi heartbeat nella registrazione di controllo.

> [!NOTE]
> La classe `mip::PolicyHandler::Observer` deve essere implementata in una classe derivata perché `CreatePolicyHandler` richiede l'oggetto `Observer`. 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

Dopo aver correttamente creato l'oggetto `PolicyHandler`, le azioni possono essere calcolate e gli eventi di controllo inviati.

# <a name="compute-an-action"></a>Calcolare un'azione

Come descritto in precedenza, le funzioni principali dell'API Criteri sono:

- Elencare le etichette disponibili.
- Restituire il set specifico di azioni da intraprendere, in base allo stato corrente e a quello desiderato. 

L'ultimo passaggio del processo consiste nello specificare un identificatore di etichetta e, facoltativamente, i metadati relativi all'etichetta esistente per la funzione `ComputeActions()`.

Il codice di esempio per questo articolo è reperibile in GitHub.

* [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>Calcolare un'azione per una nuova etichetta

Il calcolo di `mip::Actions` per una nuova etichetta può essere ottenuto usando l'elemento `ExecutionStateImpl` definito nella sezione [ExecutionState](concept-auditing-policy-executionstate-cpp.md).

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Set desired newLabelId in ExecutionStateOptions.
options.newLabelId = newLabelId;

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions.
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

Scrivendo solo l'elemento `mip::MetadataActions` restituito come parte di `actions` viene visualizzato:

```cpp
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled : true
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate : 2018-10-23T20:39:06-0800
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method : Standard
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name : Contoso FTEs (C)
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId : 2266fbe8-a0d9-44e8-bad8-00008f2a0915
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits : 3
```

L'elemento `PolicyHandler` calcola le azioni e restituisce un elemento `std::vector` di `mip::Action`. Spetta allo sviluppatore di applicazioni applicare i metadati al file o ai dati.

> [!NOTE]
> Nell'esempio precedente viene visualizzato solo l'output `mip::MetadataAction`. Per un esempio di visualizzazione di tipi di azioni aggiuntive, esaminare le aggregazioni di esempio con il [download dell'API Criteri](https://aka.ms/mipsdkbins).

## <a name="compute-actions-with-an-existing-label"></a>Calcolare azioni con un'etichetta esistente

Quando si usa l'API Criteri, spetta all'applicazione leggere i metadati dal contenuto. Questi metadati vengono offerti all'API come parte dell'elemento `mip::ExecutionState`. `ComputeActions()` può gestire operazioni più complesse dell'applicazione di una nuova etichetta a un documento senza etichetta. Nell'esempio seguente viene illustrato il downgrade di un'etichetta da un'etichetta più sensibile a un'etichetta meno sensibile, quando è già presente un'etichetta. Questo processo viene simulato tramite la lettura in una stringa di metadati delimitata da virgole e l'invio all'API tramite `mip::ExecutionState`.

> [!NOTE]
> L'esempio usa una funzione di utilità chiamata `SplitString()`. Per un esempio, vedere [qui](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-advanced/blob/master/mipsdk-policyapi-cpp-sample-advanced/utils.cpp)

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and set newLabelId.
sample::policy::ExecutionStateOptions options;
options.newLabelId = newLabelId;

// Split metadata string by commas, store in vector.
vector<string> metadataPairs = sample::utils::SplitString(metadata, ','); 

// Iterate through each string, splitting by the pipe.
// Add each key/value pair to ExecutionStateOptions metadata.
for (const string& metadataPair : metadataPairs) {
    vector<string> keyValue = sample::utils::SplitString(metadataPair, '|');
    options.metadata[keyValue[0]] = keyValue[1];
}

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

L'esempio precedente può generare diverse azioni. Queste azioni dipendono dalle etichette specificate come input e dalla configurazione etichetta. Come minimo, il risultato sarà un unico elemento `mip::MetadataAction` contenente i dati da rimuovere tramite `GetMetadataToRemove()` e i dati da aggiungere tramite `GetMetadataToAdd()`.

```
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Enabled : true
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SetDate : 2018-10-23T23:59:41-0800
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Method : Standard
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Name : General
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ActionId : 447a996b-28ea-482c-b0b5-000075bd4bb3
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ContentBits : 7
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId
```

## <a name="next-steps"></a>Passaggi successivi

* Scaricare quindi gli [esempi dell'API Criteri da GitHub e provare l'API Criteri](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
* Leggere informazioni su come [passare gli eventi di controllo alla funzionalità di analisi di Azure Information Protection](concept-auditing-policy-cpp.md)