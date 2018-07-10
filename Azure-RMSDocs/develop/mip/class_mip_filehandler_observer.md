# <a name="class-mipfilehandlerobserver"></a>Classe mip::FileHandler::Observer 
Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero delle notifiche degli eventi correlati al gestore di file da parte dei client.
Se si verifica un evento *Error, l'oggetto errore contiene la classe [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _Non ancora documentato._
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  Viene chiamato quando il gestore è creato correttamente.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando la creazione del gestore non è riuscita a causa di un errore.
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'etichetta (dal file) è riuscito correttamente.
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'etichetta (dal file) non è riuscito a causa di un errore.
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei criteri di protezione (dal file) è riuscito correttamente.
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei criteri di protezione (dal file) non è riuscito a causa di un errore.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il commit delle modifiche al file non è riuscito a causa di un errore.
 protected Observer()  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="observer"></a>~Observer
_Non ancora documentato._

  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
Viene chiamato quando il gestore è creato correttamente.
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
Viene chiamato quando la creazione del gestore non è riuscita a causa di un errore.
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Viene chiamato quando il recupero dell'etichetta (dal file) è riuscito correttamente.
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Viene chiamato quando il recupero dell'etichetta (dal file) non è riuscito a causa di un errore.
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Viene chiamato quando il recupero dei criteri di protezione (dal file) è riuscito correttamente.
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Viene chiamato quando il recupero dei criteri di protezione (dal file) non è riuscito a causa di un errore.
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
  
### <a name="oncommitfailure"></a>OnCommitFailure
Viene chiamato quando il commit delle modifiche al file non è riuscito a causa di un errore.
  
### <a name="observer"></a>Osservatore
_Non ancora documentato._
