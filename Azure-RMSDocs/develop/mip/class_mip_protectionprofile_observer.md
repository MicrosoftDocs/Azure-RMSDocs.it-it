# <a name="class-mipprotectionprofileobserver"></a>Classe mip::ProtectionProfile::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
Questa interfaccia deve implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'eliminazione di un motore ha restituito un errore.
  
## <a name="members"></a>Membri
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: riferimento all'oggetto [ProtectionProfile](class_mip_protectionprofile.md) appena creato


* **context**: lo stesso contesto passato a ProtectionProfile::LoadAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a ProtectionProfile::LoadAsync e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il caricamento 


* **context**: lo stesso contesto passato a ProtectionProfile::LoadAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a ProtectionProfile::LoadAsync e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **context**: contesto passato all'operazione.


  
### <a name="onlistengineserror"></a>OnListEnginesError
Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: contesto passato all'operazione.


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
  
### <a name="onaddengineerror"></a>OnAddEngineError
Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: contesto passato all'operazione.


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **context**: contesto passato all'operazione.


  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Viene chiamato quando l'eliminazione di un motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: contesto passato all'operazione.

