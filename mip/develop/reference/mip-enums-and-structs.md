---
title: Riepilogo
description: Riepilogo
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5af209d5a627263399c8c60f474495dcadab24a0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446499"
---
# <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
**comuni** |
enum Consent       |  Risposta dell'utente quando viene richiesto il consenso per connettersi a un endpoint di servizio.
struct ApplicationInfo  |  Struct che include informazioni specifiche dell'applicazione.
**mip** |
enum ErrorType       | _Non ancora documentato._
enum HttpRequestType       |  Tipo di richiesta HTTP.
enum LogLevel       |  Diversi livelli di log usati in MIP SDK.
enum ProtectionHandlerCreationOptions       |  Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.
enum ProtectionType       |  Indica se la protezione si basa un modello o è ad hoc (personalizzata)
enum ActionType       |  Tipi di azioni diversi.
struct mip::PublishingLicenseContext | Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.

  
## <a name="enumerations-common"></a>Enumerazioni (comuni)
  
### <a name="consent"></a>Consent
Rappresenta la decisione di un utente di fornire il consenso per connettersi a un endpoint di servizio.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
AcceptAlways            | Fornisce il consenso e memorizza questa decisione
Accetta            | Fornisce il consenso una sola volta
Rifiuta            | Non fornisce il consenso
  
## <a name="enumerations-mip"></a>Enumerazioni (mip)

### <a name="actiontype"></a>ActionType

Tipi di azioni diversi.

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

CUSTOM è il tipo di azione generico. Ogni altro tipo di azione è un'azione specifica con un significato specifico.

I valori ActionType possono essere combinati usando gli operatori seguenti:

- Operatore And (&) per [Action](class_mip_action.md) (`operator &(ActionType a, ActionType b)`)
- Operatore Or logico (Xor) (^) per [Action](class_mip_action.md). (`operator ^(ActionType a, ActionType b)`)


### <a name="errortype"></a>ErrorType
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | Il chiamante ha passato un input errato.
FILE_IO_ERROR            | Errore di I/O file generale.
NETWORK_ERROR            | Problemi generali di rete, ad esempio servizio non raggiungibile.
TRANSIENT_NETWORK_ERROR            | Problemi di rete temporanei, ad esempio gateway non valido.
INTERNAL_ERROR            | Errori imprevisti interni, ad esempio nel protocollo client-server (è stata ricevuta una risposta imprevista).
JUSTIFICATION_REQUIRED            | Per completare l'azione sul file, è necessario specificare una giustificazione.
NOT_SUPPORTED_OPERATION            | L'operazione richiesta non è ancora supportata.
PRIVILEGED_REQUIRED            | Non è possibile eseguire l'override dell'etichetta con privilegi quando il nuovo metodo di etichetta è standard.
ACCESS_DENIED            | L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni, contenuto revocato e così via.
CONSENT_DENIED            | Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
  
### <a name="httprequesttype"></a>HttpRequestType
Tipo di richiesta HTTP.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Ottenere            | GET
Post            | POST
  
### <a name="loglevel"></a>LogLevel

Diversi livelli di log usati in MIP SDK.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Avviso            | 
Errore            | 
Diversi livelli di log usati tra in MIP SDK.
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Nessuno            | Nessuno
OfflineOnly            | Non consente operazioni dell'interfaccia utente e di rete.
AllowAuditedExtraction            | Il contenuto può essere aperto in un'app che non supporta l'SDK di protezione
PreferDeprecatedAlgorithms            | Usa algoritmi di crittografia deprecati per la compatibilità con le versioni precedenti


### <a name="protectiontype"></a>ProtectionType
Indica se la protezione si basa un modello o è ad hoc (personalizzata)

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
TemplateBased            | L'handle è stato creato da un modello
Personalizzato            | L'handle è stato creato ad hoc

  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions
Operatore OR bit per bit ProtectionHandlerCreationOptions.

Parametri:  
* **a**: valore sinistro 

* **b**: valore destro

### <a name="releaseallresources"></a>ReleaseAllResources
Rilascia tutte le risorse (thread e così via) prima dell'arresto.
Se le librerie dinamiche MIP sono a caricamento ritardato da un'applicazione, questa funzione deve essere chiamata prima che l'applicazione scarichi in modo esplicito tali librerie MIP per evitare deadlock. Ad esempio, in win32 questa funzione deve essere chiamata prima di qualsiasi chiamata per scaricare in modo esplicito DLL MIP tramite FreeLibrary o \__FUnloadDelayLoadedDLL2. Le applicazioni devono rilasciare i riferimenti a tutti gli oggetti MIP (ad esempio, profili, motori, gestori) prima di chiamare questa funzione.
  
**Restituisce**: OR bit per bit di parametri
  
## <a name="structures"></a>Strutture

### <a name="applicationinfo"></a>ApplicationInfo 
Struct che include informazioni specifiche dell'applicazione.

 Campi                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Identificatore dell'applicazione impostato nel portale di Azure AD.
 public std::string applicationName  |  Nome applicazione
 public std::string applicationVersion  |  Versione dell'applicazione in uso
  
### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
  
 Campi                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector<uint8_t> licenseInfo  | _Non ancora documentato._
public const std::vector<uint8_t> serializedPublishingLicense  | _Non ancora documentato._
public PublishingLicenseContext(const std::vector<uint8_t>& licenseInfo, const std::vector<uint8_t>& serializedPublishingLicense)  | _Non ancora documentato._
  
