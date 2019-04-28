---
title: Microsoft Information Protection SDK per le enumerazioni e gli struct di riferimento di C++
description: Documentazione di riferimento per gli struct C++ MIP SDK e le enumerazioni.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c9e634d436d02b147fc10a734c8c3d5b1fcdec71
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173357"
---
# <a name="enumerations-and-structures"></a>Enumerazioni e strutture

## <a name="namespace-mip"></a>Namespace mip

 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Enumerazione ActionSource       |  definisce che cosa ha attivato l'evento SetLabel
enum ActionType       |  Tipi di azioni diversi.
Enumerazione AssignmentMethod       |  Il metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come un'operazione con privilegi (l'equivalente a un'operazione di amministratore).
enum Consent       |  Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
Enumerazione visualizzazione       |  Formato del contenuto.
enum ContentMarkAlignment       |  Allineamento contenuto contrassegna (contenuto dell'intestazione o piè di pagina contenuto).
Enumerazione DataState       |  Definisce lo stato dei dati l'applicazione agisce.
enum ErrorType       | _Non ancora documentato._
enum HttpRequestType       |  Tipo di richiesta HTTP.
enum LogLevel       |  Diversi livelli di log usati in MIP SDK.
enum ProtectionHandlerCreationOptions       |  Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.
enum ProtectionType       |  Indica se la protezione si basa un modello o è ad hoc (personalizzata)
Enumerazione WatermarkLayout       |  Layout delle filigrane.
struct ApplicationInfo  |  Struct che include informazioni specifiche dell'applicazione.
struct PublishingLicenseContext  |  Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
  
## <a name="enumerations-mip"></a>Enumerazioni (mip)

### <a name="actionsource"></a>ActionSource

Definisce che cosa ha attivato l'evento SetLabel.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
MANUAL            | Selezionato manualmente dall'utente
AUTOMATICO            | Impostazione delle condizioni dei criteri
CONSIGLIATO            | Impostato dall'utente dopo l'etichetta è stato consigliato per le condizioni dei criteri
DEFAULT            | L'impostazione predefinita nei criteri
OBBLIGATORIO            | Impostato dall'utente dopo il criterio applicato per impostare un'etichetta



### <a name="actiontype"></a>ActionType

Tipi di azioni diversi. CUSTOM è il tipo di azione generico. Ogni altro tipo di azione è un'azione specifica con un significato specifico.

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


### <a name="assignmentmethod"></a>AssignmentMethod

Il metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come un'operazione con privilegi (l'equivalente a un'operazione di amministratore).

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
STANDARD            | [Etichetta](class_mip_label.md) metodo di assegnazione è standard
CON PRIVILEGI            | [Etichetta](class_mip_label.md) dispone dei privilegi necessari metodo di assegnazione
AUTO            | [Etichetta](class_mip_label.md) metodo di assegnazione è automatico


### <a name="consent"></a>Fornire il consenso

Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
AcceptAlways            | Fornisce il consenso e memorizza questa decisione
Accetta            | Fornisce il consenso una sola volta
Rifiuta            | Non fornisce il consenso


### <a name="contentformat"></a>ContentFormat

Formato del contenuto.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
DEFAULT            | Formato del contenuto è il formato di file standard
POSTA ELETTRONICA            | È contenuto il formato di posta elettronica

### <a name="contentmarkalignment"></a>ContentMarkAlignment

Allineamento contenuto contrassegna (contenuto dell'intestazione o piè di pagina contenuto).

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
LEFT            | Contrassegno contenuto è allineato a sinistra
RIGHT            | Contrassegno contenuto è allineato a destra
CENTER            | Contrassegno contenuto viene centrato

### <a name="datastate"></a>DataState
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
REST            | Dati inattivi archiviati fisicamente nel database o file/data warehouse
MOVIMENTO            | Dati che attraversa una rete o temporaneamente che risiedono nella memoria del computer da leggere o aggiornare
USE            | Dati attivi in costante evoluzione archiviate fisicamente nel database o file/data warehouse e così via


### <a name="errortype"></a>ErrorType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | Il chiamante ha passato un input errato.
FILE_IO_ERROR            | Errore di I/O file generale.
NETWORK_ERROR            | Problemi generali di rete; ad esempio, il servizio non raggiungibile.
TRANSIENT_NETWORK_ERROR            | Problemi di rete temporanei; ad esempio, i gateway non valido.
INTERNAL_ERROR            | Errori imprevisti interni,
JUSTIFICATION_REQUIRED            | Per completare l'azione sul file, è necessario specificare una giustificazione.
NOT_SUPPORTED_OPERATION            | L'operazione richiesta non è ancora supportata.
PRIVILEGED_REQUIRED            | Non è possibile eseguire l'override dell'etichetta con privilegi quando il nuovo metodo di etichetta è standard.
ACCESS_DENIED            | L'utente non è stato possibile ottenere l'accesso ai servizi.
CONSENT_DENIED            | Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
POLICY_SYNC_ERROR            | Tentativo di sincronizzare i dati dei criteri non riuscito.
NO_PERMISSIONS            | L'utente non è riuscito a ottenere l'accesso al contenuto, Ad esempio, alcuna autorizzazione, contenuti non revocato
NO_AUTH_TOKEN            | L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un token di autenticazione vuoto.
DISABLED_SERVICE            | L'utente non è stato possibile ottenere l'accesso al contenuto a causa la disattivazione del servizio
PROXY_AUTH_ERROR            | Autenticazione proxy non riuscita.
NO_POLICY_ERROR            | Nessun criterio è configurato per tenant/utente
OPERATION_CANCELLED            | Operazione annullata
ADHOC_PROTECTION_REQUIRED            | Protezione ad hoc deve essere impostata per completare l'azione sul file
  
### <a name="httprequesttype"></a>HttpRequestType

Tipo di richiesta HTTP.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Ottenere            | GET
Post            | INSERISCI

  
### <a name="loglevel"></a>LogLevel

Diversi livelli di log usati in MIP SDK.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Avviso            | 
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Nessuno            | Nessuno
OfflineOnly            | Non consente operazioni dell'interfaccia utente e di rete.
AllowAuditedExtraction            | Il contenuto può essere aperto in un'app che non supporta l'SDK di protezione
PreferDeprecatedAlgorithms            | Usa algoritmi di crittografia deprecati per la compatibilità con le versioni precedenti


### <a name="protectiontype"></a>ProtectionType

Descrive se protezione si basa un modello o ad hoc (personalizzato).

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
TemplateBased            | L'handle è stato creato da un modello
Personalizzato            | L'handle è stato creato ad hoc

  
### <a name="watermarklayout"></a>WatermarkLayout

Layout delle filigrane.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ORIZZONTALE            | Layout della filigrana è orizzontale
DIAGONALI            | Layout della filigrana è diagonale


## <a name="structures"></a>Strutture 

### <a name="mipapplicationinfo"></a>mip::ApplicationInfo 
Struct che include informazioni specifiche dell'applicazione.
  
#### <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificatore dell'applicazione come impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
public std::string applicationName  |  Nome dell'applicazione (deve contenere solo caratteri ASCII valida esclusa ';')
public std::string applicationVersion  |  La versione dell'applicazione in uso, (deve contenere solo caratteri ASCII valida esclusa ';')
  
#### <a name="members"></a>Membri
  
##### <a name="applicationid-struct-member"></a>membro struct applicationId
Identificatore dell'applicazione come impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
  
##### <a name="applicationname-struct-member"></a>membro struct applicationName
Nome dell'applicazione (deve contenere solo caratteri ASCII valida esclusa ';')
  
##### <a name="applicationversion-struct-member"></a>membro struct applicationVersion
La versione dell'applicazione in uso, (deve contenere solo caratteri ASCII valida esclusa ';')  

### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
  
#### <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: Vector const\<uint8_t\> licenseInfo  | _Non ancora documentato._
Public std:: Vector const\<uint8_t\> serializedPublishingLicense  | _Non ancora documentato._
pubblica PublishingLicenseContext (const std:: Vector\<uint8_t\>& licenseInfo, const std:: Vector\<uint8_t\>& serializedPublishingLicense)  | _Non ancora documentato._
  
#### <a name="members"></a>Membri
  
##### <a name="licenseinfo-struct-member"></a>membro struct licenseInfo
_Non ancora documentato._

  
##### <a name="serializedpublishinglicense-struct-member"></a>membro struct serializedPublishingLicense
_Non ancora documentato._

  
##### <a name="publishinglicensecontext-function"></a>PublishingLicenseContext (funzione)
_Non ancora documentato._
