# <a name="class-mipprotectionengine"></a>Classe mip::ProtectionEngine 
Esegue azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione dalla forma serializzata.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni del motore.

  
**Restituisce**: impostazioni del motore
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **observer**: classe che implementa l'interfaccia [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: questo stesso contesto verrà inoltrato a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)


  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **descriptor**: [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: questo stesso contesto verrà inoltrato a [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) o ProtectionHandler::Observer::OnCreateProtectionHandlerFailure


  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
Crea un gestore di protezione dalla forma serializzata.

Parametri:  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: questo stesso contesto verrà inoltrato a [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) o ProtectionHandler::Observer::OnCreateProtectionHandlerFailure

