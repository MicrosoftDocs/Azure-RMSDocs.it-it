# <a name="class-mipfileprofileobserver"></a>Classe mip::FileProfile::Observer 
Interfaccia [Observer](#classmip_1_1_file_profile_1_1_observer) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Se si verifica un evento *Error, l'oggetto errore contiene la classe [mip::Error](#classmip_1_1_error). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline virtual  ~Observer | 
public inline virtual void OnLoadSuccessmip::FileProfile > & profile,const std::shared_ptr< void > & context) | Viene chiamato quando il profilo è stato caricato correttamente.
public inline virtual void OnLoadFailure | Viene chiamato quando il caricamento di un profilo ha causato un errore.
public inline virtual void OnListEnginesSuccess | Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public inline virtual void OnListEnginesError | Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
public inline virtual void OnUnloadEngineSuccess | Viene chiamato quando un motore è stato scaricato correttamente.
public inline virtual void OnUnloadEngineError | Viene chiamato quando lo scaricamento di un motore ha causato un errore.
public inline virtual void OnAddEngineSuccessmip::FileEngine > & engine,const std::shared_ptr< void > & context) | Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public inline virtual void OnAddEngineError | Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
public inline virtual void OnDeleteEngineSuccess | Viene chiamato quando un motore è stato eliminato correttamente.
public inline virtual void OnDeleteEngineError | Viene chiamato quando l'eliminazione di un motore ha causato un errore.
public inline virtual void OnPolicyChanged | Viene chiamato quando il criterio del motore con l'ID specificato è cambiato.
protected inline  Observer | 
## <a name="members"></a>Membri
### <a name="observer"></a>~Observer
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Viene chiamato quando l'elenco dei motori è stato generato correttamente.
### <a name="onlistengineserror"></a>OnListEnginesError
Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Viene chiamato quando un motore è stato scaricato correttamente.
### <a name="onunloadengineerror"></a>OnUnloadEngineError
Viene chiamato quando lo scaricamento di un motore ha causato un errore.
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
### <a name="onaddengineerror"></a>OnAddEngineError
Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Viene chiamato quando un motore è stato eliminato correttamente.
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Viene chiamato quando l'eliminazione di un motore ha causato un errore.
### <a name="onpolicychanged"></a>OnPolicyChanged
Viene chiamato quando il criterio del motore con l'ID specificato è cambiato.
### <a name="observer"></a>Osservatore