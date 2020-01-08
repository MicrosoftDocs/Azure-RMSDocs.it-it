---
title: Cronologia delle versioni di Microsoft Information Protection (MIP) SDK e criteri di supporto
description: Cronologia delle versioni e note sulle modifiche per il MIP SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: c28ab93feedea4c27ef9fe032f889d17da078d49
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555943"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Cronologia delle versioni di Microsoft Information Protection (MIP) SDK e criteri di supporto

## <a name="servicing"></a>Servizio 

Ogni versione disponibile a livello generale è supportata per sei mesi dopo il rilascio della versione GA successiva. La documentazione potrebbe non includere informazioni sulle versioni non supportate. Le correzioni e le nuove funzionalità sono applicabili solo alla versione GA più recente.

Le versioni di anteprima non devono essere distribuite nell'ambiente di produzione. Usare invece la versione di anteprima più recente per testare nuove funzionalità o correzioni che saranno disponibili nella prossima versione GA. È supportata solo la versione di anteprima più recente.

## <a name="release-history"></a>Cronologia versioni

Usare le informazioni seguenti per visualizzare le novità o le modifiche per una versione supportata. La versione più recente è elencata per prima. 

> [!NOTE]
> Le correzioni minime non sono elencate, quindi se si verifica un problema con l'SDK, è consigliabile verificare se è stato risolto con la versione GA più recente. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, visitare il [forum stack overflow Microsoft Information Protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 

## <a name="version-140"></a>Versione 1.4.0 

**Data di rilascio**: 6 novembre 2019

Questa versione introduce il supporto per l'API di protezione nel pacchetto .NET (Microsoft. InformationProtection. file).

### <a name="sdk-changes"></a>Modifiche dell'SDK
- Miglioramenti delle prestazioni e correzioni di bug
- Enumerazione StorageType rinominata in CacheStorageType
- Collegamenti Android a libc + + anziché gnustl
- Sono state rimosse le API deprecate in precedenza
  - File/criteri/profilo:: le impostazioni devono essere inizializzate con un MipContext
  - File/criteri/profilo:: impostazioni, percorso, informazioni sull'applicazione, delegato del logger, telemetria e getter/setter del livello di log sono stati rimossi. Queste proprietà sono gestite da MipContext
- Migliore supporto della libreria statica sulle piattaforme Apple
  - Librerie statiche monolitiche
    - libmip_file_sdk_static. a
    - libmip_upe_sdk_static. a
    - libmip_protection_sdk_static. a
    - libmip_upe_and_protection_sdk_static. a
  - dipendenze di terze parti estratte in librerie separate
    - libsqlite3. a
    - libssl. a
- Rimosso mip_telemetry. dll (Unito in mip_core. dll)

### <a name="file-api"></a>API File

- RPMSG
  - Encryption
  - Aggiunta del supporto per la decrittografia String8
- Comportamento dell'estensione PFILE configurabile (impostazione predefinita, <EXT>. PFILE o P<EXT>)
  - ProtectionSettings::SetPFileExtensionBehavior

### <a name="policy-api"></a>API Criteri

- API C completa
- Configurare il filtraggio delle etichette associate alla protezione
  - PolicyEngine:: impostazioni:: SetLabelFilter ()

### <a name="protection-api"></a>API Protezione

- Sono state rimosse le API deprecate in precedenza
  - Rimozione di ProtectionEngine:: CreateProtectionHandlerFromDescriptor [async] (usare ProtectionEngine:: CreateProtectionHandlerForPublishing [async])
  - Rimozione di ProtectionEngine:: CreateProtectionHandlerFromPublishingLicense [async] (usare ProtectionEngine:: CreateProtectionHandlerForConsumption [async])
