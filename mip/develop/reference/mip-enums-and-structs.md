---
title: Microsoft Information Protection SDK per le enumerazioni e gli struct di riferimento di C++
description: Documentazione di riferimento per gli struct C++ MIP SDK e le enumerazioni.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 04abc581d94c0b05cf19d01362f7b416155a372c
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256108"
---
# <a name="summary"></a>Riepilogo

 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
**Namespace `mip` :** |
Enumerazione ActionSource       |  definisce che cosa ha attivato l'evento SetLabel
enum ActionType       |  Tipi di azioni diversi.
Enumerazione AssignmentMethod       |  Il metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come un'operazione con privilegi (l'equivalente a un'operazione di amministratore).
enum Consent       |  Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
Enumerazione visualizzazione       |  Formato del contenuto.
enum ContentMarkAlignment       |  Allineamento contenuto contrassegna (contenuto dell'intestazione o piè di pagina contenuto).
enum ContentState       |  Definisce lo stato dei dati l'applicazione agisce.
enum ErrorType       | _Non ancora documentato._
enum HttpRequestType       |  Tipo di richiesta HTTP.
enum LogLevel       |  Diversi livelli di log usati in MIP SDK.
enum ProtectionHandlerCreationOptions       |  Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.
enum ProtectionType       |  Indica se la protezione si basa un modello o è ad hoc (personalizzata)
Enumerazione WatermarkLayout       |  Layout delle filigrane.
struct ApplicationInfo  |  Struct che include informazioni specifiche dell'applicazione.
struct PublishingLicenseContext | Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
  
## <a name="enumerations-mip"></a>Enumerazioni (`mip`)

### <a name="actionsource-enum"></a>ActionSource enum

definisce che cosa ha attivato l'evento SetLabel

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
MANUAL            | Selezionato manualmente dall'utente
AUTOMATICO            | Impostazione delle condizioni dei criteri
CONSIGLIATO            | Impostato dall'utente dopo l'etichetta è stato consigliato per le condizioni dei criteri
IMPOSTAZIONE PREDEFINITA            | L'impostazione predefinita nei criteri
OBBLIGATORIO            | Impostato dall'utente dopo il criterio applicato per impostare un'etichetta


### <a name="actiontype-enum"></a>ActionType enum

Tipi di azioni diversi. CUSTOM è il tipo di azione generico. Ogni altro tipo di azione è un'azione specifica con un significato specifico.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | Aggiunge un piè di pagina contenuto al tipo di azione del documento.
ADD_CONTENT_HEADER            | Aggiunge un'intestazione contenuto al tipo di azione del documento.
ADD_WATERMARK            | Aggiunge una filigrana al tipo di azione dell'intero documento.
PERSONALIZZATI            | Tipo di azione definito personalizzato.
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

### <a name="assignmentmethod-enum"></a>AssignmentMethod enum

Il metodo di assegnazione dell'etichetta nel documento. Indica se l'assegnazione dell'etichetta è stata eseguita automaticamente, standard o come un'operazione con privilegi (l'equivalente a un'operazione di amministratore).

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
STANDARD            | [Etichetta](class_mip_label.md) metodo di assegnazione è standard
CON PRIVILEGI            | [Etichetta](class_mip_label.md) dispone dei privilegi necessari metodo di assegnazione
AUTO            | [Etichetta](class_mip_label.md) metodo di assegnazione è automatico


### <a name="consent-enum"></a>Enumerazione di consenso

Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
AcceptAlways            | Fornisce il consenso e memorizza questa decisione
Accettare            | Fornisce il consenso una sola volta
Rifiutare            | Non fornisce il consenso


### <a name="contentformat-enum"></a>Enumerazione di visualizzazione

Formato del contenuto.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
IMPOSTAZIONE PREDEFINITA            | Formato del contenuto è il formato di file standard
POSTA ELETTRONICA            | È contenuto il formato di posta elettronica

### <a name="contentmarkalignment-enum"></a>Enumerazione ContentMarkAlignment

Allineamento contenuto contrassegna (contenuto dell'intestazione o piè di pagina contenuto).

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
A SINISTRA            | Contrassegno contenuto è allineato a sinistra
OK            | Contrassegno contenuto è allineato a destra
CENTER            | Contrassegno contenuto viene centrato

### <a name="contentstate-enum"></a>ContentState enum

Definisce lo stato dei dati l'applicazione agisce.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
REST            | Dati inattivi archiviati fisicamente nel database o file/data warehouse
MOVIMENTO            | Dati che attraversa una rete o temporaneamente che risiedono nella memoria del computer da leggere o aggiornare
USE            | Dati attivi in costante evoluzione archiviate fisicamente nel database o file/data warehouse e così via

### <a name="errortype-enum"></a>Enumerazione ErrorType

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
  
### <a name="httprequesttype-enum"></a>HttpRequestType enum

Tipo di richiesta HTTP.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Ottenere            | GET
Post            | INSERISCI

  
### <a name="loglevel-enum"></a>LogLevel enum

Diversi livelli di log usati in MIP SDK.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
traccia            | 
Info            | 
Avviso            | 
Errore            | 

  
### <a name="protectionhandlercreationoptions-enum"></a>ProtectionHandlerCreationOptions enum

Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Nessuno            | Nessuno
OfflineOnly            | Non consente operazioni dell'interfaccia utente e di rete.
AllowAuditedExtraction            | Il contenuto può essere aperto in un'app che non supporta l'SDK di protezione
PreferDeprecatedAlgorithms            | Usa algoritmi di crittografia deprecati per la compatibilità con le versioni precedenti
  
### <a name="protectiontype-enum"></a>Enumerazione ProtectionType

Descrive se protezione si basa un modello o ad hoc (personalizzato).

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
TemplateBased            | L'handle è stato creato da un modello
Personalizzato            | L'handle è stato creato ad hoc
  
### <a name="watermarklayout-enum"></a>WatermarkLayout enum

Layout delle filigrane.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
ORIZZONTALE            | Layout della filigrana è orizzontale
DIAGONALI            | Layout della filigrana è diagonale


## <a name="structures"></a>Strutture 

### `mip::ApplicationInfo` 

Struct che include informazioni specifiche dell'applicazione.
  
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Identificatore dell'applicazione come impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
 public std::string applicationName  |  Nome dell'applicazione (deve contenere solo caratteri ASCII valida esclusa ';')
 public std::string applicationVersion  |  La versione dell'applicazione in uso, (deve contenere solo caratteri ASCII valida esclusa ';')
  
### `mip::PublishingLicenseContext` 

Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
  
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: Vector const\<uint8_t\> licenseInfo  | _Non ancora documentato._
Public std:: Vector const\<uint8_t\> serializedPublishingLicense  | _Non ancora documentato._
pubblica PublishingLicenseContext (const std:: Vector\<uint8_t\>& licenseInfo, const std:: Vector\<uint8_t\>& serializedPublishingLicense)  | _Non ancora documentato._
  
