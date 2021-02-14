---
title: Cronologia delle versioni di Microsoft Information Protection (MIP) SDK e criteri di supporto
description: Cronologia delle versioni e note sulle modifiche per il MIP SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
ms.openlocfilehash: 52e43c9c0960ca5dadcd581db53bad2be2323b25
ms.sourcegitcommit: 0f694bf6c7ea9c7709954bfb5dbd1c5f009b85a7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2021
ms.locfileid: "100360348"
---
# <a name="microsoft-information-protection-mip-software-development-kit-sdk-version-release-history-and-support-policy"></a>Cronologia delle versioni di Microsoft Information Protection (MIP) Software Development Kit (SDK) e criteri di supporto

## <a name="servicing"></a>Servizio

Ogni versione disponibile a livello generale è supportata per un anno dopo il rilascio della prossima versione GA. La documentazione potrebbe non includere informazioni sulle versioni non supportate. Le correzioni e le nuove funzionalità sono applicabili solo alla versione GA più recente.

Le versioni di anteprima non devono essere distribuite nell'ambiente di produzione. Usare invece la versione di anteprima più recente per testare nuove funzionalità o correzioni che saranno disponibili nella prossima versione GA. È supportata solo la versione di anteprima più recente.

## <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per visualizzare le novità o le modifiche per una versione supportata. La versione più recente è elencata per prima.

> [!NOTE]
> Le correzioni minime non sono elencate. Se si verifica un problema con l'SDK, è consigliabile verificare se è stato risolto con la versione GA più recente. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, visitare il [forum stack overflow Microsoft Information Protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection).

## <a name="version-1894"></a>Versione 1.8.94

**Data di rilascio:** 8 febbraio 2021

- Correzione del bug nel pacchetto NuGet in cui la configurazione di debug per i progetti C++ distribuiva i binari della versione. 
- Correzione di un bug per cui il motore dei criteri era necessario per rimuovere la protezione. 
  - Se non è possibile caricare il motore dei criteri e i metadati delle etichette sono presenti, verranno eliminati se la protezione viene rimossa. 
- Correzione di un bug `labelInfo.xml` in cui è stato generato Empty se il file è stato modificato in un'altra etichetta protetta. 

## <a name="version-1886"></a>Versione 1.8.86

**Data di rilascio:** 13 gennaio, 2021

### <a name="general-changes"></a>Modifiche generali

- Aggiunta del supporto per Mac su ARM.
- Firma di tutti i file dylib per Mac.
- Tutti i cloud sono completamente supportati in tutti e tre gli SDK.
- Rinominare `TelemetryConfiguration` con `DiagnosticConfiguration`.
- Aggiornato `MipContext` per accettare `DiagnosticConfiguration` anziché `TelemetryConfiguration` .
- Nuovi `TelemetryDelegate` e esposti `AuditDelegate` .
- Il nome di diverse impostazioni personalizzate è stato modificato e verrà rimosso nella versione 1,9. Che continueranno a funzionare in parallelo con i nomi degli aggiornamenti nella versione 1,8. 

| Nuovo nome          | Nome precedente                   |
| ----------------- | -------------------------- |
| is_debug_audit    | is_debug_telemetry         |
| is_audit_disabled | is_built_in_audit_disabled |

### <a name="file-sdk"></a>SDK file

- Aggiunta del supporto per le etichette definite dall'utente con crittografia a chiave doppia.
- Aggiunta di un'API `MsgInspector.BodyType` per esporre il tipo di codifica del corpo per i file msg.
- Sono state aggiunte API per supportare la crittografia a chiave doppia con autorizzazioni User-Defined.
- Aggiunta del flag per `mip::FileHandler` che consente al chiamante di disabilitare l'invio di eventi di individuazione del controllo. Questo consente di correggere uno scenario in cui l'uso dell' `ClassifyAsync()` API genera eventi di individuazione duplicati.
- Correzione dei bug nei casi seguenti: 
  - L'impostazione della protezione nel file XPS non riesce.
  - Non è possibile aprire un file dopo il caricamento/download da SharePoint Online e la rimozione delle autorizzazioni personalizzate.
  - `RemoveProtection()` la funzione accetterebbe un input Message. rpmsg. Ora accetta solo i file MSG.
  - Arresto anomalo che si è verificato durante il tentativo di rilevare o revocare i file non protetti.