- API C# completa
- API C completa
  - Modifiche di normalizzazione dell'API c dall'anteprima dell'API v 1.3 C:
    - Ridenominazione di mip_cc_storage_type in mip_cc_cache_storage_type
    - Ridenominazione di MIP_CC_AddProtectionProfileEngine in MIP_CC_ProtectionProfile_AddEngine
    - Ridenominazione di MIP_CC_CreateProtectionEngineSettingsForExistingEngine in MIP_CC_CreateProtectionEngineSettingsWithEng
    - Ridenominazione di MIP_CC_CreateProtectionEngineSettingsForNewEngine in MIP_CC_CreateProtectionEngineSettingsWithIdentity
    - Ridenominazione di MIP_CC_SetProtectionProfileSettingsHttpDelegate in MIP_CC_ProtectionProfileSettings_SetHttpDelegate
    - Ridenominazione di MIP_CC_CreateProtectionHandlerForConsumption in MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption
    - Ridenominazione di MIP_CC_CreateProtectionHandlerForPublishing in MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing
    - Ridenominazione di MIP_CC_GetProtectionEngineId in MIP_CC_ProtectionEngine_GetEngineId
    - Ridenominazione di MIP_CC_GetProtectionEngineTemplates in MIP_CC_ProtectionEngine_GetTemplates
    - Ridenominazione di MIP_CC_GetProtectionEngineTemplatesSize in MIP_CC_ProtectionEngine_GetTemplatesSize
    - Ridenominazione di MIP_CC_SetTelemetryConfigurationHttpDelegate in MIP_CC_TelemetryConfiguration_SetHttpDelegate
    - Ridenominazione di MIP_CC_SetTelemetryConfigurationHostName in MIP_CC_TelemetryConfiguration_SetHostName
    - Ridenominazione di MIP_CC_SetTelemetryConfigurationIsLocalCachingEnabled in MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled
    - Ridenominazione di MIP_CC_SetTelemetryConfigurationIsNetworkDetectionEnabled in MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled
    - Ridenominazione di MIP_CC_SetTelemetryConfigurationIsTelemetryOptedOut in MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut
    - Ridenominazione di MIP_CC_SetTelemetryConfigurationLibraryName in MIP_CC_TelemetryConfiguration_SetLibraryName
    - Rimossi MIP_CC_ProtectionEngine_GetRightsForLabelIdSize e aggiornati MIP_CC_ProtectionEngine_GetRightsForLabelId per popolare un mip_cc_string_list anziché un buffer di stringa delimitato da virgole
    - Rimossi MIP_CC_ProtectionHandler_GetRightsSize e aggiornati MIP_CC_ProtectionHandler_GetRights per popolare un mip_cc_string_list anziché un buffer di stringa delimitato da virgole
    - Aggiunta MIP_CC_ProtectionEngine_GetEngineIdSize e aggiornata MIP_CC_ProtectionEngine_GetEngineId per popolare un buffer di stringa anziché un mip_cc_guid
    - MIP_CC_CreateProtectionDescriptorFromUserRights ora accetta il parametro ' mip_cc_dictionary-' anziché' mip_cc_dictionary '
    - MIP_CC_ProtectionEngineSettings_SetCustomSettings ora accetta il parametro ' mip_cc_dictionary-' anziché' mip_cc_dictionary '
    - MIP_CC_ProtectionProfileSettings_SetCustomSettings ora accetta il parametro ' mip_cc_dictionary-' anziché' mip_cc_dictionary '
    - MIP_CC_TelemetryConfiguration_SetCustomSettings ora accetta il parametro ' mip_cc_dictionary-' anziché' mip_cc_dictionary '
    - MIP_CC_CreateMipContext accetta parametri ' isOfflineOnly ' è loggerDelegateOverride '


## <a name="version-130"></a>Versione 1.3.0

**Data di rilascio**: 22 agosto 2019

### <a name="new-features"></a>Nuove funzioni e caratteristiche

- `mip::MipContext` è il nuovo oggetto di livello più alto.
- Ora è supportata la decrittografia dei file MSG protetti.
- Il controllo dei file Message. rpmsg è supportato tramite `mip::FileInspector` e `mip::FileHandler::InspectAsync()`.
- È ora possibile crittografare facoltativamente la cache su disco.
- L'API di protezione ora supporta il cloud sovrano Cina.
- Supporto di Arm64 in Android.
- Supporto di Arm64e in iOS.
- È ora possibile disabilitare la cache del contratto di licenza con l'utente finale.
- . la crittografia Pfile può essere disabilitata tramite `mip::FileEngine::EnablePFile`
- Miglioramento delle prestazioni per le operazioni di protezione mediante la riduzione del numero di chiamate HTTP
- Rimossi i dettagli dell'identità delegata da `mip::Identity` e aggiunti `DelegatedUserEmail` a `mip::FileEngine::Settings`, `mip::ProtectionSettings`, `mip::PolicyEngine::Settings`e `mip::ProtectionHandler``PublishingSettings` e `ConsumptionSettings`.
- Le funzioni che in precedenza restituivano LabelId ora restituiscono un oggetto `mip::Label`.

