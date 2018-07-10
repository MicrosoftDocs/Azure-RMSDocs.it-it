# <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 enum Consent       |  Rappresenta la decisione di un utente di fornire il consenso per connettersi a un endpoint di servizio.
 struct ApplicationInfo  |  ID dell'applicazione impostato nel portale di Azure AD.
**mip** |
 enum ActionType       |  Tipi di azioni diversi.
 enum ErrorType       | _Non ancora documentato._
 enum LogLevel       |  Diversi livelli di log usati tra in MIP SDK.
 enum ProtectionHandlerCreationOptions       |  Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.
 enum ProtectionType       |  Indica se la protezione si basa un modello o è ad hoc (personalizzata)

  
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
  
I valori di **ActionType** supportano gli operatori seguenti:

* Operatore Or (|) per il tipo enum [Action](class_mip_action.md).  
* Operatore And (&) per il tipo enum [Action](class_mip_action.md).  
* Operatore Xor (^) per il tipo enum [Action](class_mip_action.md).  

### <a name="errortype"></a>ErrorType

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | Il chiamante ha passato un input errato.
FILE_IO_ERROR            | Errore di I/O file generale.
NETWORK_ERROR            | Problemi generali di rete, ad esempio servizio non raggiungibile.
INTERNAL_ERROR            | Errori imprevisti interni, ad esempio nel protocollo client-server (è stata ricevuta una risposta imprevista).
JUSTIFICATION_REQUIRED            | Per completare l'azione sul file, è necessario specificare una giustificazione.
NOT_SUPPORTED_OPERATION            | L'operazione richiesta non è ancora supportata.
PRIVILEGED_REQUIRED            | Non è possibile eseguire l'override dell'etichetta con privilegi quando il nuovo metodo di etichetta è standard.
ACCESS_DENIED            | L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni, contenuto revocato e così via.
  
### <a name="loglevel"></a>LogLevel

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Avviso            | 
Errore            | 
Diversi livelli di log usati tra in MIP SDK.
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Nessuno            | Nessuno
OfflineOnly            | Non consente operazioni dell'interfaccia utente e di rete.
AllowAuditedExtraction            | Il contenuto può essere aperto in un'app che non supporta l'SDK di protezione
PreferDeprecatedAlgorithms            | Usa algoritmi di crittografia deprecati per la compatibilità con le versioni precedenti
Flag di bit che determinano il comportamento di creazione di criteri aggiuntivi.
  
### <a name="protectiontype"></a>ProtectionType

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
TemplateBased            | L'handle è stato creato da un modello
Personalizzato            | L'handle è stato creato ad hoc
Indica se la protezione si basa un modello o è ad hoc (personalizzata)
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Operatore OR bit per bit ProtectionHandlerCreationOptions.

Parametri: 
 
* **a**: valore sinistro 

* **b**: valore destro
  
**Restituisce**: OR bit per bit di parametri
  


## <a name="structures"></a>Strutture

### <a name="applicationinfo"></a>ApplicationInfo 
Identificatore dell'applicazione impostato nel portale di Azure AD.
  
 Campi                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public std::string applicationId  | ID dell'applicazione nel portale di Azure AD.
 public std::string friendlyName  | Nome descrittivo dell'app, specificato nel portale.
  