### <a name="policy-sdk"></a>SDK criteri

- Rimosso `ActionId` dalle proprietà predefinite dei metadati per garantire la coerenza tra Microsoft Office e i documenti con etichetta SharePoint Online.
- Aggiunta del supporto per le etichette specifiche di Azure per le competenze.
- Aggiunta la possibilità di eseguire l'override dei dati di telemetria e del controllo tramite delegati per ogni
  - Il delegato di controllo offre la possibilità di inviare eventi di controllo AIP a una destinazione diversa da AIP Analytics o in aggiunta a AIP Analytics.
- Aggiunta del flag per `mip::PolicyHandler` che consentirà al chiamante di individuare l'invio dell'evento di individuazione del controllo. Questo consente di correggere uno scenario in cui l'uso dell' `ClassifyAsync()` API genera eventi di individuazione duplicati.
- Correzione di un bug in cui non è stato possibile aprire il database dei criteri crittografati in determinati scenari.
- Esposto nuovo `AuditDelegate` che consente agli sviluppatori di eseguire l'override della pipeline di controllo predefinita MIP SDK e di inviare eventi alla propria infrastruttura. 
- `mip::ClassifierUniqueIdsAndContentFormats` e `GetContentFormat()` ora restituiscono `std::string` anziché `mip::ContentFormat` . Questa modifica viene replicata nei wrapper .NET e Java. 
- `ContentFormat.Default` è ora `ContentFormat.File` .

### <a name="protection-sdk"></a>SDK di protezione

- Aggiunta di una `ProtectionEngineSettings.SetAllowCloudServiceOnly` proprietà che vieterà le connessioni ai cluster Active Directory Rights Management Services se true. Verranno utilizzati solo gli ambienti cloud.
- Aggiunta del supporto per l'acquisizione delle licenze di delega.
  - Le licenze di delega consentono ai servizi di recuperare una licenza per il contenuto per conto di un utente.
  - Questo consente al servizio di visualizzare i dati sui diritti e di decrittografare per conto dell'utente senza ulteriori chiamate al servizio.  

### <a name="java-wrapper-public-preview"></a>Wrapper Java (anteprima pubblica)

- Aggiunta del supporto per Track and Revoke to Java wrapper.
- Aggiunta del supporto del flusso al wrapper Java

### <a name="c-api"></a>API C

- Rimosso **MIP_FLIGHTING_FEATURE_KEEP_PDF_LINEARIZATION** flag dall'API C.

## <a name="version-17147"></a>Versione 1.7.147

### <a name="file-sdk"></a>SDK file

- Correzione di bug secondari per il formato di file PBIX. 

## <a name="version-17145"></a>Versione 1.7.145

**Data di rilascio:** 13 novembre, 2020

### <a name="general-changes"></a>Modifiche generali