### <a name="changes"></a>Modifiche

* Nelle versioni precedenti è necessario chiamare `mip::ReleaseAllResources`. La versione 1,3 sostituisce questa operazione con `mip::MipContext::~MipContext` o `mip::MipContext::Shutdown`.
* Rimossi `ActionSource` da `mip::LabelingOptions` e `mip::ExecutionState::GetNewLabelActionSource`
* Sostituito `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` con `mip::ProtectionEngine::CreateProtectionHandlerForPublishing`.
* Sostituito `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` con `mip::ProtectionEngine::CreateProtectionHandlerForConsumption`.
* Rinominato `mip::PublishingLicenseContext` `mip::PublishingLicenseInfo` e aggiornato in modo da contenere campi avanzati anziché byte serializzati non elaborati.
* `mip::PublishingLicenseInfo` contiene i dati rilevanti per MIP dopo l'analisi di una licenza di pubblicazione (PL).
* `mip::TemplateNotFoundError` e `mip::LabelNotFoundError` generata quando l'applicazione passa MIP un ID modello o un ID etichetta non riconosciuto.
* Aggiunta del supporto per l'accesso condizionale basato su etichetta tramite il parametro claims di `AcquireToken()` e `mip::AuthDelegate::OAuth2Challenge()`. Questa funzionalità non è stata ancora esposta tramite il portale del Centro sicurezza e conformità.


## <a name="version-120"></a>Versione 1.2.0

**Data di rilascio**: 15 aprile 2019

### <a name="new-features"></a>Nuove funzioni e caratteristiche

 - Il componente di telemetria USA ora lo stesso stack HTTP come il resto del MIP, anche se l'applicazione client ne ha eseguito l'override con HttpDelegate.
 - Le applicazioni client possono controllare il comportamento di threading delle attività asincrone eseguendo l'override di TaskDispatcherDelegate nei profili.
 - Crittografia RPMSG ora disponibile in anteprima.
 - Allinea il comportamento di gestione delle eccezioni di file/criteri SDK con Protection SDK:
    - ProxyAuthError generata da tutti gli SDK se un proxy è configurato per richiedere l'autenticazione.
    - NoAuthTokenError generata da tutti gli SDK se il token di autenticazione vuoto viene fornito dall'implementazione dell'applicazione MIP:: AuthDelegate:: AcquireOAuth2Token.
 - La memorizzazione nella cache HTTP migliorata per policy SDK riduce il numero di chiamate HTTP richieste da metà.
 - Log di controllo/telemetria più completi per migliorare il rilevamento e il debug degli errori.
 - Supporto per le etichette esterne/esterne per facilitare la migrazione alle etichette AIP.
 - Abilitazione del supporto per le applicazioni di terze parti per scaricare i tipi di sensibilità da SCC.
 - Altre impostazioni di telemetria sono esposte e configurabili (comportamento di Caching/Threading e così via).
 
### <a name="sdk-changes"></a>Modifiche dell'SDK

 - mip_common. dll viene suddivisa in mip_core. dll e mip_telemetry. dll.
 - Rinominato MIP:: ContentState in MIP::D ataState per descrivere il modo in cui un'applicazione interagisce con i dati a un livello elevato.
 - l'eccezione MIP:: AdhocProtectionRequiredError viene generata da FileHandler:: xmllabel per notificare a un'applicazione che deve prima applicare la protezione ad hoc prima di applicare un'etichetta.
 - l'eccezione MIP:: OperationCancelledError viene generata quando un'operazione è stata annullata, ad esempio a causa dell'arresto o dell'annullamento HTTP.
 - Nuove API:
    - MIP:: ClassificationResult:: GetSensitiveInformationDetections
    - MIP:: fileengine:: GetLastPolicyFetchTime
    - MIP:: fileengine:: GetDefaultSensitivityLabel
    - MIP:: fileengine:: GetPolicyId
    - MIP:: fileengine:: HasClassificationRules
    - MIP:: fileengine:: Settings:: SetPolicyCloudEndpointBaseUrl
    - MIP:: FileHandler:: GetDecryptedTemporaryFileAsync
    - MIP:: FileHandler:: Observer:: OnGetDecryptedTemporaryFileFailure
    - MIP:: FileHandler:: Observer:: OnGetDecryptedTemporaryFileSuccess
    - MIP:: file/Policy/ProtectionProfile:: SetTaskDispatcherDelegate
    - MIP:: file/Policy/ProtectionProfile:: SetTelemetryConfiguration
    - MIP:: HttpRequest:: GetBody restituisce std:: Vector < uint8_t > anziché std:: String
    - MIP:: HttpRequest:: GetId
    - MIP::P olicyEngine:: GetLastPolicyFetchTime
    - MIP::P olicyEngine:: GetPolicyId
    - MIP::P olicyEngine:: HasClassificationRules
    - MIP::P olicyEngine:: Settings:: SetCloudEndpointBaseUrl
    - MIP::P rotectionDescriptor:: GetContentId
    - (interfaccia) MIP:: TaskDispatcherDelegate
 
