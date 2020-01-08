---
title: 'Concetti: implementazione di ExecutionState in Microsoft Information Protection SDK'
description: Questo articolo aiuta a comprendere come si usa ExecutionState in Microsoft Information Protection SDK per calcolare le azioni e specificare i dettagli per la registrazione di controllo.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: c3973488cb8c3ec109a5a11dea1e540f09db92d4
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555705"
---
# <a name="implement-executionstate"></a>Implementare ExecutionState

Il passaggio di informazioni a Microsoft Information Protection SDK per calcolare un'azione che deve essere usata, in base allo stato corrente e allo stato desiderato, viene implementato usando la classe `mip::ExecutionState`. Analogamente ad altre classi nell'SDK, `ExecutionState` è una classe astratta e deve essere implementata dallo sviluppatore.

> Per un esempio completo di implementazione di `ExecutionState`, esaminare l'origine di esempio seguente:
>
> * [execution_state_impl.h](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)
> * [execution_state_impl.cpp](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.cpp)

## <a name="mipexecutionstate-members"></a>mip::ExecutionState Members

`ExecutionState` espone i membri virtuali seguenti. Ognuno di essi specifica un contesto per il motore dei criteri per restituire le informazioni sulle azioni che devono essere eseguite dall'applicazione. Inoltre, queste informazioni possono essere usate per specificare informazioni di controllo per la funzionalità di reporting di Azure Information Protection.

| Membro                                                                             | Returns                                                                                                              |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `std::shared_ptr<mip::Label> GetNewLabel()`                                        | Restituisce l'etichetta da applicare all'oggetto.                                                                       |
| `mip::DataState GetDataState()`                                                    | Restituisce il MIP::D ataState dell'oggetto.                                                                            |
| `std::pair<bool, std::string> IsDowngradeJustified()`                              | Restituisce un std::pair che esprime se il downgrade è giustificato e la giustificazione.                                 |
| `std::string GetContentIdentifier()`                                               | Restituisce l'identificatore del contenuto. Deve essere un identificatore leggibile dall'utente, che indica la posizione dell'oggetto.        |
| `mip::ActionSource GetNewLabelActionSource()`                                      | Restituisce il mip::ActionSource dell'etichetta.                                                                          |
| `mip::AssignmentMethod GetNewLabelAssignmentMethod()`                              | Restituisce il mip::AssignmentMethod dell'etichetta                                                                       |
| `std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties()` | Restituisce un std::vector di std::pairs di stringa contenente i metadati personalizzati che verranno applicati al documento. |
| `std::vector<std::pair<std::string, std::string>> GetContentMetadata()`            | Restituisce un std::vector di std::pairs di stringa contenente i metadati di contenuto correnti.                               |
| `std::shared_ptr<mip::ProtectionDescriptor> GetProtectionDescriptor()`             | Restituisce un puntatore a un mip::ProtectionDescriptor                                                                     |
| `mip::ContentFormat GetContentFormat()`                                            | Restituisce mip::ContentFormat                                                                                           |
| `mip::ActionType GetSupportedActions()`                                            | Restituisce mip::ActionTypes per l'etichetta.                                                                              |
| `std::shared_ptr<mip::ClassificationResults>`                                      | Restituisce un elenco di risultati di classificazione, se implementato.                                                            |

Ogni elemento deve essere sottoposto a override in un'implementazione di una classe derivata da `mip::ExecutionState`. Nell'applicazione di esempio a cui fa riferimento il collegamento precedente questo processo viene eseguito implementando uno struct chiamato `ExecutionStateOptions` e passandolo al costruttore della classe derivata.

Nell'[esempio](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h) uno struct chiamato `ExecutionStateOptions` viene definito come:

```cpp
struct ExecutionStateOptions {
    std::unordered_map<std::string, std::string> metadata;
    std::string newLabelId;
    std::string contentIdentifier;
    mip::ActionSource actionSource = mip::ActionSource::MANUAL;
    mip::DataState dataState = mip::DataState::USE;
    mip::AssignmentMethod assignmentMethod = mip::AssignmentMethod::STANDARD;
    bool isDowngradeJustified = false;
    std::string downgradeJustification;
    std::string templateId;
    mip::ContentFormat contentFormat = mip::ContentFormat::DEFAULT;
    mip::ActionType supportedActions;
    bool generateAuditEvent;
};
```

Ogni proprietà viene impostata dall'applicazione, quindi `ExecutionStateOptions` viene passato al costruttore della classe derivata da `mip::ExecutionState`. Queste informazioni vengono usate per determinare le azioni da eseguire. I dati disponibili in `mip::ExecutionState` vengono esposti anche nell'analitica di Azure Information Protection.

### <a name="next-steps"></a>Passaggi successivi

- Informazioni su come determinare le [azioni di calcolo per un'etichetta nuova o esistente](concept-handler-policy-computeactions-cpp.md), in base allo stato corrente e desiderato.
- Scaricare gli [esempi di API dei criteri da GitHub e provare l'API dei criteri](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
