---
title: Concetti - Concetti fondamentali di MIP SDK - Profilo e motore
description: Questo articolo aiuterà a comprendere i concetti fondamentali dell'SDK, ovvero il profilo e il motore creati durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e815820fa9f3a6de95d5e37e350ed18df8513b21
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175106"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - Concetti relativi agli oggetti profilo e motore

## <a name="profiles"></a>Profiles

Il profilo è la classe radice per tutte le operazioni in MIP SDK. Prima di usare una delle tre API, l'applicazione client deve creare un profilo. Le operazioni future vengono eseguite dal profilo o da altri oggetti *aggiunti* al profilo.

Esistono tre tipi di profilo in MIP SDK:

- [`PolicyProfile`](reference/class_mip_policyprofile.md): La classe di profilo per l'API di criteri di MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): La classe di profilo per l'API di protezione MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): La classe di profilo per l'API File MIP.

L'API usata nell'applicazione che determina quale classe profilo deve essere usata.

Il profilo stesso offre le funzionalità seguenti:

- Definisce la posizione di archiviazione per lo stato dell'SDK. I dati di stato includono i dettagli dell'utente, i criteri utente scaricati, i log e i dati di telemetria.
- Definisce se lo stato deve essere caricato in memoria o salvato in modo permanente su disco.
- Gestisce l'autenticazione mediante l'accettazione di un `mip::AuthDelegate`.
- Imposta l'ID dell'applicazione e il nome descrittivo dell'app che utilizza l'SDK.

### <a name="profile-settings"></a>Impostazioni profilo

- `Path`: Percorso del file in cui la registrazione, la telemetria e altro stato persistente viene archiviato.
- `useInMemoryStorage`: Un valore booleano che definisce se lo stato deve essere archiviato in memoria, o su disco.
- `authDelegate`: Un puntatore condiviso della classe `mip::AuthDelegate`. 
- `consentDelegate`: Un puntatore condiviso della classe [ `mip::ConsentDelegate` ](reference/class_mip_consentdelegate.md). 
- `observer`: Un puntatore condiviso per il profilo `Observer` implementazione (in [ `PolicyProfile` ](reference/class_mip_policyprofile_observer.md), [ `ProtectionProfile` ](reference/class_mip_protectionprofile_observer.md), e [ `FileProfile` ](reference/class_mip_fileprofile_observer.md)).
- `applicationInfo`: Oggetto [ `mip::ApplicationInfo` ](reference/mip-enums-and-structs.md#structures) oggetto. Informazioni sull'applicazione che utilizza il SDK, che corrisponde l'ID di registrazione dell'applicazione Azure Active Directory e al nome.

## <a name="engines"></a>Motori

I motori di File, il profilo e API di protezione forniscono un'interfaccia alle operazioni eseguite per conto di un'identità specifica. Un motore viene aggiunto all'oggetto profilo, per ogni utente che esegue l'accesso all'applicazione. Tutte le operazioni eseguite dal motore presenti nel contesto di tale identità.

Esistono tre classi motore nell'SDK, una per ogni API. L'elenco seguente illustra le classi motore e alcune delle funzioni associate a ognuna:

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: Ottiene l'elenco di etichette per il motore caricato.
  - `GetSensitivityLabel()`: Ottiene l'etichetta dal contenuto esistente.
  - `ComputeActions()`: Fornito con un ID dell'etichetta e, facoltativamente i metadati, restituisce l'elenco di azioni che devono verificarsi in un elemento specifico.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: Ottiene l'elenco di etichette per il motore caricato.
  - `CreateFileHandler()`: Crea un `mip::FileHandler` per un flusso o file specifici.

### <a name="engine-states"></a>Stati del motore

Un motore può avere uno di due stati:

- `CREATED`: Creata indica che il SDK dispone di sufficienti informazioni sullo stato locale dopo la chiamata dei servizi di back-end richiesto.
- `LOADED`: il SDK è progettato le strutture di dati necessari per il motore per essere operativi.

Un motore deve essere creato e caricato per eseguire qualsiasi operazione. La classe `Profile` espone alcuni metodi di gestione del motore: `AddEngineAsync`, `RemoveEngineAsync` e `UnloadEngineAsync`.

La tabella seguente descrive gli stati possibili di gestione e i metodi che è possono modificare tale stato:

|         | NONE              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>ID del motore

Ogni motore ha un identificatore univoco, `id`, che viene usato in tutte le operazioni di gestione del motore. L'applicazione può fornire un `id`, o il SDK può generato uno, se non viene fornito dall'applicazione. Tutte le altre proprietà del motore (ad esempio, l'indirizzo di posta elettronica nelle informazioni sull'identità) sono payload opachi per l'SDK. L'SDK NON esegue alcuna logica per mantenere univoche le altre proprietà o applicare altri vincoli.

### <a name="engine-management-methods"></a>Metodi di gestione del motore

Come accennato in precedenza, sono disponibili tre metodi di gestione del motore nel SDK: `AddEngineAsync`, `DeleteEngineAsync`, e `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Questo metodo carica un motore esistente o ne crea uno se non esiste già nello stato locale.

Se l'applicazione non fornisce un `id`, `AddEngineAsync` genera un nuovo `id`. Controlla quindi se esiste già un motore con tale `id` nello stato locale. In caso affermativo, carica tale motore. Se il motore *non* esiste nello stato locale, viene creato un nuovo motore chiamando le API e i servizi back-end necessari.

In entrambi i casi, se il metodo ha esito positivo, il motore viene caricato ed è pronto all'uso.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Elimina il motore con l'`id` specificato. Tutte le tracce del motore vengono rimosse dallo stato locale.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Scarica le strutture di dati in memoria per il motore con l'`id` specificato. Lo stato locale di questo motore è ancora integro e può essere ricaricato con `AddEngineAsync`.

Questo metodo consente all'applicazione di essere attento sull'utilizzo della memoria, da motori di scaricamento che non si prevede di usare presto.

## <a name="next-steps"></a>Passaggi successivi

- Scoprire di più sui [concetti correlati all'autenticazione](concept-authentication-cpp.md) e sugli [osservatori](concept-async-observers.md). MIP fornisce un modello di autenticazione estensibile, mentre gli osservatori vengono usati per fornire le notifiche degli eventi per gli eventi asincroni. Entrambi sono fondamentali e si applicano a tutti i set di API MIP.
- Procedere quindi ad approfondire i concetti di profilo e motore per le API File, Criteri e Protezione
  - [Concetti relativi al profilo dell'API File](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API File](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Criteri](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Criteri](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Protezione](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Protezione](concept-profile-engine-file-engine-cpp.md)  