### <a name="new-requirements"></a>Nuovi requisiti
 - MIP:: ReleaseAllResources deve essere chiamato prima della terminazione del processo (dopo la cancellazione dei riferimenti a tutti i profili, motori e gestori)
 - (Interface) MIP:: ExecutionState:: GetClassificationResults tipo restituito e il parametro "classificationIds" è stato modificato
 - (Interface) MIP:: FileExecutionState:: GetAuditMetadata può essere implementato dalle applicazioni per specificare informazioni dettagliate per la superficie del dashboard di controllo di un amministratore tenant, ad esempio mittente, destinatari, Ultima modifica e così via.
 - (Interface) MIP:: FileExecutionState:: GetClassificationResults tipo restituito è stato modificato e ora richiede un parametro FileHandler
 - (Interface) MIP:: FileExecutionState:: GetDataState deve essere implementato dalle applicazioni per specificare la modalità di interazione di un'applicazione con contentIdentifier
 - (interfaccia) MIP:: HttpDelegate l'interfaccia richiede i metodi ' CancelOperation ' è CancelAllOperations '
 - (interfaccia) MIP:: HttpDelegate l'interfaccia ' Send ' è SendAsync ' restituiscono MIP:: HttpOperation anziché MIP:: HttpResponse
 - (interfaccia) MIP:: HttpResponse:: GetBody restituisce std:: Vector < uint8_t > anziché std:: String
 - (Interface) MIP:: HttpResponse l'interfaccia richiede l'implementazione del metodo ' GetId '
 - MIP:: ContentLabel:: GetCreationTime restituisce std:: Chrono:: time_point anziché std:: String
 - MIP:: fileengine:: CreateFileHandlerAsync non accetta più il parametro ' contentIdentifier '
 - MIP::P olicyHandler:: NotifyCommitedActions rinominato in MIP::P olicyHandler:: NotifyCommittedActions


## <a name="version-110"></a>Versione 1.1.0

**Data di rilascio**: 15 gennaio 2019

Questa versione introduce il supporto per le piattaforme seguenti:

  - .NET
  - iOS SDK (API criteri)
  - Android SDK (API per i criteri e API di protezione)

### <a name="new-features"></a>Nuove funzioni e caratteristiche

- Supporto di ADRMS
- Le operazioni dell'API di protezione sono realmente asincrone (su Win32), consentendo operazioni di crittografia/decrittografia simultanee non bloccanti
  - I callback dell'applicazione (AuthDelegate, HTTPDelegate e così via) possono ora essere richiamati in qualsiasi thread in background
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

### <a name="new-requirements"></a>Nuovi requisiti 

  - Popolamento applicato dei campi ID/nome/versione MIP:: ApplicationInfo durante la creazione di MIP:: fileprofile, MIP::P olicyProfile e MIP::P rotectionProfile
  - Per la creazione di MIP:: FileHandler, le applicazioni devono implementare la nuova interfaccia MIP:: FileExecutionState
  
### <a name="new-exceptions"></a>Nuove eccezioni 

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

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sulle piattaforme supportate e altro, vedere [domande frequenti e problemi relativi a MIP SDK](faqs-known-issues.md) .
- Per informazioni su come iniziare a usare l'SDK MIP, vedere [installazione e configurazione di MIP SDK](setup-configure-mip.md) .
