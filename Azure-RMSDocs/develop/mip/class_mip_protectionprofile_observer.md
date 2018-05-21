# <a name="class-mipprotectionprofileobserver"></a>Classe mip::ProtectionProfile::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
Questa interfaccia deve implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
  
## <a name="members"></a>Membri
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: riferimento all'oggetto [ProtectionProfile](class_mip_protectionprofile.md) appena creato


* **context**: lo stesso contesto passato a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il caricamento 


* **context**: lo stesso contesto passato a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)