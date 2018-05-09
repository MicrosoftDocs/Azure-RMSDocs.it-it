# <a name="class-mipfilehandlerobserver"></a>Classe mip::FileHandler::Observer 
Interfaccia [Observer](#classmip_1_1_file_handler_1_1_observer) per il recupero delle notifiche degli eventi correlati al gestore di file da parte dei client.
Se si verifica un evento *Error, l'oggetto errore contiene la classe [mip::Error](#classmip_1_1_error). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline virtual ~Observer()  |  
public void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'etichetta (dal file) è riuscito correttamente.
public void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'etichetta (dal file) non è riuscito a causa di un errore.
public void OnGetProtectionSuccess(const std::shared_ptr<UserPolicy>& userPolicy, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei criteri di protezione (dal file) è riuscito correttamente.
public void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei criteri di protezione (dal file) non è riuscito a causa di un errore.
public void OnCommitSuccess(bool commited, const std::shared_ptr<void>& context)  |  Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
public void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il commit delle modifiche al file non è riuscito a causa di un errore.
protected inline Observer()  |  
  
## <a name="members"></a>Membri
  
### <a name="observer"></a>~Observer
  
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