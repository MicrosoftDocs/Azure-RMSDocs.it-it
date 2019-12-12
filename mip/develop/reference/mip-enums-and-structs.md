---
title: SDK MIP per C++ struct e enumerazioni di riferimento
description: Documentazione di riferimento per C++ gli struct e le enumerazioni dell'SDK MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: a6e5fae2296fb6f966f5f7fb6b73facb867398a2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560456"
---
# <a name="enumerations-and-structures"></a>Enumerazioni e strutture

## <a name="namespace-mip"></a>Spazio dei nomi MIP

Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
WatermarkLayout enum       |  Layout per le filigrane.
ContentMarkAlignment enum       |  Allineamento per i contrassegni di contenuto (intestazione del contenuto o piè di pagina del contenuto).
AssignmentMethod enum       |  Metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come operazione con privilegi (equivalente a un'operazione di amministratore).
ActionSource enum       |  definisce ciò che ha attivato l'evento di etichettatura
DataState enum       |  Definisce lo stato dei dati su cui si sta eseguendo l'applicazione.
ContentFormat enum       |  Formato del contenuto.
LabelFilterType enum       |  Tipi di filtro etichette, set facoltativo di proprietà che possono essere usate per filtrare le etichette quando si chiamano etichette di riservatezza degli elenchi.
enum Consent       |  Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
CacheStorageType enum       |  Tipo di archiviazione per le cache.
PFileExtensionBehavior enum       |  Descrive il comportamento delle estensioni PFile.
enum ErrorType       | Non ancora documentato.
InspectorType enum       |  Tipo di controllo correlato ai tipi di file supportati.
BodyType enum       |  Enumeratore del tipo di corpo.
FlightingFeature enum       |  Definisce nuove funzionalità in base al nome.
enum HttpRequestType       |  Tipo di richiesta HTTP.
enum LogLevel       |  Diversi livelli di log usati in MIP SDK.
enum ProtectionType       |  Indica se la protezione si basa un modello o è ad hoc (personalizzata)
enum ActionType       |  Tipi di azioni diversi.
LabelState enum       | Non ancora documentato.
ActionDataType enum       | Non ancora documentato.
ConditionDataType enum       | Non ancora documentato.
ContentMarkPlacement enum       | Non ancora documentato.
LabelActionDataType enum       | Non ancora documentato.
ProtectionActionType enum       | Non ancora documentato.
struct MIP:: ApplicationInfo  |  Struct che include informazioni specifiche dell'applicazione.
struct MIP:: TelemetryConfiguration  |  Impostazioni di telemetria personalizzate (non usate comunemente)

### <a name="enumerations"></a>Enumerazioni

#### <a name="watermarklayout-enum"></a>Enumerazione WatermarkLayout
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ORIZZONTALE            | Il layout della filigrana è orizzontale
DIAGONALE            | Il layout della filigrana è diagonale
Layout per le filigrane.
  
#### <a name="contentmarkalignment-enum"></a>Enumerazione ContentMarkAlignment
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
LEFT            | Il contrassegno del contenuto è allineato a sinistra
RIGHT            | Il contrassegno del contenuto è allineato a destra
CENTER            | Il contrassegno del contenuto è centrato
Allineamento per i contrassegni di contenuto (intestazione del contenuto o piè di pagina del contenuto).
  
#### <a name="assignmentmethod-enum"></a>Enumerazione AssignmentMethod
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
STANDARD            | Il metodo di assegnazione etichette è standard
CON privilegi            | Il metodo di assegnazione etichetta è con privilegi
AUTO            | Il metodo di assegnazione etichette è automatico
Metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come operazione con privilegi (equivalente a un'operazione di amministratore).
  
#### <a name="actionsource-enum"></a>Enumerazione ActionSource
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
MANUAL            | Selezionato manualmente dall'utente
AUTOMATIC            | Imposta da condizioni dei criteri
CONSIGLIABILE            | Impostato dall'utente dopo la raccomandazione dell'etichetta per le condizioni dei criteri
DEFAULT            | Impostazione predefinita nei criteri
definisce ciò che ha attivato l'evento di etichettatura
  
#### <a name="datastate-enum"></a>Enum di DataState
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
REST            | Dati inattivi archiviati fisicamente in database/file/warehouse
MOVIMENTO            | Dati che attraversano una rete o che risiedono temporaneamente nella memoria del computer per la lettura o l'aggiornamento
USE            | Dati attivi con modifiche costanti archiviati fisicamente in database/file/warehouse e così via
Definisce lo stato dei dati su cui si sta eseguendo l'applicazione.
  
#### <a name="contentformat-enum"></a>Enumerazione ContentFormat
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
DEFAULT            | Il formato del contenuto è il formato di file standard
E-MAIL            | Il formato del contenuto è formato posta elettronica
Formato del contenuto.
  
#### <a name="labelfiltertype-enum"></a>Enumerazione LabelFilterType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Nessuno            | Disabilita filtro etichette predefinito
Custom            | Filtrare le etichette che possono causare la protezione personalizzata
TemplateProtection            | Filtrare le etichette che possono causare la mancata esecuzione
DoNotForwardProtection            | Filtrare le etichette che possono causare la protezione del modello
AdhocProtection            | Filtrare le etichette che possono causare la protezione ad hoc
HyokProtection            | Filtrare le etichette che possono causare la protezione Hyok
PredefinedTemplate            | Filtrare le etichette che possono comportare la protezione modello predefinita
Tipi di filtro etichette, set facoltativo di proprietà che possono essere usate per filtrare le etichette quando si chiamano etichette di riservatezza degli elenchi.
  
#### <a name="consent-enum"></a>Enum di consenso
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
AcceptAlways            | Fornisce il consenso e memorizza questa decisione
Accetta            | Fornisce il consenso una sola volta
Rifiuta            | Non fornisce il consenso
Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
  
#### <a name="cachestoragetype-enum"></a>Enumerazione CacheStorageType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
InMemory            | Archiviazione in memoria
OnDisk            | Archiviazione su disco
OnDiskEncrypted            | Sull'archiviazione su disco con crittografia (se supportata dalla piattaforma)
Tipo di archiviazione per le cache.
  
#### <a name="pfileextensionbehavior-enum"></a>Enumerazione PFileExtensionBehavior
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Valore predefinito            | Le estensioni diventeranno il comportamento predefinito di SDK
PFileSuffix            | Le estensioni diventeranno <EXT>. PFILE
PPrefix            | Le estensioni diventeranno P<EXT>
Descrive il comportamento delle estensioni PFile.
  
#### <a name="errortype-enum"></a>Enumerazione ErrorType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | Il chiamante ha passato un input errato.
FILE_IO_ERROR            | Errore di I/O file generale.
NETWORK_ERROR            | Problemi di rete generali; ad esempio, un servizio irraggiungibile.
TRANSIENT_NETWORK_ERROR            | Problemi di rete temporanei; ad esempio, gateway non valido.
INTERNAL_ERROR            | Errori imprevisti interni,
JUSTIFICATION_REQUIRED            | Per completare l'azione sul file, è necessario specificare una giustificazione.
NOT_SUPPORTED_OPERATION            | L'operazione richiesta non è ancora supportata.
PRIVILEGED_REQUIRED            | Non è possibile eseguire l'override dell'etichetta con privilegi quando il nuovo metodo di etichetta è standard.
ACCESS_DENIED            | L'utente non è riuscito a ottenere l'accesso ai servizi.
CONSENT_DENIED            | Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
POLICY_SYNC_ERROR            | Tentativo di sincronizzare i dati dei criteri non riuscito.
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
  
#### <a name="inspectortype-enum"></a>Enumerazione InspectorType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Unknown            | Controllo file sconosciuto.
Msg            | Controllo file di tipo msg, basato su rpmsg/msg.
Tipo di controllo correlato ai tipi di file supportati.
  
#### <a name="bodytype-enum"></a>Enumerazione BodyType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
UNKNOWN            | Tipo di corpo sconosciuto
TXT            | Tipo di corpo dello stile del testo, la codifica viene restituita come UTF8
HTML            | Tipo di corpo dello stile HTML, la codifica viene restituita come UTF8
RTF            | Tipo di corpo dello stile RTF, formato binario
Enumeratore del tipo di corpo.
  
#### <a name="flightingfeature-enum"></a>Enumerazione FlightingFeature
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | Utilizzare una chiamata HTTP separata per determinare gli endpoint di servizio RMS
AuthInfoCache            | Memorizzare nella cache le richieste OAuth2 per dominio/tenant per ridurre le risposte 401 non necessarie. Disabilitare per app/servizi che gestiscono la propria autenticazione HTTP (ad esempio, SPO, Edge)
LinuxEncryptedCache            | Abilitare la memorizzazione nella cache crittografata per le piattaforme Linux (leggere i prerequisiti per questa funzionalità)
SingleDomainName            | Abilitare il nome della singola società per la ricerca DNS. ad esempio [https://corprights](https://corprights)
PolicyAuth            | Abilitare l'autenticazione HTTP automatica per le richieste inviate al servizio criteri. Disabilitare per app/servizi che gestiscono la propria autenticazione HTTP (ad esempio, SPO, Edge)
Definisce nuove funzionalità in base al nome.
  
#### <a name="httprequesttype-enum"></a>Enumerazione HttpRequestType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Ottenere            | GET
Post            | POST
Tipo di richiesta HTTP.
  
#### <a name="loglevel-enum"></a>Enumerazione LogLevel
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Avviso            | 
Errore di            | 
Diversi livelli di log usati in MIP SDK.
  
#### <a name="protectiontype-enum"></a>Enumerazione ProtectionType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
TemplateBased            | L'handle è stato creato da un modello
Custom            | L'handle è stato creato ad hoc
Indica se la protezione si basa un modello o è ad hoc (personalizzata)
  
#### <a name="actiontype-enum"></a>Enumerazione ActionType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | Aggiunge un piè di pagina contenuto al tipo di azione del documento.
ADD_CONTENT_HEADER            | Aggiunge un'intestazione contenuto al tipo di azione del documento.
ADD_WATERMARK            | Aggiunge una filigrana al tipo di azione dell'intero documento.
PERSONALIZZATO            | Tipo di azione definito personalizzato.
JUSTIFY            | Tipo di azione di allineamento.
METADATA            | Tipo di azione di modifica dei metadati.
PROTECT_ADHOC            | Tipo di azione di protezione con criteri ad hoc.
PROTECT_BY_TEMPLATE            | Tipo di azione di protezione con modello.
PROTECT_DO_NOT_FORWARD            | Tipo di azione di protezione senza inoltro.
REMOVE_CONTENT_FOOTER            | Tipo di azione di rimozione del piè di pagina contenuto.
REMOVE_CONTENT_HEADER            | Tipo di azione di rimozione dell'intestazione contenuto.
REMOVE_PROTECTION            | Tipo di azione di rimozione di agenti protezione.
REMOVE_WATERMARK            | Tipo di azione di rimozione della filigrana.
APPLY_LABEL            | Tipo di azione di applicazione dell'etichetta.
RECOMMEND_LABEL            | Tipo di azione di etichetta consigliata.
Tipi di azioni diversi.
CUSTOM è il tipo di azione generico. Ogni altro tipo di azione è un'azione specifica con un significato specifico.
  
#### <a name="labelstate-enum"></a>Enumerazione LabelState
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
NoChange            | 
Remove            | 
Aggiornamento/Aggiornare            | 
  
#### <a name="actiondatatype-enum"></a>Enumerazione ActionDataType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Custom            | 
Protection            | 
ContentMarking            | 
AddWatermark            | 
Label            | 
  
#### <a name="conditiondatatype-enum"></a>Enumerazione ConditionDataType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Valore predefinito            | 
Sensibilità            | 
  
#### <a name="contentmarkplacement-enum"></a>Enumerazione ContentMarkPlacement
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Header            | 
Piè di pagina            | 
  
#### <a name="labelactiondatatype-enum"></a>Enumerazione LabelActionDataType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Raccomandazione            | 
Applica            | 
  
#### <a name="protectionactiontype-enum"></a>Enumerazione ProtectionActionType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Custom            | 
Modello            | 
DoNotForward            | 
Adhoc            | 
DoNotForwardWithPrompt            | 
Hyok            | 
PredefinedTemplate            | 
RemoveProtection            | 

### <a name="structures"></a>Strutture

#### <a name="struct-mipapplicationinfo"></a>struct MIP:: ApplicationInfo 
Struct che include informazioni specifiche dell'applicazione.
  
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
public std::string applicationName  |  Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
public std::string applicationVersion  |  Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')
  

##### <a name="applicationid-struct-member"></a>membro struct applicationId
Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
  
##### <a name="applicationname-struct-member"></a>membro struct di ApplicationName
Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
  
##### <a name="applicationversion-struct-member"></a>membro struct applicationVersion
Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')

#### <a name="struct-miptelemetryconfiguration"></a>struct MIP:: TelemetryConfiguration 
Impostazioni di telemetria personalizzate (non usate comunemente)
  
Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String hostNameOverride  |  Nome dell'istanza di telemetria host. Se non è impostato, MIP fungerà da host.
public std:: String libraryNameOverride  |  Nome file della libreria di telemetria alternativa (DLL).
public std:: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  Se impostato, la gestione HTTP verrà gestita da questa istanza
public std:: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
public bool isNetworkDetectionEnabled  |  Se impostato, il componente di telemetria effettuerà il ping dello stato della rete sul thread in background
public bool isLocalCachingEnabled  |  Se impostato, il componente di telemetria utilizzerà la memorizzazione nella cache su disco
public bool isTraceLoggingEnabled  |  Se impostato, il componente di telemetria scriverà i log di avviso/errore sul disco
public bool isTelemetryOptedOut  |  Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
public bool isFastShutdownEnabled  |  Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
public std:: Map\<std:: String, std:: String\> customSettings  |  Impostazioni di telemetria personalizzate >
    
##### <a name="hostnameoverride-struct-member"></a>membro struct hostNameOverride
Nome dell'istanza di telemetria host. Se non è impostato, MIP fungerà da host.
  
##### <a name="librarynameoverride-struct-member"></a>membro struct libraryNameOverride
Nome file della libreria di telemetria alternativa (DLL).
  
##### <a name="httpdelegate"></a>HttpDelegate
Se impostato, la gestione HTTP verrà gestita da questa istanza
  
##### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
  
##### <a name="isnetworkdetectionenabled-struct-member"></a>membro struct isNetworkDetectionEnabled
Se impostato, il componente di telemetria effettuerà il ping dello stato della rete sul thread in background
  
##### <a name="islocalcachingenabled-struct-member"></a>membro struct isLocalCachingEnabled
Se impostato, il componente di telemetria utilizzerà la memorizzazione nella cache su disco
  
##### <a name="istraceloggingenabled-struct-member"></a>membro struct isTraceLoggingEnabled
Se impostato, il componente di telemetria scriverà i log di avviso/errore sul disco
  
##### <a name="istelemetryoptedout-struct-member"></a>membro struct isTelemetryOptedOut
Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
  
##### <a name="isfastshutdownenabled-struct-member"></a>membro struct isFastShutdownEnabled
Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
  
##### <a name="customsettings-struct-member"></a>membro struct customSettings
Impostazioni di telemetria personalizzate >

## <a name="namespace-mipauditmetadatakeys"></a>spazio dei nomi MIP:: auditmetadatakeys
  
### <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String sender ()       |  Controllare le chiavi dei metadati nella rappresentazione di stringa.
Destinatari std:: String pubblici ()       | Non ancora documentato.
public std:: String LastModifiedBy ()       | Non ancora documentato.
public std:: String LastModifiedDate ()       | Non ancora documentato.
  
### <a name="members"></a>Membri
  
#### <a name="sender-function"></a>Funzione sender
Controllare le chiavi dei metadati nella rappresentazione di stringa.
  
#### <a name="recipients-function"></a>Funzione Recipients
_Non ancora documentato._

  
#### <a name="lastmodifiedby-function"></a>LastModifiedBy (funzione)
_Non ancora documentato._

  
#### <a name="lastmodifieddate-function"></a>LastModifiedDate (funzione)
_Non ancora documentato._

## <a name="namespace-miprights"></a>spazio dei nomi MIP:: Rights
  
### <a name="summary"></a>Riepilogo
 
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string Owner()       |  Ottiene l'identificatore della stringa per il diritto "owner".
public std::string View()       |  Ottiene l'identificatore della stringa per il diritto "view".
public std::string AuditedExtract()       |  Ottiene l'identificatore della stringa per il diritto "audited extract".
public std::string Edit()       |  Ottiene l'identificatore della stringa per il diritto "edit".
public std::string Export()       |  Ottiene l'identificatore della stringa per il diritto "export".
public std::string Extract()       |  Ottiene l'identificatore della stringa per il diritto "extract".
public std::string Print()       |  Ottiene l'identificatore della stringa per il diritto "print".
public std::string Comment()       |  Ottiene l'identificatore della stringa per il diritto "comment".
public std::string Reply()       |  Ottiene l'identificatore della stringa per il diritto "reply".
public std::string ReplyAll()       |  Ottiene l'identificatore della stringa per il diritto "reply all".
public std::string Forward()       |  Ottiene l'identificatore della stringa per il diritto "forward".
public std:: Vector\<std:: String\> EmailRights ()       |  Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.
public std:: Vector\<std:: String\> EditableDocumentRights ()       |  Ottiene un elenco di diritti che si applicano ai documenti.
public std:: Vector\<std:: String\> CommonRights ()       |  Ottiene un elenco di diritti che si applicano in tutti gli scenari.
  
### <a name="members"></a>Membri
  
#### <a name="owner-function"></a>Funzione Owner
Ottiene l'identificatore della stringa per il diritto "owner".

  
**Restituisce**: identificatore della stringa per il diritto "owner"
  
#### <a name="view-function"></a>Funzione View
Ottiene l'identificatore della stringa per il diritto "view".

  
**Restituisce**: identificatore della stringa per il diritto "view"
  
#### <a name="auditedextract-function"></a>AuditedExtract (funzione)
Ottiene l'identificatore della stringa per il diritto "audited extract".

  
**Restituisce**: identificatore della stringa per il diritto "audited extract"
  
#### <a name="edit-function"></a>Modifica funzione
Ottiene l'identificatore della stringa per il diritto "edit".

  
**Restituisce**: identificatore della stringa per il diritto "edit"
  
#### <a name="export-function"></a>Funzione Export
Ottiene l'identificatore della stringa per il diritto "export".

  
**Restituisce**: identificatore della stringa per il diritto "export"
  
#### <a name="extract-function"></a>Extract - funzione
Ottiene l'identificatore della stringa per il diritto "extract".

  
**Restituisce**: identificatore della stringa per il diritto "extract"
  
#### <a name="print-function"></a>Funzione Print
Ottiene l'identificatore della stringa per il diritto "print".

  
**Restituisce**: identificatore della stringa per il diritto "print"
  
#### <a name="comment-function"></a>Funzione Comment
Ottiene l'identificatore della stringa per il diritto "comment".

  
**Restituisce**: identificatore della stringa per il diritto "comment"
  
#### <a name="reply-function"></a>Funzione Reply
Ottiene l'identificatore della stringa per il diritto "reply".

  
**Restituisce**: identificatore della stringa per il diritto "reply"
  
#### <a name="replyall-function"></a>ReplyAll (funzione)
Ottiene l'identificatore della stringa per il diritto "reply all".

  
**Restituisce**: identificatore della stringa per il diritto "reply all"
  
#### <a name="forward-function"></a>Funzione di avanzamento
Ottiene l'identificatore della stringa per il diritto "forward".

  
**Restituisce**: identificatore della stringa per il diritto "forward"
  
#### <a name="emailrights-function"></a>EmailRights (funzione)
Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.

  
**Restituisce**: elenco di diritti che si applicano ai messaggi di posta elettronica
  
#### <a name="editabledocumentrights-function"></a>EditableDocumentRights (funzione)
Ottiene un elenco di diritti che si applicano ai documenti.

  
**Restituisce**: elenco di diritti che si applicano ai documenti
  
#### <a name="commonrights-function"></a>CommonRights (funzione)
Ottiene un elenco di diritti che si applicano in tutti gli scenari.

  
**Restituisce**: elenco di diritti che si applicano in tutti gli scenari

## <a name="namespace-miproles"></a>spazio dei nomi MIP:: Roles
  
### <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Ottiene l'identificatore della stringa per il ruolo "viewer".
public std::string Reviewer()       |  Ottiene l'identificatore della stringa per il ruolo "reviewer".
public std::string Author()       |  Ottiene l'identificatore della stringa per il ruolo "author".
public std::string CoOwner()       |  Ottiene l'identificatore della stringa per il ruolo "co-owner".
  
### <a name="members"></a>Membri
  
#### <a name="viewer-function"></a>Funzione Viewer
Ottiene l'identificatore della stringa per il ruolo "viewer".

  
**Restituisce**: identificatore della stringa per il ruolo "viewer". Un visualizzatore può solo visualizzare il contenuto. Non può modificarlo, copiarlo o stamparlo.
  
#### <a name="reviewer-function"></a>Revisore (funzione)
Ottiene l'identificatore della stringa per il ruolo "reviewer".

  
**Restituisce**: identificatore della stringa per il ruolo "reviewer". Un revisore può visualizzare e modificare il contenuto. Non può copiarlo o stamparlo.
  
#### <a name="author-function"></a>Author (funzione)
Ottiene l'identificatore della stringa per il ruolo "author".

  
**Restituisce**: identificatore della stringa per il ruolo "author". Un autore può visualizzare, modificare, copiare e stampare il contenuto.
  
#### <a name="coowner-function"></a>Funzione CoOwner
Ottiene l'identificatore della stringa per il ruolo "co-owner".

  
**Restituisce**: identificatore della stringa per il ruolo "co-owner". Un comproprietario ha tutte le autorizzazioni

