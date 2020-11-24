---
title: 'Concetti: i concetti di base in MIP SDK-MipContext'
description: Questo articolo consente di comprendere il concetto di Core SDK, denominato MipContext, che determina l'inizializzazione dell'applicazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: ed5c960215c67d424a31f7293a94b42629251eb4
ms.sourcegitcommit: 4815ab96e4596303af297ae4c13fb6d7083b21e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/30/2020
ms.locfileid: "95568431"
---
# <a name="microsoft-information-protection-sdk---mipcontext-object-concepts"></a>Microsoft Information Protection SDK-concetti sugli oggetti MipContext

## <a name="mipcontext"></a>MipContext

`MipContext` è l'oggetto di livello più alto nell'SDK. È responsabile della gestione dello stato in tutti i profili che possono essere creati come parte di un'applicazione o di un servizio. Inoltre, gestisce il rilascio delle risorse SDK MIP dopo che l'oggetto MipContext è stato eliminato definitivamente. È consentito solo un singolo `MipContext` processo. La creazione di più di uno può causare un comportamento imprevisto.

In particolare, `MipContext` fornisce le impostazioni per le opzioni seguenti:

- `mip::ApplicationInfo` nell'SDK, usato per l'ID applicazione, la versione e il nome dell'applicazione.
- Il percorso in cui devono essere archiviate le informazioni sullo stato MIP, se abilitato.
- Livello di registrazione.
- Delegato del logger personalizzato, se lo si desidera.
- Override della configurazione della telemetria.
- Abilitare le funzionalità di anteprima nell'SDK dietro ai flag funzionalità.

Una volta creato un oggetto `mip::MipContext` , l' `MipContext` oggetto può essere utilizzato per creare `mip::FileProfile` oggetti (o `PolicyProfile` / `ProtectionProfile` ).

### <a name="mipcontext-functions"></a>Funzioni MipContext

`mip::MipContext` espone tre funzioni statiche importanti che consentono di creare ed eliminare definitivamente `MipContext` oggetti.

#### `mip::MipContext::Create()`

Crea una nuova istanza di MipContext da utilizzare durante l'inizializzazione dei profili. Questa funzione accetta:

- `mip::ApplicationInfo`
- Percorso per la cache di archiviazione MIP.
- `mip::LogLevel`
- (Facoltativo) `mip::LoggerDelegate`
- (Facoltativo) `mip::TelemetryConfiguration`

#### `mip::MipContext::CreateWithCustomFeatureSettings()`

Crea una nuova istanza di MipContext da utilizzare durante l'inizializzazione dei profili, con le impostazioni delle funzionalità personalizzate abilitate.

- `mip::ApplicationInfo`
- Percorso per la cache di archiviazione MIP.
- `mip::LogLevel`
- (Facoltativo) `mip::LoggerDelegate`
- (Facoltativo) `mip::TelemetryConfiguration`
- `mip::FlightingFeature`

#### `mip::mipContext::Shutdown()`

Rilascia tutte le risorse MIP. Deve essere chiamato prima dell'arresto dell'app. Il distruttore chiamerà `MipContext` anche questa funzione quando l' `MipContext` oggetto viene eliminato definitivamente.

## <a name="next-steps"></a>Passaggi successivi

- Scoprire di più sui [concetti correlati all'autenticazione](concept-authentication-cpp.md) e sugli [osservatori](concept-async-observers.md). MIP fornisce un modello di autenticazione estensibile, mentre gli osservatori vengono usati per fornire le notifiche degli eventi per gli eventi asincroni. Entrambi sono fondamentali e si applicano a tutti i set di API MIP.
- Procedere quindi ad approfondire i concetti di profilo e motore per le API File, Criteri e Protezione
  - [Concetti relativi al profilo dell'API File](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API File](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Criteri](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Criteri](concept-profile-engine-file-engine-cpp.md)
  - [Concetti relativi al profilo dell'API Protezione](concept-profile-engine-file-profile-cpp.md)
  - [Concetti relativi al motore dell'API Protezione](concept-profile-engine-file-engine-cpp.md)
