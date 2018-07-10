# <a name="class-mipfilehandler"></a>Classe mip::FileHandler 
Interfaccia per tutte le funzioni di gestione file.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  Avvia il recupero dell'etichetta di riservatezza dal file.
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  Avvia il recupero dei criteri di protezione dal file.
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Imposta l'etichetta di riservatezza per il file.
 public void DeleteLabel(AssignmentMethod method, const std::string& justificationMessage)  |  Elimina l'etichetta di riservatezza dal file.
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
 public void RemoveProtection()  |  Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\ |  .
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\ |  .
 public std::string GetOutputFileName()  |  Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
 public virtual ~FileHandler()  | _Non ancora documentato._
 protected FileHandler()  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="getlabelasync"></a>GetLabelAsync
Avvia il recupero dell'etichetta di riservatezza dal file.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).

Parametri:  
* **context**: contesto client che verrà passato in maniera opaca all'observer.


  
### <a name="getprotectionasync"></a>GetProtectionAsync
Avvia il recupero dei criteri di protezione dal file.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).

Parametri:  
* **context**: contesto client che verrà passato in maniera opaca all'observer.


  
### <a name="setlabel"></a>SetLabel
Imposta l'etichetta di riservatezza per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede una giustificazione e tramite il parametro labelingOptions non è stato fornito alcun messaggio di giustificazione.
  
### <a name="deletelabel"></a>DeleteLabel
Elimina l'etichetta di riservatezza dal file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede una giustificazione e tramite il parametro justificationMessage non è stato fornito alcun messaggio di giustificazione.
  
### <a name="setprotection"></a>SetProtection
Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="removeprotection"></a>RemoveProtection
Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="commitasync"></a>CommitAsync
Scrive le modifiche nel file specificato dal parametro |outputFilePath|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="commitasync"></a>CommitAsync
Scrive le modifiche nel flusso specificato dal parametro |outputStream|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="getoutputfilename"></a>GetOutputFileName
Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
  
### <a name="filehandler"></a>~FileHandler
_Non ancora documentato._

  
### <a name="filehandler"></a>FileHandler
_Non ancora documentato._
