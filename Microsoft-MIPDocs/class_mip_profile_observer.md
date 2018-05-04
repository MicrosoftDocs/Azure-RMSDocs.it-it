# <a name="class-mipprofileobserver"></a>Classe mip::Profile::Observer 
Interfaccia [Observer](#classmip_1_1_profile_1_1_observer) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Se si verifica un evento *Error, l'oggetto errore contiene la classe [mip::Error](#classmip_1_1_error). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProfile > & profile,const std::shared_ptr< void > & context) | Viene chiamato quando il profilo è stato caricato correttamente.
public inline virtual void OnLoadFailure | Viene chiamato quando il caricamento di un profilo ha causato un errore.
public inline virtual void OnListEnginesSuccess | Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public inline virtual void OnListEnginesError | Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
public inline virtual void OnUnloadEngineSuccess | Viene chiamato quando un motore è stato scaricato correttamente.
public inline virtual void OnUnloadEngineError | Viene chiamato quando lo scaricamento di un motore ha causato un errore.
public inline virtual void OnAddEngineSuccessPolicyEngine > & engine,const std::shared_ptr< void > & context) | Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public inline virtual void OnAddEngineError | Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
public inline virtual void OnDeleteEngineSuccess | Viene chiamato quando un motore è stato eliminato correttamente.
public inline virtual void OnDeleteEngineError | Viene chiamato quando l'eliminazione di un motore ha causato un errore.
public inline virtual void OnPolicyChanged | Viene chiamato quando il criterio del motore con l'ID specificato è cambiato.
## <a name="members"></a>Membri
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.
#### <a name="parameters"></a>Parametri
* profile Profilo corrente usato per avviare l'operazione. 
* context Contesto passato all'operazione.
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.
#### <a name="parameters"></a>Parametri
* error Errore che ha causato il fallimento dell'operazione di caricamento. 
* context Contesto passato all'operazione.
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Viene chiamato quando l'elenco dei motori è stato generato correttamente.
#### <a name="parameters"></a>Parametri
* engineIds Elenco degli ID motore disponibili. 
* context Contesto passato all'operazione.
### <a name="onlistengineserror"></a>OnListEnginesError
Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
#### <a name="parameters"></a>Parametri
* error Errore che ha causato il fallimento dell'operazione di elenco motori. 
* context Contesto passato all'operazione.
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Viene chiamato quando un motore è stato scaricato correttamente.
#### <a name="parameters"></a>Parametri
* context Contesto passato all'operazione.
### <a name="onunloadengineerror"></a>OnUnloadEngineError
Viene chiamato quando lo scaricamento di un motore ha causato un errore.
#### <a name="parameters"></a>Parametri
* error Errore che ha causato il fallimento dell'operazione di scaricamento motore. 
* context Contesto passato all'operazione.
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
### <a name="onaddengineerror"></a>OnAddEngineError
Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
#### <a name="parameters"></a>Parametri
* error Errore che ha causato il fallimento dell'operazione di aggiunta motore. 
* context Contesto passato all'operazione.
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Viene chiamato quando un motore è stato eliminato correttamente.
#### <a name="parameters"></a>Parametri
* context Contesto passato all'operazione.
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Viene chiamato quando l'eliminazione di un motore ha causato un errore.
#### <a name="parameters"></a>Parametri
* error Errore che ha causato il fallimento dell'operazione di eliminazione motore. 
* context Contesto passato all'operazione.
### <a name="onpolicychanged"></a>OnPolicyChanged
Viene chiamato quando il criterio del motore con l'ID specificato è cambiato.
#### <a name="parameters"></a>Parametri
* engineId Il motore. Per caricare il nuovo criterio è necessario chiamare di nuovo AddEngineAsync con l'ID motore specificato.