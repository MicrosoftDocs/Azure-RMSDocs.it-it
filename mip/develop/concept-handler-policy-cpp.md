---
title: Concetti - Gestori di criteri in MIP SDK.
description: Questo articolo illustra le modalità di creazione e uso dei gestori dell'API Criteri per la chiamata di operazioni.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/16/2018
ms.author: tommos
ms.openlocfilehash: cc35475086de76b869428c62cfc35e73fc3060db
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258777"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft Information Protection SDK - Concetti relativi ai gestori di criteri

Nell'API di criteri, `mip::PolicyHandler` espone operazioni usate per le azioni dei criteri di calcolo e inviare gli eventi di controllo.

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

Il primo passaggio necessario per ottenere le azioni dei criteri consiste nella creazione di un oggetto `PolicyHandler`. Questa classe implementa le funzionalità richieste per ottenere l'elenco delle azioni che deve intraprendere un'etichetta specifica. Implementa inoltre la funzione per attivare un evento di controllo.

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

## <a name="next-steps"></a>Passaggi successivi

Ora che si sono appresi la creazione di un gestore dei criteri:

- Informazioni su come [creare una classe di stato di esecuzione](concept-handler-policy-executionstate-cpp.md), che viene usato per determinare le azioni di calcolo.
- Scaricare il [esempi dell'API dei criteri da GitHub e provare l'API di criteri](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
