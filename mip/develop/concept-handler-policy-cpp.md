---
title: Concetti - Gestori di criteri in MIP SDK.
description: Questo articolo illustra le modalità di creazione e uso dei gestori dell'API Criteri per la chiamata di operazioni.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 583e59832e40f87665232ebf39e1dddb462ba212
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556181"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft Information Protection SDK - Concetti relativi ai gestori di criteri

Nell'API dei criteri, `mip::PolicyHandler` espone le operazioni usate per calcolare le azioni dei criteri e inviare gli eventi di controllo.

## <a name="policy-handler-functions"></a>Funzioni di gestione criteri

`mip::PolicyHandler` espone i metodi per la lettura, scrittura e rimozione sia delle etichette che delle informazioni sulla protezione. Per un elenco completo, vedere le [informazioni di riferimento sull'API](reference/class_mip_PolicyHandler.md).

In questo articolo verranno descritti i metodi seguenti:

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>requisiti

La creazione di un elemento `PolicyHandler` richiede:

- Un elemento `mip::MipContext`
- Un elemento `mip::PolicyProfile`
- Un elemento `mip::PolicyEngine` aggiunto a `mip::PolicyProfile`
- Classe che implementa `mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>Creare un gestore di criteri

Il primo passaggio necessario per ottenere le azioni dei criteri consiste nella creazione di un oggetto `PolicyHandler`. Questa classe implementa la funzionalità necessaria per ottenere l'elenco delle azioni che devono essere eseguite da un'etichetta specifica. Implementa inoltre la funzione per attivare un evento di controllo.

Per creare `PolicyHandler` è sufficiente chiamare la funzione `CreatePolicyHandlerAsync` di `PolicyEngine` usando il modello promise/future.

`CreatePolicyHandlerAsync` accetta un singolo parametro: **isAuditDiscoveryEnabled**. Impostare questo valore su **true** se l'applicazione deve far emergere gli eventi heartbeat e di individuazione nella registrazione di controllo.

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

Ora che si è appreso come creare un gestore dei criteri:

- Informazioni su come [creare una classe di stato di esecuzione](concept-handler-policy-executionstate-cpp.md), che viene usata per determinare le azioni di calcolo.
- Scaricare gli [esempi di API dei criteri da GitHub e provare l'API dei criteri](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