- Aggiornamento del pacchetto NuGet per la copia delle dipendenze solo in aggiornamento anziché sempre.
- La configurazione di debug in .NET utilizzerà la versione di rilascio delle librerie native. È stato rilevato che i clienti che distribuiscono soluzioni .NET in modalità di debug a server remoti sono necessari per installare il runtime di debug di VC + +, operazione non semplice. Se è necessario eseguire il debug nelle librerie native, copiare le dll da SDK Redistributable nella cartella del progetto (https://ala.ms/mipsdkbins)
- Correzione di un bug che generava avvisi per i progetti .NET Core.

## <a name="version-17133"></a>Versione 1.7.133

**Data di rilascio**: 23 settembre 2020

### <a name="general-sdk-changes"></a>Modifiche generali dell'SDK

- Anteprima pubblica disponibile per Java in Windows e Ubuntu 18,04.
- .NET Core è ora supportato in Windows.
- Supporto per l'anteprima pubblica per .NET Core in Ubuntu 18,04.
- Registrazione locale migliorata per l'archivio chiavi quando il tipo di cache di archiviazione è impostato su `OnDiskEncrypted.`
- Funzionalità di flighting abilitata per il wrapper .NET
- Il comportamento di telemetria SDK è stato ripristinato prima di 1,6. Un set minimo di eventi di utilizzo viene ora inviato quando si opta per solo la telemetria minima.

### <a name="file-sdk"></a>SDK file

- Correzione della conversione del corpo UTF-16/UTF-8 in `MSGInspector` .
- Impostare un limite di dimensioni massime del file predefinito per i file protetti da file SDK a 6 GB.
  - Modifica apportata a causa della decrittografia dei file di grandi dimensioni che richiedono *almeno la dimensione* del file nella memoria disponibile.
  - È possibile eseguire l'override dell'impostazione personalizzata `max_file_size_for_protection` .
- Aggiunta del supporto per i PDF linearizzati.
- Correzione di un bug in cui LastModifiedDate non è stato aggiornato in caso di modifica.
- Correzione di una perdita di memoria nella creazione di PDF protetti.
- File SDK supporta la revoca dei file rilevati.
- `FileEngine::Settings::SetLabelFilter` è deprecato. in `ConfigureFunctionality` alternativa, usare.

### <a name="policy-sdk"></a>SDK criteri

- Policy SDK supporta ora le azioni di assegnazione di etichette solo per la crittografia.
- Correzione di un bug `mip::Identity` per cui non veniva caricato correttamente dai motori memorizzati nella cache.
- Correzione di un bug per cui i confronti dei GUID di classificazione fanno distinzione tra maiuscole e minuscole nell'API
- Gli eventi di controllo sono stati arricchiti aggiungendo nuovi campi.

### <a name="protection-sdk"></a>SDK di protezione

- Correzione di un bug `mip::Identity` per cui non veniva caricato correttamente dai motori memorizzati nella cache.
- Aggiunta della registrazione implicita per le licenze di pubblicazione appena create.
- Aggiunta del supporto per gli algoritmi di crittografia usati per supportare DKE nei file di Office.
- I `documentId` parametri e sono `owner` facoltativi.

### <a name="c-apis"></a>API C

- Sono state aggiunte le API DKE e Identity mancanti.
- Spostato `AuthDelegate` dal profilo al motore in tutti gli SDK.
- Pubblicare l'esempio di SDK dei criteri per C
- `MIP_CC_CreateProtectionEngineSettingsWithIdentity` è stato deprecato. in `MIP_CC_CreateProtectionEngineSettingsWithIdentityAndAuthCallback` alternativa, usare.
- `MIP_CC_CreateProtectionEngineSettingsWithEngineId` è stato deprecato. in `MIP_CC_CreateProtectionEngineSettingsWithEngineIdAndAuthCallback` alternativa, usare.
- `MIP_CC_CreateProtectionProfileSettings` la firma è stata modificata.
- `MIP_CC_CreatePolicyEngineSettingsWithIdentity` è stato deprecato, usare `MIP_CC_CreatePolicyEngineSettingsWithIdentityAndAuthCallback` .
- `MIP_CC_CreatePolicyEngineSettingsWithEngineId` è stato deprecato, usare `MIP_CC_CreatePolicyEngineSettingsWithEngineIdAndAuthCallback` .
- `MIP_CC_PolicyEngineSettings_SetLabelFilter` è stato deprecato, usare `MIP_CC_PolicyEngineSettings_ConfigureFunctionality` .
- `MIP_CC_CreatePolicyProfileSettings` la firma è stata modificata.

### <a name="breaking-changes"></a>Modifiche di rilievo

#### <a name="common"></a>Comuni

- `TelemetryConfiguration::isTelemetryOptedOut` è stato rinominato in `isMinimalTelemetryEnabled`. 

#### <a name="c-api"></a>API C

- `mip_cc_document_state` è stato aggiornato con un nuovo valore `mip_cc_metadata_version_format` contentMetadataVersionFormat

## <a name="version-16103"></a>Versione 1.6.103

**Data di rilascio**: 16 aprile 2020

### <a name="general-sdk-changes"></a>Modifiche generali dell'SDK

- TLS 1,2 applicato per tutte le comunicazioni HTTP non ADRMS.
- Implementazione HTTP iOS/macOS di cui è stata eseguita la migrazione da NSURLConnection a NSURLSession.
- Componente di telemetria iOS migrato da aria SDK a 1DS SDK.
- Il componente di telemetria USA ora HttpDelegate di MIP in iOS, macOs e Linux. (In precedenza solo Win32).
- Miglioramento dell'indipendenza dai tipi per l'API C.
- Il AuthDelegate è stato spostato dal profilo al motore nelle API C++, C# e Java.
- AuthDelegate spostato dal costruttore di `Profile::Settings` a `Engine::Settings` .
- Aggiunta della categoria a NoPolicyError per fornire altre informazioni sui motivi per cui la sincronizzazione dei criteri non è riuscita.
- Aggiunto `PolicyEngine::GetTenantId` metodo.
- Aggiunta del supporto esplicito per tutti i cloud.
  - Nuovo `Engine::Settings::SetCloud` metodo per impostare il cloud di destinazione (GCC High, 21-Viani e così via).
  - La `Engine::Settings::SetCloudEndpointBaseUrl` chiamata al metodo esistente non è più necessaria per i cloud riconosciuti.
- Abilitazione di bitcode per i file binari iOS.

### <a name="file-sdk"></a>SDK file

- Aggiunta `IFileHandler::InspectAsync` ai wrapper C# e Java
- Nuovo supporto tramite `FileProfile::AcquirePolicyAuthToken` per l'attivazione dell'acquisizione dei token di criteri per consentire a un'applicazione di eseguire il riscaldamento della cache dei token.    
- `MsgInspector::GetAttachments` restituisce `vector<shared_ptr<MsgAttachmentData>>` anziché `vector<unique_ptr<MsgAttachmentData>>`
- `TelemetryConfiguration::isOptedOut` l'impostazione ora Disabilita completamente la telemetria. In precedenza è stato inviato un set di dati di telemetria minimi.

### <a name="policy-sdk"></a>SDK criteri

- Nuovo supporto per l'attivazione dell'acquisizione di token per consentire a un'applicazione di eseguire il riscaldamento della cache dei token tramite `PolicyProfile::AcquireAuthToken` .
- Per impostazione predefinita, le etichette HYOK sono filtrate.
- I metadati associati alle etichette eliminate verranno ora rimossi.
- In caso di mancata corrispondenza tra i criteri di etichetta memorizzati nella cache e i criteri di riservatezza, la cache dei criteri verrà ora cancellata.
- Nuovo supporto per i metadati con versione:
  - Un formato di file può comparire la posizione o il formato dei metadati delle etichette. In tal caso, un'applicazione deve fornire MIP con tutti i metadati e MIP determinerà quali metadati sono "true".
  - `ContentLabel::GetExtendedProperties` restituisce ora `vector<MetadataEntry>` invece di `vector<pair<string, string>>` .
  - `MetadataAction::GetMetadataToAdd` restituisce ora `vector<MetadataEntry>` invece di `vector<pair<string, string>>` .
  - `ExecutionState::GetContentMetadata` dovrebbe ora restituire `vector<MetadataEntry>` anziché `vector<pair<string, string>>` .
  - `ExecutionState::GetContentMetadataVersion` deve restituire la versione più recente dei metadati riconosciuta dall'applicazione per il formato di file corrente (in genere 0).
  - `PolicyEngine::GetWxpMetadataVersion` Restituisce la versione dei metadati per i documenti di Office configurata dall'amministratore del tenant (0 = impostazione predefinita, 1 = formato abilitato per la coautenticazione).
  - Modifiche equivalenti nell'API C:
    - `MIP_CC_ContentLabel_GetExtendedProperties`
    - `MIP_CC_MetadataAction_GetMetadataToAdd`
    - `mip_cc_metadata_callback`
    - `mip_cc_document_state`
    - `MIP_CC_PolicyEngine_GetWxpMetadataVersion`
- `TelemetryConfiguration::isOptedOut` l'impostazione ora Disabilita completamente la telemetria. In precedenza è stato inviato un set di dati di telemetria minimi. 

### <a name="protection-sdk"></a>SDK di protezione

- Nuovo supporto per la registrazione e la revoca per il rilevamento dei documenti.
- Nuovo supporto per la generazione di una licenza preliminare durante la pubblicazione.
- Certificato Microsoft TLS pubblico esposto utilizzato dal servizio di protezione.
   - `GetMsftCert` e `GetMsftCertPEM`
   - Se un'applicazione esegue l'override dell' `HttpDelegate` interfaccia, deve considerare attendibili i certificati del server rilasciati da questa CA.
   - Questo requisito dovrebbe essere rimosso in ritardo nel 2020.    

## <a name="version-15124"></a>Versione 1.5.124

**Data di rilascio**: 2 marzo 2020

### <a name="general-sdk-changes"></a>Modifiche generali dell'SDK

- API Java (solo Windows)
- Annullamento di attività MIP asincrone
  - Tutte le chiamate asincrone restituiscono l'oggetto MIP:: AsyncControl con un metodo Cancel ()
- Caricamento ritardato dei file binari dipendenti
- Facoltativamente, mascherare le proprietà di telemetria/controllo specifiche
   - Configurabile tramite MIP:: TelemetryConfiguration:: maskedProperties
- Eccezioni migliorate:
  - Tutti gli errori includono ID di correlazione di utilità pratica nella stringa di descrizione
  - Errore di rete con campi ' Category ',' BaseUrl ',' RequestId ' è StatusCode '
- Miglioramento del risultato dell'API C/dettagli dell'errore

### <a name="file-sdk"></a>SDK file

- Verifica senza rete se il file è con etichetta o protetto
  - MIP:: FileHandler:: IsLabeledOrProtected ()
  - Rischio minore di falsi positivi (ad esempio se il file contiene metadati dell'etichetta zombie)
- Filtrare le etichette associate a tipi specifici di protezione
  - Configurabile tramite MIP:: fileengine:: Settings:: SetLabelFilter ()
- Esporre i dati dei criteri all'API file
  - MIP:: fileengine:: GetPolicyDataXml ()

### <a name="policy-sdk"></a>SDK criteri

- Contrassegno del contenuto dinamico per le azioni filigrana/intestazione/piè di pagina:
  - I campi come $ {Item. Label}, $ {Item.Name}, $ {User.Name}, $ {Event. DateTime} verranno popolati automaticamente da MIP
  - MIP:: Identity può essere costruito con un campo "nome" descrittivo usato dal contrassegno di contenuto dinamico
  - Configurabile tramite MIP::P olicyEngine:: Settings:: SetVariableTextMarkingType ()
- Verifica senza rete se il contenuto è etichettato
  - MIP::P olicyHandler:: etichettato ()
  - Rischio minore di falsi positivi (ad esempio se il contenuto contiene metadati dell'etichetta zombie)
- Valore TTL cache criteri etichetta
  - Impostazione predefinita: 30 giorni
  - Configurabile tramite MIP::P olicyProfile:: SetCustomSettings ()
- **Modifica di rilievo**
  - Aggiornamento di PolicyEngine. Settings. LabelFilter dall'elenco di enumerazioni a Nullable bit.

### <a name="protection-sdk"></a>SDK di protezione

- Pre-licenza
  - L'esistenza di una pre-licenza insieme al contenuto crittografato, insieme a un certificato utente recuperato in precedenza, consente la decrittografia offline del contenuto
  - MIP::P rotectionHandler:: ConsumptionSettings può essere costruito con una licenza preliminare
  - MIP::P rotectionEngine:: LoadUserCert | Async () Recupera il certificato utente archiviato in base a MIP::P criteri di memorizzazione nella cache di rotectionProfile
- Verifica delle funzionalità specifiche del server
  - Verifica se il tenant dell'utente supporta la funzionalità "solo crittografia" (disponibile solo in Azure RMS)
  - MIP::P rotectionEngine:: IsFeatureSupported ()
- Dettagli più completi durante il recupero dei modelli RMS
- **Modifiche di rilievo**
  - `mip::ProtectionEngine::GetTemplates()``vector<shared_ptr<string>>`valore restituito sostituito con `vector<shared_ptr<mip::TemplateDescriptor>>` (C++)
  - `mip::ProtectionEngine::Observer::OnGetTemplatesSuccess()``shared_ptr<vector<string>>`parametro di callback sostituito con `vector<shared_ptr<mip::TemplateDescriptor>>` (C++)
  - IProtectionEngine. gettemplates | Il valore restituito Async () è stato `List<string>` sostituito con `List<TemplateDescriptor>` . (C#)
  - MIP_CC_ProtectionEngine_GetTemplates () mip_cc_guid * param sostituito con mip_cc_template_descriptor * (API C)

### <a name="c-api"></a>API C

- **Modifiche di rilievo**: la maggior parte delle funzioni per includere mip_cc_error * parametro può essere null
  

### <a name="errorexception-updates"></a>Aggiornamenti errori/eccezioni

- Riepilogo gestione errori:
  - AccessDeniedError: all'utente non sono stati concessi i diritti per accedere al contenuto
      - NoAuthTokenError: l'app non ha fornito il token di autenticazione
      - NoPermissionsError: all'utente non sono stati concessi i diritti per contenuto specifico, ma è disponibile un referrer/un proprietario
      - ServiceDisabledError: il servizio è disabilitato per utente/dispositivo/piattaforma/tenant
  - AdhocProtectionRequiredError: è necessario impostare la protezione ad hoc prima di impostare un'etichetta
  - BadInputError: input non valido da utente/app
      - InsufficientBufferError: input del buffer non valido da utente/app
      - LabelDisabledError: l'ID etichetta è riconosciuto ma disabilitato per l'uso
      - LabelNotFoundError: ID etichetta non riconosciuto
      - TemplateNotFoundError: ID modello non riconosciuto
  - ConsentDeniedError: non è stato concesso il consenso a un'operazione che richiede il consenso dell'utente o dell'app
  - DeprecatedApiError: questa API è stata deprecata
  - FileIOError: non è stato possibile leggere/scrivere il file
  - InternalError: errore interno imprevisto
  - NetworkError
      - ProxyAuthenticationError: è richiesta l'autenticazione proxy
    - Category = BadResponse: il server ha restituito una risposta HTTP illeggibile (il tentativo potrebbe avere esito positivo)
    - Categoria = annullata: non è stato possibile stabilire una connessione HTTP perché l'operazione è stata annullata dall'utente o dall'app.
    - Category = FailureResponseCode: il server ha restituito una risposta di errore generico (il tentativo potrebbe avere esito positivo)
    - Categoria = NOCONNECTION: non è stato possibile stabilire la connessione HTTP (il tentativo potrebbe avere esito positivo)
    - Categoria = offline: non è stato possibile stabilire la connessione HTTP perché l'applicazione è in modalità offline (il tentativo non riesce)
    - Categoria = proxy: non è stato possibile stabilire una connessione HTTP a causa di un problema del proxy (il tentativo potrebbe probabilmente non riuscire)
    - Categoria = SSL: non è stato possibile stabilire una connessione HTTP a causa di un problema SSL (probabilmente il tentativo non riuscirà)
    - Categoria = limitato: il server ha restituito una risposta "limitata" (backoff/Retry avrà probabilmente esito positivo)
    - Categoria = timeout: non è stato possibile stabilire una connessione HTTP dopo il timeout (il tentativo avrà probabilmente esito positivo)
    - Category = UnexpectedResponse: il server ha restituito dati imprevisti (il tentativo potrebbe avere esito positivo)
  - NoPolicyError: il tenant o l'utente non è configurato per le etichette
  - NotSupportedError: operazione non supportata nello stato corrente
  - OperationCancelledError: operazione annullata
  - PrivilegedRequiredError: non è possibile modificare l'etichetta a meno che il metodo di assegnazione = privilegiato
- Modifiche
  - Rimossi PolicySyncError inutilizzati. Sostituito da NetworkError
  - Rimossi TransientNetworkError inutilizzati. Sostituito da categorie NetworkError

## <a name="version-140"></a>Versione 1.4.0 

**Data di rilascio**: 6 novembre 2019

Questa versione introduce il supporto per l'SDK di protezione nel pacchetto .NET (Microsoft. InformationProtection. file).

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
- Rimossi mip_telemetry.dll (Uniti in mip_core.dll)

### <a name="file-sdk"></a>SDK file

- RPMSG
  - Crittografia
  - Aggiunta del supporto per la decrittografia String8
- Comportamento dell'estensione PFILE configurabile (impostazione predefinita: <EXT> . PFILE o P <EXT> )
  - ProtectionSettings::SetPFileExtensionBehavior

### <a name="policy-sdk"></a>SDK criteri

- API C completa
- Configurare il filtraggio delle etichette associate alla protezione
  - PolicyEngine:: impostazioni:: SetLabelFilter ()

### <a name="protection-sdk"></a>SDK di protezione

- Sono state rimosse le API deprecate in precedenza
  - Rimozione di ProtectionEngine:: CreateProtectionHandlerFromDescriptor [async] (usare ProtectionEngine:: CreateProtectionHandlerForPublishing [async])
  - Rimozione di ProtectionEngine:: CreateProtectionHandlerFromPublishingLicense [async] (usare ProtectionEngine:: CreateProtectionHandlerForConsumption [async])
- Completa API C#
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
- Il controllo dei file Message. rpmsg è supportato tramite `mip::FileInspector` e `mip::FileHandler::InspectAsync()` .
- È ora possibile crittografare facoltativamente la cache su disco.
- Protection SDK supporta ora i clienti cloud cinesi.
- Supporto di Arm64 in Android.
- Supporto di Arm64e in iOS.
- È ora possibile disabilitare la cache del contratto di licenza con l'utente finale.
- . la crittografia Pfile può essere disabilitata tramite `mip::FileEngine::EnablePFile`
- Miglioramento delle prestazioni per le operazioni di protezione mediante la riduzione del numero di chiamate HTTP
- Rimossi i dettagli dell'identità delegata da `mip::Identity` e aggiunti `DelegatedUserEmail` a `mip::FileEngine::Settings` , `mip::ProtectionSettings` , e e `mip::PolicyEngine::Settings` `mip::ProtectionHandler` `PublishingSettings` `ConsumptionSettings` .
- Le funzioni che in precedenza restituivano LabelId ora restituiscono un `mip::Label` oggetto.

### <a name="changes"></a>Modifiche

* Nelle versioni precedenti è necessario chiamare `mip::ReleaseAllResources` . La versione 1,3 sostituisce questa operazione con `mip::MipContext::~MipContext` o `mip::MipContext::Shutdown` .
* Rimosso `ActionSource` da `mip::LabelingOptions` e `mip::ExecutionState::GetNewLabelActionSource`
* Sostituito `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` con `mip::ProtectionEngine::CreateProtectionHandlerForPublishing` .
* Sostituito `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` con `mip::ProtectionEngine::CreateProtectionHandlerForConsumption` .
* Ridenominazione `mip::PublishingLicenseContext` in `mip::PublishingLicenseInfo` e aggiornata per contenere campi avanzati anziché byte serializzati non elaborati.
* `mip::PublishingLicenseInfo` contiene i dati rilevanti per MIP dopo l'analisi di una licenza di pubblicazione (PL).
* `mip::TemplateNotFoundError` e `mip::LabelNotFoundError` generata quando l'applicazione passa MIP un ID modello o un ID etichetta non riconosciuto.
* Aggiunta del supporto per l'accesso condizionale basato su etichetta tramite il parametro claims di `AcquireToken()` e `mip::AuthDelegate::OAuth2Challenge()` . Questa funzionalità non è stata ancora esposta tramite il portale del Centro sicurezza e conformità.


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

 - mip_common.dll suddivisi in mip_core.dll e mip_telemetry.dll.
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
    - MIP:: HttpRequest:: GetBody restituisce std:: Vector<uint8_t> anziché std:: String
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
 - (Interface) MIP:: FileExecutionState:: GetAuditMetadata può essere implementato dalle applicazioni per specificare informazioni dettagliate per la superficie del dashboard di controllo di un amministratore tenant (ad esempio, mittente, destinatari, Ultima modifica e così via)
 - (Interface) MIP:: FileExecutionState:: GetClassificationResults tipo restituito è stato modificato e ora richiede un parametro FileHandler
 - (Interface) MIP:: FileExecutionState:: GetDataState deve essere implementato dalle applicazioni per specificare la modalità di interazione di un'applicazione con contentIdentifier
 - (interfaccia) MIP:: HttpDelegate l'interfaccia richiede i metodi ' CancelOperation ' è CancelAllOperations '
 - (interfaccia) MIP:: HttpDelegate l'interfaccia ' Send ' è SendAsync ' restituiscono MIP:: HttpOperation anziché MIP:: HttpResponse
 - (interfaccia) MIP:: HttpResponse:: GetBody restituisce std:: Vector<uint8_t> anziché std:: String
 - (Interface) MIP:: HttpResponse l'interfaccia richiede l'implementazione del metodo ' GetId '
 - MIP:: ContentLabel:: GetCreationTime restituisce std:: Chrono:: time_point anziché std:: String
 - MIP:: fileengine:: CreateFileHandlerAsync non accetta più il parametro ' contentIdentifier '
 - MIP::P olicyHandler:: NotifyCommitedActions rinominato in MIP::P olicyHandler:: NotifyCommittedActions


## <a name="version-110"></a>Versione 1.1.0 

**Data di rilascio**: 15 gennaio 2019

Questa versione introduce il supporto per le piattaforme seguenti:

  - .NET
  - iOS SDK (Policy SDK)
  - Android SDK (Policy SDK and Protection SDK)

### <a name="new-features"></a>Nuove funzioni e caratteristiche

- Supporto di ADRMS
- Le operazioni di Protection SDK sono realmente asincrone (su Win32), consentendo operazioni di crittografia/decrittografia simultanee non bloccanti
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
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - MIP:: NoPolicyError generato se il tenant non è configurato per le etichette
    - Si applica alla creazione di:
      - mip::FileEngine
      - mip::PolicyEngine
  - MIP:: ServiceDisabledError generata se il servizio RMS è disabilitato per un utente/dispositivo/piattaforma/tenant specifico
    - Si applica alla creazione di:
      - mip::FileHandler
      - mip::ProtectionHandler
  - MIP:: NoPermissionsError generata se un utente non dispone dei diritti per decrittografare un documento o il contenuto è scaduto
    - Si applica alla creazione di:
      - mip::FileHandler
      - mip::ProtectionHandler

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sulle piattaforme supportate e altro, vedere [domande frequenti e problemi relativi a MIP SDK](faqs-known-issues.md) .
- Per informazioni su come iniziare a usare l'SDK MIP, vedere [installazione e configurazione di MIP SDK](setup-configure-mip.md) .
