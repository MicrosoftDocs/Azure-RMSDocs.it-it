---
title: Cronologia delle versioni di Microsoft Information Protection (MIP) SDK e criteri di supporto
description: Guida introduttiva che mostra come scrivere la logica di inizializzazione per applicazioni client di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/08/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: c2a5d89bf318d9e685d00033ba3ad53915659cdb
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882662"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Cronologia delle versioni di Microsoft Information Protection (MIP) SDK e criteri di supporto

## <a name="servicing"></a>Manutenzione 

Ogni versione disponibile a livello generale è supportata per sei mesi dopo il rilascio della versione GA successiva. La documentazione potrebbe non includere informazioni sulle versioni non supportate. Le correzioni e le nuove funzionalità sono applicabili solo alla versione GA più recente.

Le versioni di anteprima non devono essere distribuite nell'ambiente di produzione. Usare invece la versione di anteprima più recente per testare nuove funzionalità o correzioni che saranno disponibili nella prossima versione GA. È supportata solo la versione di anteprima più recente.

## <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per visualizzare le novità o le modifiche per una versione supportata. La versione più recente è elencata per prima. 

> [!NOTE]
> Le correzioni minime non sono elencate, quindi se si verifica un problema con l'SDK, è consigliabile verificare se è stato risolto con la versione GA più recente. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, visitare il [forum stack overflow Microsoft Information Protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 


## <a name="version-130"></a>Versione 1.3.0

**Data di rilascio**: TBD

## <a name="version-120"></a>Versione 1.2.0

**Data di rilascio**: 15 aprile 2019

## <a name="version-110"></a>Versione 1.1.0

**Data di rilascio**: 15 gennaio 2019

Questa versione introduce il supporto per le piattaforme seguenti:

  - .NET
  - iOS SDK (API criteri)
  - Android SDK (API per i criteri e API di protezione)

**Nuove funzionalità:**

- Supporto di ADRMS
- Le operazioni dell'API di protezione sono realmente asincrone (su Win32), consentendo operazioni di crittografia/decrittografia simultanee non bloccanti
  - I callback dell'applicazione (AuthDelegate, HTTPDelegate e così via) possono ora essere richiamati in *qualsiasi* thread in background
- È ora possibile leggere le proprietà personalizzate dell'etichetta impostate dagli amministratori IT tramite MIP:: Label:: GetCustomSettings
- È ora possibile recuperare la licenza di pubblicazione serializzata direttamente da un file senza operazioni HTTP tramite MIP:: FileHandler:: GetSerializedPublishingLicense
- Le applicazioni ricevono una notifica se è necessaria un'operazione HTTP per completare la creazione di un MIP:: fileengine/MIP::P olicyEngine tramite MIP:: fileprofile:: Observer:: OnAddPolicyEngineStarting/MIP::P olicyProfile:: Observer:: OnAddEngineStarting
- Il rilevamento del contenuto protetto con una data di scadenza o non è stato semplificato con il metodo di convenienza MIP::P rotectionDescriptor::D oesContentExpire
- Classificazione
  - I tipi di riservatezza (espressioni Regex per CC #, Passport # e così via) possono essere acquisiti dal servizio SCC
    - Abilitare la funzionalità impostando MIP:: fileengine:: Settings/MIP::P olicyEngine:: Settings flag
    - Leggere i tipi tramite MIP:: fileengine:: ListSensitivityTypes/MIP::P olicyEngine:: ListSensitivityTypes
  - I risultati della classificazione delle utilità per lo scanner di documenti esterni possono essere inseriti nel MIP per guidare le etichette consigliate/obbligatorie in base al contenuto del documento
    - Passa i risultati a MIP tramite MIP:: FileExecutionState:: GetClassificationResults/MIP:: ExecutionState:: GetClassificationResults
    - MIP:: ApplyLabelAction e MIP:: RecommendLabelAction possono essere restituiti da MIP::P olicyEngine:: ComputeActions quando i risultati della classificazione corrispondono a una regola di criteri che indica le etichette obbligatorie/consigliate

- Nuovi requisiti:
  - Popolamento applicato dei campi ID/nome/versione MIP:: ApplicationInfo durante la creazione di MIP:: fileprofile, MIP::P olicyProfile e MIP::P rotectionProfile
  - Per la creazione di MIP:: FileHandler, le applicazioni devono implementare la nuova interfaccia MIP:: FileExecutionState
  
- Eccezioni aggiornate:
  - MIP:: NoAuthTokenError generata se AuthDelegate dell'applicazione restituisce un token vuoto (a causa dell'annullamento)
    - Si applica alla creazione di:
      - mip::FileEngine
      - mip::FileHandler
      - MIP::P olicyEngine
      - MIP::P rotectionHandler
  - MIP:: NoPolicyError generato se il tenant non è configurato per le etichette
    - Si applica alla creazione di:
      - mip::FileEngine
      - MIP::P olicyEngine
  - MIP:: ServiceDisabledError generata se il servizio RMS è disabilitato per un utente/dispositivo/piattaforma/tenant specifico
    - Si applica alla creazione di:
      - mip::FileHandler
      - MIP::P rotectionHandler
  - MIP:: NoPermissionsError generata se un utente non dispone dei diritti per decrittografare un documento o il contenuto è scaduto
    - Si applica alla creazione di:
      - mip::FileHandler
      - MIP::P rotectionHandler

**Correzioni**:

TBD

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sulle piattaforme supportate e altro, vedere [domande frequenti e problemi relativi a MIP SDK](faqs-known-issues.md) .
- Per informazioni su come iniziare a usare l'SDK MIP, vedere [installazione e configurazione di MIP SDK](setup-configure-mip.md) .
