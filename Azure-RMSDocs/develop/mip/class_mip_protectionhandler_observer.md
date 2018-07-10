# <a name="class-mipprotectionhandlerobserver"></a>Classe mip::ProtectionHandler::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
Questa interfaccia deve implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.
public virtual void OnCreateProtectionHandlerError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.
  
## <a name="members"></a>Membri
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.

Parametri:  
* **protectionHandler**: nuovo [ProtectionHandler](class_mip_protectionhandler.md) creato


* **context**: lo stesso contesto passato a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function e così via) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) e quello stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlererror"></a>OnCreateProtectionHandlerError
Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante la creazione 


* **context**: lo stesso contesto passato a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function e così via) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) e quello stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure