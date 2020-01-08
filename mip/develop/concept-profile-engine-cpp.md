---
title: Concetti - Concetti fondamentali di MIP SDK - Profilo e motore
description: Questo articolo aiuterà a comprendere i concetti fondamentali dell'SDK, ovvero il profilo e il motore creati durante l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2019
ms.author: mbaldwin
ms.openlocfilehash: de78ed0e5b3dfe7f9f5c1e2efa7edd77a0719986
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556130"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - Concetti relativi agli oggetti profilo e motore

## <a name="profiles"></a>Profiles

Se la `MipContext` è la classe per l'archiviazione delle impostazioni specifiche dell'SDK, il profilo è la classe radice per tutte le operazioni di assegnazione di etichette MIP e specifiche della protezione in MIP SDK. Prima di usare uno dei tre set di API, l'applicazione client deve creare un profilo. Le operazioni future vengono eseguite dal profilo o da altri oggetti *aggiunti* al profilo.

Esistono tre tipi di profilo in MIP SDK:

- [`PolicyProfile`](reference/class_mip_policyprofile.md): la classe profilo per l'API Criteri di MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): la classe profilo per l'API Protezione di MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): la classe profilo per l'API File di MIP.

L'API usata nell'applicazione di consumo determina la classe del profilo da usare.

Il profilo stesso offre le funzionalità seguenti:

- Definisce se lo stato deve essere caricato in memoria o salvato in modo permanente su disco e, se è salvato in modo permanente su disco, deve essere crittografato.
- Gestisce l'autenticazione mediante l'accettazione di un `mip::AuthDelegate`.
- Definisce la `mip::ConsentDelegate` che deve essere utilizzata per le operazioni di consenso.
- Definisce l'implementazione del `mip::FileProfile::Observer` che verrà utilizzata per i callback asincroni per le operazioni del profilo.

### <a name="profile-settings"></a>Impostazioni profilo

- `MipContext`: oggetto `MipContext` inizializzato per archiviare le informazioni sull'applicazione, il percorso di stato e così via.
- `CacheStorageType`: definisce come archiviare lo stato: in memoria, su disco o su disco e crittografato.
- `authDelegate`: puntatore condiviso della classe `mip::AuthDelegate`.
- `consentDelegate`: puntatore condiviso della classe [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md).
- `observer`: un puntatore condiviso all'implementazione del `Observer` del profilo (in [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)e [`FileProfile`](reference/class_mip_fileprofile_observer.md)).
- `applicationInfo`: oggetto [`mip::ApplicationInfo`](reference/mip-enums-and-structs.md#structures) . Informazioni sull'applicazione che utilizza l'SDK, che corrisponde all'ID e al nome della registrazione dell'applicazione Azure Active Directory.

## <a name="engines"></a>Motori

I motori di file, profili e API di protezione forniscono un'interfaccia per le operazioni eseguite su da un'identità specifica. Un motore viene aggiunto all'oggetto profilo per ogni utente o entità servizio che accede all'applicazione. È possibile eseguire operazioni delegate tramite `mip::ProtectionSettings` e il file o il gestore di protezione. Per altri dettagli, vedere [la sezione impostazioni di protezione nei concetti relativi a FileHandler](concept-handler-file-cpp.md) .

Esistono tre classi motore nell'SDK, una per ogni API. L'elenco seguente illustra le classi motore e alcune delle funzioni associate a ognuna:

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: ottiene l'elenco di etichette per il motore caricato.
  - `GetSensitivityLabel()`: ottiene l'etichetta dal contenuto esistente.
  - `ComputeActions()`: specificando l'ID di etichetta e metadati facoltativi, restituisce l'elenco delle azioni che devono verificarsi per un elemento specifico.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: ottiene l'elenco di etichette per il motore caricato.
  - `CreateFileHandler()`: crea un `mip::FileHandler` per un flusso o un file specifico.

### <a name="engine-states"></a>Stati del motore

Un motore può avere uno di due stati:

- `CREATED`: indica che l'SDK dispone di informazioni sufficienti sullo stato locale dopo la chiamata dei servizi back-end richiesti.
- `LOADED`: l'SDK ha costruito le strutture di dati necessarie affinché il motore possa essere operativo.

Un motore deve essere creato e caricato per eseguire qualsiasi operazione. La classe `Profile` espone alcuni metodi di gestione del motore: `AddEngineAsync`, `RemoveEngineAsync` e `UnloadEngineAsync`.

Nella tabella seguente vengono descritti i possibili stati del motore e quali metodi possono modificare lo stato:

|         | NONE              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>ID del motore

Ogni motore ha un identificatore univoco, `id`, che viene usato in tutte le operazioni di gestione del motore. L'applicazione può fornire un `id`o l'SDK può generarne uno, se non è fornito dall'applicazione. Tutte le altre proprietà del motore (ad esempio, l'indirizzo di posta elettronica nelle informazioni sull'identità) sono payload opachi per l'SDK. L'SDK NON esegue alcuna logica per mantenere univoche le altre proprietà o applicare altri vincoli.

> [!IMPORTANT]
> Come procedura consigliata, usare un ID del motore univoco per l'utente e usarlo ogni volta che l'utente esegue un'operazione con l'SDK. Se non si specifica un ID di motore esistente, i round trip di servizio aggiuntivi potranno recuperare i criteri e le licenze che potrebbero essere già state memorizzate nella cache per il motore esistente.

### <a name="engine-management-methods"></a>Metodi di gestione del motore

Come indicato in precedenza, nell'SDK sono disponibili tre metodi di gestione del motore: `AddEngineAsync`, `DeleteEngineAsync`e `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Questo metodo carica un motore esistente o ne crea uno se non ne esiste già uno nello stato locale.

Se l'applicazione non fornisce un `id`, `AddEngineAsync` genera un nuovo `id`. Controlla quindi se esiste già un motore con tale `id` nello stato locale. In caso affermativo, carica tale motore. Se il motore *non* esiste nello stato locale, viene creato un nuovo motore chiamando le API e i servizi back-end necessari.

In entrambi i casi, se il metodo ha esito positivo, il motore viene caricato ed è pronto all'uso.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Elimina il motore con l'`id` specificato. Tutte le tracce del motore vengono rimosse dallo stato locale.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Scarica le strutture di dati in memoria per il motore con l'`id` specificato. Lo stato locale di questo motore è ancora integro e può essere ricaricato con `AddEngineAsync`.

Questo metodo consente all'applicazione di essere prudente sull'utilizzo della memoria, scaricando i motori che non si prevede di utilizzare a breve.

## <a name="next-steps"></a>Passaggi successivi

- Scoprire di più sui [concetti correlati all'autenticazione](concept-authentication-cpp.md) e sugli [osservatori](concept-async-observers.md). MIP fornisce un modello di autenticazione estensibile, mentre gli osservatori vengono usati per fornire le notifiche degli eventi per gli eventi asincroni. Entrambi sono fondamentali e si applicano a tutti i set di API MIP.
- Procedere quindi ad approfondire i concetti di profilo e motore per le API File, Criteri e Protezione
  - [Concetti relativi al profilo dell'API File](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API File](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Criteri](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Criteri](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Protezione](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Protezione](concept-profile-engine-file-engine-cpp.md)  
