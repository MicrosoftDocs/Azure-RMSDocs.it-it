---
title: 'Concetti: uso di Microsoft Information Protection per generare eventi di controllo'
description: Questo articolo consente di comprendere come usare Microsoft Information Protection SDK per il calcolo.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 6bf4bc78d6008354275abacddf8f37e42dce1650
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555790"
---
# <a name="compute-an-action"></a>Calcolare un'azione

Come descritto in precedenza, le funzioni principali dell'API Criteri sono:

- elencare le etichette disponibili
- Restituisce un set di azioni da intraprendere in base allo stato corrente e desiderato

L'ultimo passaggio del processo consiste nello specificare un identificatore di etichetta e, facoltativamente, i metadati relativi all'etichetta esistente per la funzione `ComputeActions()`.

Il codice di esempio per questo articolo è reperibile in GitHub.

- [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>Calcolare un'azione per una nuova etichetta

Il calcolo di `mip::Actions` per una nuova etichetta può essere eseguito usando il `ExecutionStateImpl` definito in  [ExecutionState](concept-handler-policy-executionstate-cpp.md).

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Resolve desired label id to mip::Label and set in ExecutionStateOptions.
options.newLabel = mEngine->GetLabelById(newLabelId);

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

Quando si usa l'API dei criteri, l'applicazione deve leggere i metadati dal contenuto. Questi metadati vengono offerti all'API come parte dell'elemento `mip::ExecutionState`. `ComputeActions()` può gestire operazioni più complesse dell'applicazione di una nuova etichetta a un documento senza etichetta. Nell'esempio seguente viene illustrato il downgrade di un'etichetta da un'etichetta più sensibile, a un'etichetta meno sensibile. Questo processo viene simulato leggendo una stringa di metadati con valori delimitati da virgole e fornendo all'API tramite `mip::ExecutionState`.

> [!NOTE]
> L'esempio usa una funzione di utilità chiamata `SplitString()`. Per un esempio, vedere [qui](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/utils.cpp)

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and resolve newLabelId to mip::Label
sample::policy::ExecutionStateOptions options;
options.newLabel = mEngine->GetLabelById(newLabelId);

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

L'esempio precedente può generare diverse azioni. Queste azioni dipendono dalle etichette specificate come input e dalla configurazione etichetta. Come minimo, il risultato sarà un unico elemento `mip::MetadataAction` contenente i dati da rimuovere usando `GetMetadataToRemove()` e i dati da aggiungere usando `GetMetadataToAdd()`.

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

- Informazioni su come [passare gli eventi di controllo a Azure Information Protection Analytics](concept-handler-policy-auditing-cpp.md)
- Scaricare gli [esempi di API dei criteri da GitHub e provare l'API dei criteri](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
