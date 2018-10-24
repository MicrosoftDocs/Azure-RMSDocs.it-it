---
title: Concetti - Concetti fondamentali di MIP SDK - Profilo e motore
description: Questo articolo aiuterà a comprendere i concetti fondamentali dell'SDK, ovvero il profilo e il motore creati durante l'inizializzazione dell'applicazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6f11944e7cceed39423af2a8104ce044d1f6eec6
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453419"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - Concetti relativi agli oggetti profilo e motore

## <a name="profiles"></a>Profili

Il profilo è la classe radice per tutte le operazioni in MIP SDK. Prima di usare una delle tre API, l'applicazione client deve creare un profilo. Tutte le operazioni future verranno eseguite dal profilo o da altri oggetti *aggiunti* al profilo.

Esistono tre tipi di profilo in MIP SDK:

- [`PolicyProfile`](reference/class_mip_policyprofile.md): la classe profilo per l'API Criteri di MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): la classe profilo per l'API Protezione di MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): la classe profilo per l'API File di MIP.

L'API usata nell'applicazione di destinazione determinerà la classe di profilo da usare.

Il profilo stesso offre le funzionalità seguenti:

- Definisce la posizione di archiviazione per lo stato dell'SDK. I dati di stato includono i dettagli dell'utente, i criteri utente scaricati, i log e i dati di telemetria.
- Definisce se lo stato deve essere caricato in memoria o salvato in modo permanente su disco.
- Gestisce l'autenticazione mediante l'accettazione di un `mip::AuthDelegate`.
- Imposta l'ID dell'applicazione e il nome descrittivo dell'app che utilizza l'SDK.

### <a name="profile-settings"></a>Impostazioni profilo

- `Path`: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
- `useInMemoryStorage`: valore booleano che definisce se gli stati devono essere archiviati in memoria o su disco.
- `authDelegate`: puntatore condiviso della classe `mip::AuthDelegate`. 
- `consentDelegate`: puntatore condiviso della classe `mip::ConsentDelegate`. 
- `observer`: puntatore condiviso all'implementazione `Observer` del profilo (in `PolicyProfile`, `ProtectionProfile` e `EngineProfile`).
- `applicationInfo`: oggetto `mip::ApplicationInfo`. Informazioni relative all'applicazione che utilizza l'SDK.

## <a name="engines"></a>Motori

Nelle API File, Criteri e Protezione, i motori offrono un'interfaccia per le operazioni eseguite per conto di un'identità specifica. Verrà aggiunto un motore all'oggetto profilo per ogni utente che accede all'applicazione. Tutte le operazioni eseguite dal motore saranno nel contesto di tale identità.

Esistono tre classi motore nell'SDK, una per ogni API. L'elenco seguente illustra le classi motore e alcune delle funzioni associate a ognuna:

- [`mip::ProtectionEngine`]
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

La tabella seguente descrive gli stati possibili del motore e quale metodo può modificare tale stato.

|         | NONE              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>ID del motore

Ogni motore ha un identificatore univoco, `id`, che viene usato in tutte le operazioni di gestione del motore. L'applicazione può fornire un `id` o l'SDK genererà un nuovo identificatore univoco, se non ne viene fornito uno dall'applicazione. Tutte le altre proprietà del motore (ad esempio, l'indirizzo di posta elettronica nelle informazioni sull'identità) sono payload opachi per l'SDK. L'SDK NON esegue alcuna logica per mantenere univoche le altre proprietà o applicare altri vincoli.

### <a name="engine-management-methods"></a>Metodi di gestione del motore

Come indicato in precedenza, sono disponibili tre metodi di gestione del motore nell'SDK: `AddEngineAsync`, `DeleteEngineAsync` e `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Questo metodo carica un motore esistente o ne crea uno nuovo se non ne esiste già uno nello stato locale.

Se l'applicazione non fornisce un `id`, `AddEngineAsync` genera un nuovo `id`. Controlla quindi se esiste già un motore con tale `id` nello stato locale. In caso affermativo, carica tale motore. Se il motore *non* esiste nello stato locale, viene creato un nuovo motore chiamando le API e i servizi back-end necessari.

In entrambi i casi, se il metodo ha esito positivo, il motore viene caricato ed è pronto all'uso.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Elimina il motore con l'`id` specificato. Tutte le tracce del motore vengono rimosse dallo stato locale.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Scarica le strutture di dati in memoria per il motore con l'`id` specificato. Lo stato locale di questo motore è ancora integro e può essere ricaricato con `AddEngineAsync`.

Questo metodo consente all'applicazione di utilizzare la memoria in modo efficiente, scaricando i motori che non è previsto vengano usati a breve.

## <a name="next-steps"></a>Passaggi successivi

- Scoprire di più sui [concetti correlati all'autenticazione](concept-authentication-cpp.md) e sugli [osservatori](concept-async-observers.md). MIP fornisce un modello di autenticazione estensibile, mentre gli osservatori vengono usati per fornire le notifiche degli eventi per gli eventi asincroni. Entrambi sono fondamentali e si applicano a tutti i set di API MIP.
- Procedere quindi ad approfondire i concetti di profilo e motore per le API File, Criteri e Protezione
  - [Concetti relativi al profilo dell'API File](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API File](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Criteri](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Criteri](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Protezione](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Protezione](concept-profile-engine-file-engine-cpp.md)  
