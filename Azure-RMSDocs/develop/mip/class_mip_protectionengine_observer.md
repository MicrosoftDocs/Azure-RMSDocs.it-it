# <a name="class-mipprotectionengineobserver"></a>Classe mip::ProtectionEngine::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
Questa interfaccia deve implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei modelli genera un errore.
  
## <a name="members"></a>Membri
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri:  
* **templateIds**: riferimento all'elenco di modelli recuperati 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
Viene chiamato quando il recupero dei modelli genera un errore.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il recupero dei modelli 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)