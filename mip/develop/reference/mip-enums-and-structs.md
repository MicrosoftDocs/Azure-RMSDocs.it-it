---
title: Strutture e enumerazioni di riferimento di MIP SDK per C++
description: Documentazione di riferimento per gli struct e le enumerazioni di C++ SDK MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: e602b13ce5dedb8ff210372d1d06e03625611e0e
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214100"
---
# <a name="enumerations-and-structures"></a>Enumerazioni e strutture


Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
WatermarkLayout enum       |  Layout per le filigrane.
ContentMarkAlignment enum       |  Allineamento per i contrassegni di contenuto (intestazione del contenuto o piè di pagina del contenuto).
AssignmentMethod enum       |  Metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come operazione con privilegi (equivalente a un'operazione di amministratore).
ActionSource enum       |  definisce ciò che ha attivato l'evento di etichettatura
DataState enum       |  Definisce lo stato dei dati su cui si sta eseguendo l'applicazione.
ContentFormat enum       |  Formato del contenuto.
LabelFilterType enum       |  Tipi di filtro etichette, set facoltativo di proprietà che possono essere usate per filtrare le etichette quando si chiamano etichette di riservatezza degli elenchi.
FeatureId enum       |  Definisce nuove funzionalità in base al nome.
VariableTextMarkingType enum       |  è possibile impostare vari campi dinamici nel messaggio di testo dell'applicazione: $ {Item. Label} $ {Item.Name} $ {Item. location} $ {User.Name} $ {User. PrincipalName} $ {Event. DateTime} other non è ancora definito: l'SDK li sostituirà con i valori corretti usando questi flag di controllo.
enum Consent       |  Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
CacheStorageType enum       |  Tipo di archiviazione per le cache.
PFileExtensionBehavior enum       |  Descrive il comportamento delle estensioni PFile.
enum ErrorType       | _Non ancora documentato._
InspectorType enum       |  Tipo di controllo correlato ai tipi di file supportati.
BodyType enum       |  Enumeratore del tipo di corpo.
FlightingFeature enum       |  Definisce nuove funzionalità in base al nome.
enum HttpRequestType       |  Tipo di richiesta HTTP.
enum LogLevel       |  Diversi livelli di log usati in MIP SDK.
enum ProtectionType       |  Indica se la protezione si basa un modello o è ad hoc (personalizzata)
enum ActionType       |  Tipi di azioni diversi.
LabelState enum       | _Non ancora documentato._
ActionDataType enum       | _Non ancora documentato._
ConditionDataType enum       | _Non ancora documentato._
ContentMarkPlacement enum       | _Non ancora documentato._
LabelActionDataType enum       | _Non ancora documentato._
ProtectionActionType enum       | _Non ancora documentato._
struct MIP:: ApplicationInfo  |  Struct che include informazioni specifiche dell'applicazione.
struct MIP:: TelemetryConfiguration  |  Impostazioni di telemetria personalizzate (non usate comunemente)

## <a name="enumerations"></a>Enumerazioni

### <a name="watermarklayout-enum"></a>Enumerazione WatermarkLayout
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ORIZZONTALE            | Il layout della filigrana è orizzontale
DIAGONALE            | Il layout della filigrana è diagonale

Layout per le filigrane.
  
### <a name="contentmarkalignment-enum"></a>Enumerazione ContentMarkAlignment
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
LEFT            | Il contrassegno del contenuto è allineato a sinistra
RIGHT            | Il contrassegno del contenuto è allineato a destra
CENTER            | Il contrassegno del contenuto è centrato

Allineamento per i contrassegni di contenuto (intestazione del contenuto o piè di pagina del contenuto).
  
### <a name="assignmentmethod-enum"></a>Enumerazione AssignmentMethod
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
STANDARD            | Il metodo di assegnazione etichette è standard
CON privilegi            | Il metodo di assegnazione etichetta è con privilegi
AUTO            | Il metodo di assegnazione etichette è automatico

Metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come operazione con privilegi (equivalente a un'operazione di amministratore).
  
### <a name="actionsource-enum"></a>Enumerazione ActionSource
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
MANUAL            | Selezionato manualmente dall'utente
AUTOMATIC            | Imposta da condizioni dei criteri
CONSIGLIABILE            | Impostato dall'utente dopo la raccomandazione dell'etichetta per le condizioni dei criteri
DEFAULT            | Impostazione predefinita nei criteri

Definisce ciò che ha attivato l'evento di etichettatura
  
### <a name="datastate-enum"></a>Enum di DataState
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
REST            | Dati inattivi archiviati fisicamente in database/file/warehouse
MOVIMENTO            | Dati che attraversano una rete o che risiedono temporaneamente nella memoria del computer per la lettura o l'aggiornamento
USE            | Dati attivi con modifiche costanti archiviati fisicamente in database/file/warehouse e così via

Definisce lo stato dei dati su cui si sta eseguendo l'applicazione.
  
### <a name="contentformat-enum"></a>Enumerazione ContentFormat
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
DEFAULT            | Il formato del contenuto è il formato di file standard
Posta elettronica            | Il formato del contenuto è formato posta elettronica

Formato del contenuto.
  
### <a name="labelfiltertype-enum"></a>Enumerazione LabelFilterType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
nessuno            | Disabilita filtro etichette predefinito
CustomProtection            | Filtrare le etichette che possono causare la protezione personalizzata
TemplateProtection            | Filtrare le etichette che possono causare la mancata esecuzione
DoNotForwardProtection            | Filtrare le etichette che possono causare la protezione del modello
AdhocProtection            | Filtrare le etichette che possono causare la protezione ad hoc
HyokProtection            | Filtrare le etichette che possono causare la protezione Hyok
PredefinedTemplateProtection            | Filtrare le etichette che possono comportare la protezione modello predefinita
DoubleKeyProtection            | Filtrare le etichette che possono comportare la protezione che richiede la doppia chiave, può essere template, Adhoc, DNF

Tipi di filtro etichette, set facoltativo di proprietà che possono essere usate per filtrare le etichette quando si chiamano etichette di riservatezza degli elenchi.
  
### <a name="featureid-enum"></a>Enumerazione FeatureId
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
EncryptOnly            | Controllare se il server supporta la funzionalità EncryptOnly

Definisce nuove funzionalità in base al nome.
  
### <a name="variabletextmarkingtype-enum"></a>Enumerazione VariableTextMarkingType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Predefinito            | I contrassegni noti vengono convertiti con contrassegno sconosciuto rimossi
Pass-through            | I contrassegni noti vengono convertiti con contrassegno sconosciuto vengono passati
nessuno            | Tutti i contrassegni vengono passati attraverso

È possibile impostare vari campi dinamici nel messaggio di testo dell'applicazione: $ {Item. Label} $ {Item.Name} $ {Item. location} $ {User.Name} $ {User. PrincipalName} $ {Event. DateTime} other non è ancora definito: l'SDK li sostituirà con i valori corretti usando questi flag di controllo.
  
### <a name="consent-enum"></a>Enum di consenso
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
AcceptAlways            | Fornisce il consenso e memorizza questa decisione
Accetta            | Fornisce il consenso una sola volta
Rifiuto            | Non fornisce il consenso

Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
  
### <a name="cachestoragetype-enum"></a>Enumerazione CacheStorageType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
InMemory            | Archiviazione in memoria
OnDisk            | Archiviazione su disco
OnDiskEncrypted            | Sull'archiviazione su disco con crittografia (se supportata dalla piattaforma)

Tipo di archiviazione per le cache.
  
### <a name="pfileextensionbehavior-enum"></a>Enumerazione PFileExtensionBehavior
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Predefinito            | Le estensioni diventeranno il comportamento predefinito di SDK
PFileSuffix            | Le estensioni diventeranno <EXT> . PFILE
PPrefix            | Le estensioni diventeranno P<EXT>

Descrive il comportamento delle estensioni PFile.
  
### <a name="errortype-enum"></a>Enumerazione ErrorType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | Il chiamante ha passato un input errato.
INSUFFICIENT_BUFFER_ERROR            | Il chiamante ha passato un buffer troppo piccolo.
FILE_IO_ERROR            | Errore di I/O file generale.
NETWORK_ERROR            | Problemi di rete generali; ad esempio, un servizio irraggiungibile.
INTERNAL_ERROR            | Errori imprevisti interni,
JUSTIFICATION_REQUIRED            | Per completare l'azione sul file, è necessario specificare una giustificazione.
NOT_SUPPORTED_OPERATION            | L'operazione richiesta non è ancora supportata.
PRIVILEGED_REQUIRED            | Non è possibile eseguire l'override dell'etichetta con privilegi quando il nuovo metodo di etichetta è standard.
ACCESS_DENIED            | L'utente non è riuscito a ottenere l'accesso ai servizi.
CONSENT_DENIED            | Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
NO_PERMISSIONS            | L'utente non è riuscito a ottenere l'accesso al contenuto, Ad esempio, nessuna autorizzazione, contenuto revocato
NO_AUTH_TOKEN            | L'utente non è riuscito a ottenere l'accesso al contenuto a causa di un token di autenticazione vuoto.
DISABLED_SERVICE            | L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione del servizio
PROXY_AUTH_ERROR            | Impossibile autenticare il proxy.
NO_POLICY            | Nessun criterio configurato per l'utente/tenant
OPERATION_CANCELLED            | Operazione annullata
ADHOC_PROTECTION_REQUIRED            | È necessario impostare la protezione ad hoc per completare l'azione sul file
DEPRECATED_API            | Il chiamante ha richiamato un'API deprecata
TEMPLATE_NOT_FOUND            | ID modello non riconosciuto
LABEL_NOT_FOUND            | ID etichetta non riconosciuto
LABEL_DISABLED            | Label disabilitato o inattivo
  
### <a name="inspectortype-enum"></a>Enumerazione InspectorType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Sconosciuto            | Controllo file sconosciuto.
Msg            | Controllo file di tipo msg, basato su rpmsg/msg.

Tipo di controllo correlato ai tipi di file supportati.
  
### <a name="bodytype-enum"></a>Enumerazione BodyType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
UNKNOWN            | Tipo di corpo sconosciuto
TXT            | Tipo di corpo dello stile del testo, la codifica viene restituita come UTF8
HTML            | Tipo di corpo dello stile HTML, la codifica viene restituita come UTF8
RTF            | Tipo di corpo dello stile RTF, formato binario

Enumeratore del tipo di corpo.
  
### <a name="flightingfeature-enum"></a>Enumerazione FlightingFeature
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | Utilizzare una chiamata HTTP separata per determinare gli endpoint di servizio RMS
AuthInfoCache            | Memorizzare nella cache le richieste OAuth2 per dominio/tenant per ridurre le risposte 401 non necessarie. Disabilitare per app/servizi che gestiscono la propria autenticazione HTTP (ad esempio, SPO, Edge)
LinuxEncryptedCache            | Abilitare la memorizzazione nella cache crittografata per le piattaforme Linux (leggere i prerequisiti per questa funzionalità)
SingleDomainName            | Abilitare il nome della singola società per la ricerca DNS. e.g. [https://corprights](https://corprights)
PolicyAuth            | Abilitare l'autenticazione HTTP automatica per le richieste inviate al servizio criteri. Disabilitare per app/servizi che gestiscono la propria autenticazione HTTP (ad esempio, SPO, Edge)
UrlRedirectCache            | Reindirizzamenti URL della cache per ridurre il numero di operazioni HTTP
Prelicenza            | Abilita controllo API pre-licenza
DoubleKey            | Abilitare la funzionalità di protezione con chiave doppia per usare una chiave cliente per la crittografia con
VariablePolicyTtl            | Abilitare la durata (TTL) dei criteri variabili, la disabilitazione Ripristina i criteri infiniti
VariableTextMarking            | Abilita contrassegno testo variabile

Definisce nuove funzionalità in base al nome.
  
### <a name="httprequesttype-enum"></a>Enumerazione HttpRequestType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Recupero            | GET
Pubblica            | POST

Tipo di richiesta HTTP.
  
### <a name="loglevel-enum"></a>Enumerazione LogLevel
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Avviso            | 
Errore            | 

Diversi livelli di log usati in MIP SDK.
  
### <a name="protectiontype-enum"></a>Enumerazione ProtectionType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
TemplateBased            | L'handle è stato creato da un modello
Personalizzato            | L'handle è stato creato ad hoc

Indica se la protezione si basa un modello o è ad hoc (personalizzata)
  
### <a name="actiontype-enum"></a>Enumerazione ActionType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | Aggiunge un piè di pagina contenuto al tipo di azione del documento.
ADD_CONTENT_HEADER            | Aggiunge un'intestazione contenuto al tipo di azione del documento.
ADD_WATERMARK            | Aggiunge una filigrana al tipo di azione dell'intero documento.
CUSTOM            | Tipo di azione definito personalizzato.
JUSTIFY            | Tipo di azione di allineamento.
METADATI            | Tipo di azione di modifica dei metadati.
PROTECT_ADHOC            | Tipo di azione di protezione con criteri ad hoc.
PROTECT_BY_TEMPLATE            | Tipo di azione di protezione con modello.
PROTECT_DO_NOT_FORWARD            | Tipo di azione di protezione senza inoltro.
REMOVE_CONTENT_FOOTER            | Tipo di azione di rimozione del piè di pagina contenuto.
REMOVE_CONTENT_HEADER            | Tipo di azione di rimozione dell'intestazione contenuto.
REMOVE_PROTECTION            | Tipo di azione di rimozione di agenti protezione.
REMOVE_WATERMARK            | Tipo di azione di rimozione della filigrana.
APPLY_LABEL            | Tipo di azione di applicazione dell'etichetta.
RECOMMEND_LABEL            | Tipo di azione di etichetta consigliata.
PROTECT_ADHOC_DK            | Tipo di azione di protezione con criteri ad hoc.
PROTECT_BY_TEMPLATE_DK            | Tipo di azione di protezione con modello.
PROTECT_DO_NOT_FORWARD_DK            | Tipo di azione di protezione senza inoltro.

Tipi di azioni diversi. CUSTOM è il tipo di azione generico. Ogni altro tipo di azione è un'azione specifica con un significato specifico.
  
### <a name="labelstate-enum"></a>Enumerazione LabelState
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
NoChange            | 
Rimuovi            | 
Aggiornamento            | 
  
### <a name="actiondatatype-enum"></a>Enumerazione ActionDataType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Personalizzato            | 
Protezione            | 
ContentMarking            | 
AddWatermark            | 
Etichetta            | 
  
### <a name="conditiondatatype-enum"></a>Enumerazione ConditionDataType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Predefinito            | 
Sensibilità            | 
  
### <a name="contentmarkplacement-enum"></a>Enumerazione ContentMarkPlacement
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Intestazione            | 
Piè di pagina            | 
  
### <a name="labelactiondatatype-enum"></a>Enumerazione LabelActionDataType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Recommend            | 
Applica            | 
  
### <a name="protectionactiontype-enum"></a>Enumerazione ProtectionActionType
Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Personalizzato            | 
Modello            | 
DoNotForward            | 
Adhoc            | 
DoNotForwardWithPrompt            | 
Hyok            | 
PredefinedTemplate            | 
RemoveProtection            | 
 

## <a name="structures"></a>Strutture

### <a name="struct-mipapplicationinfo"></a>struct MIP:: ApplicationInfo 
Struct che include informazioni specifiche dell'applicazione.
  
Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
public std::string applicationName  |  Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
public std::string applicationVersion  |  Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')
  

#### <a name="applicationid-struct-member"></a>membro struct applicationId
Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
  
#### <a name="applicationname-struct-member"></a>membro struct di ApplicationName
Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
  
#### <a name="applicationversion-struct-member"></a>membro struct applicationVersion
Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')

### <a name="struct-diagnosticconfiguration"></a>struct DiagnosticConfiguration

Configurazioni di diagnostica personalizzate (non usate comunemente)
  
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String hostNameOverride  |  Nome dell'istanza di controllo/telemetria host. Se non è impostato, MIP fungerà da host.
public std:: String libraryNameOverride  |  Nome file della libreria di controllo/telemetria (DLL) alternativo.
public std:: shared_ptr \<HttpDelegate\> httpDelegateOverride  |  Se impostato, la gestione HTTP verrà gestita da questa istanza
public std:: shared_ptr \<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di controllo/telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
public bool isNetworkDetectionEnabled  |  Se impostato, il componente di controllo/telemetria effettuerà il ping dello stato della rete sul thread in background
public bool isLocalCachingEnabled  |  Se impostato, il componente di controllo/telemetria utilizzerà la memorizzazione nella cache su disco
public bool isTraceLoggingEnabled  |  Se impostato, il componente di controllo/telemetria scriverà i log di avviso/errore sul disco
public bool isMinimalTelemetryEnabled  |  Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
public bool isFastShutdownEnabled  |  Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
public std:: Map \<std::string, std::string\> customSettings  |  Impostazioni di controllo/telemetria personalizzate >
public std:: Map \<std::string, std::vector\<std::string\> \> maskedProperties  |  Eventi/proprietà di controllo/telemetria che devono essere mascherati
public std:: shared_ptr \<AuditDelegate\> auditPipelineDelegateOverride  |  Override del delegato di controllo per la scrittura di eventi di controllo
Cloud cloud pubblico  |  Tipo di cloud per controllare i dati di telemetria e gli eventi di controllo per lo scenario del cloud
  
  
#### <a name="hostnameoverride-struct-member"></a>membro struct hostNameOverride
Nome dell'istanza di controllo/telemetria host. Se non è impostato, MIP fungerà da host.
  
#### <a name="librarynameoverride-struct-member"></a>membro struct libraryNameOverride
Nome file della libreria di controllo/telemetria (DLL) alternativo.
  
#### <a name="httpdelegate"></a>HttpDelegate
Se impostato, la gestione HTTP verrà gestita da questa istanza
  
#### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di controllo/telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
  
#### <a name="isnetworkdetectionenabled-struct-member"></a>membro struct isNetworkDetectionEnabled
Se impostato, il componente di controllo/telemetria effettuerà il ping dello stato della rete sul thread in background
  
#### <a name="islocalcachingenabled-struct-member"></a>membro struct isLocalCachingEnabled
Se impostato, il componente di controllo/telemetria utilizzerà la memorizzazione nella cache su disco
  
#### <a name="istraceloggingenabled-struct-member"></a>membro struct isTraceLoggingEnabled
Se impostato, il componente di controllo/telemetria scriverà i log di avviso/errore sul disco
  
#### <a name="isminimaltelemetryenabled-struct-member"></a>membro struct isMinimalTelemetryEnabled
Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
  
#### <a name="isfastshutdownenabled-struct-member"></a>membro struct isFastShutdownEnabled
Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
  
#### <a name="customsettings-struct-member"></a>membro struct customSettings
Impostazioni di controllo/telemetria personalizzate >
  
#### <a name="maskedproperties-struct-member"></a>membro struct maskedProperties
Eventi/proprietà di controllo/telemetria che devono essere mascherati
  
#### <a name="auditdelegate"></a>AuditDelegate
Override del delegato di controllo per la scrittura di eventi di controllo
  
#### <a name="cloud"></a>Cloud
Tipo di cloud per controllare i dati di telemetria e gli eventi di controllo per lo scenario del cloud

### <a name="struct-miptelemetryconfiguration"></a>struct MIP:: TelemetryConfiguration 
Impostazioni di telemetria personalizzate (non usate comunemente)
  
Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String hostNameOverride  |  Nome dell'istanza di telemetria host. Se non è impostato, MIP fungerà da host.
public std:: String libraryNameOverride  |  Nome file della libreria di telemetria alternativa (DLL).
public std:: shared_ptr \<HttpDelegate\> httpDelegateOverride  |  Se impostato, la gestione HTTP verrà gestita da questa istanza
public std:: shared_ptr \<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
public bool isNetworkDetectionEnabled  |  Se impostato, il componente di telemetria effettuerà il ping dello stato della rete sul thread in background
public bool isLocalCachingEnabled  |  Se impostato, il componente di telemetria utilizzerà la memorizzazione nella cache su disco
public bool isTraceLoggingEnabled  |  Se impostato, il componente di telemetria scriverà i log di avviso/errore sul disco
public bool isTelemetryOptedOut  |  Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
public bool isFastShutdownEnabled  |  Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
public std:: Map \<std::string, std::string\> customSettings  |  Impostazioni di telemetria personalizzate >
  

#### <a name="hostnameoverride-struct-member"></a>membro struct hostNameOverride
Nome dell'istanza di telemetria host. Se non è impostato, MIP fungerà da host.
  
#### <a name="librarynameoverride-struct-member"></a>membro struct libraryNameOverride
Nome file della libreria di telemetria alternativa (DLL).
  
#### <a name="httpdelegate"></a>HttpDelegate
Se impostato, la gestione HTTP verrà gestita da questa istanza
  
#### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
  
#### <a name="isnetworkdetectionenabled-struct-member"></a>membro struct isNetworkDetectionEnabled
Se impostato, il componente di telemetria effettuerà il ping dello stato della rete sul thread in background
  
#### <a name="islocalcachingenabled-struct-member"></a>membro struct isLocalCachingEnabled
Se impostato, il componente di telemetria utilizzerà la memorizzazione nella cache su disco
  
#### <a name="istraceloggingenabled-struct-member"></a>membro struct isTraceLoggingEnabled
Se impostato, il componente di telemetria scriverà i log di avviso/errore sul disco
  
#### <a name="istelemetryoptedout-struct-member"></a>membro struct isTelemetryOptedOut
Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
  
#### <a name="isfastshutdownenabled-struct-member"></a>membro struct isFastShutdownEnabled
Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
  
#### <a name="customsettings-struct-member"></a>membro struct customSettings
Impostazioni di telemetria personalizzate.

### <a name="struct-uniqueidsandcontentformats"></a>struct UniqueIdsAndContentFormats 
  
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
gli UniqueId public std:: unordered_map \<std::string, std::string\>  | _Non ancora documentato._
public std:: Vector \<std::string\> contentFormats  | _Non ancora documentato._
  

  
#### <a name="uniqueids-struct-member"></a>membro struct uniqueIds

_Non ancora documentato._

  
#### <a name="contentformats-struct-member"></a>membro struct contentFormats

_Non ancora documentato._
