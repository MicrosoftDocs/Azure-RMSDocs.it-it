---
title: "Concetti: il controllo nell'API Criteri di Microsoft Information Protection SDK"
description: Questo articolo aiuta a comprendere in che modo usare Microsoft Information Protection SDK per inviare gli eventi di controllo dell'API Criteri all'analitica di Azure Information Protection.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/07/2018
ms.author: tommos
ms.openlocfilehash: c660a5f58acd87ff9047a21fea26cc2732667493
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297815"
---
# <a name="auditing-in-the-mip-sdk"></a>Controllo in MIP SDK

Nel portale di amministrazione di Azure Information Protection è possibile accedere ai report di amministratore. Questi report offrono la visibilità sulle etichette che gli utenti applicano, manualmente o automaticamente, in tutte le applicazioni in cui è integrato MIP SDK. I partner di sviluppo che sfruttano l'SDK possono abilitare facilmente questa funzionalità per presentare nei report dei clienti le informazioni contenute nelle proprie applicazioni.

## <a name="event-types"></a>Tipi di evento

Esistono tre tipi di eventi che possono essere inviati con l'SDK all'analitica di Azure Information Protection. **Eventi di heartbeat**, **eventi di individuazione** ed **eventi di modifica**

### <a name="heartbeat-events"></a>Eventi di heartbeat

Gli eventi di heartbeat vengono generati automaticamente per qualsiasi applicazione in cui è integrata l'API Criteri. Gli eventi di heartbeat includono:

* TenantId
* Ora di generazione
* Nome dell'entità utente
* Nome del computer in cui è stato generato il controllo
* Process Name
* Piattaforma
* ID applicazione: corrisponde all'ID dell'applicazione Azure AD.

Questi eventi sono utili per rilevare nell'azienda le applicazioni che usano Microsoft Information Protection SDK.

### <a name="discovery-events"></a>Eventi di individuazione

Gli eventi di individuazione offrono indicazioni sulle informazioni con etichetta che vengono lette o usate dall'API Criteri. Questi eventi sono utili poiché indicano i dispositivi, la posizione e gli utenti che accedono alle informazioni nell'intera organizzazione.

Gli eventi di individuazione vengono generati nell'API Criteri impostando un flag booleano quando si crea l'oggetto `mip::PolicyHandler` con `mip::PolicyEngine`. Nell'esempio seguente il valore per **isAuditDiscoveryEnabled** è impostato su true. Quando `mip::ExecutionState` viene passato a `ComputeActions()` o `GetSensitivityLabel()` (con le informazioni sui metadati e l'identificatore di contenuto esistenti), le informazioni di individuazione vengono inviate all'analitica di Azure Information Protection.

Il controllo di individuazione viene generato dopo che l'applicazione chiama `ComputeActions()` o `GetSensitivityLabel()` e specifica `mip::ExecutionState`. Questo evento viene generato una sola volta per ogni gestore.

Esaminare la documentazione relativa ai concetti di `mip::ExecutionState` per altre informazioni sullo stato di esecuzione.

```cpp
// Create PolicyHandler, passing in true for isAuditDiscoveryEnabled
auto handler = mEngine->CreatePolicyHandler(true);

// Returns vector of mip::Action and generates discovery event.
auto actions = handler->ComputeActions(*state);

//Or, get the label for a given state
auto label = handler->GetSensitivityLabel(*state);
```

In pratica **isAuditDiscoveryEnabled** deve essere `true` durante la costruzione di `mip::PolicyHandler`, per consentire alle informazioni di accesso ai file di passare all'analitica di Azure Information Protection.

## <a name="change-event"></a>Evento di modifica

Gli eventi di modifica rendono disponibili informazioni sul file, sull'etichetta applicata o modificata e le motivazioni specificate dall'utente. Gli eventi di modifica vengono generati chiamando `NotifyCommittedActions()` per l'oggetto `mip::PolicyHandler`. La chiamata viene effettuata dopo l'esecuzione del commit di una modifica in un file, passando l'oggetto `mip::ExecutionState` usato per calcolare le azioni.

> Se l'applicazione non riesce a chiamare questa funzione, non arriverà alcun evento nell'analitica di Azure Information Protection.

```cpp
handler->NotifyCommittedActions(*state);
```

## <a name="audit-dashboard"></a>Dashboard di controllo

Gli eventi inviati alla pipeline di controllo di Azure Information Protection vengono visualizzati nei report in corrispondenza di https://portal.azure.com. L'analitica di Azure Information Protection è disponibile come anteprima pubblica e le funzionalità sono soggette a modifica.

## <a name="next-steps"></a>Passaggi successivi

Vedere il [blog dell'annuncio anteprima nella community IT](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) per altri dettagli sull'esperienza di controllo in Azure Information Protection.

