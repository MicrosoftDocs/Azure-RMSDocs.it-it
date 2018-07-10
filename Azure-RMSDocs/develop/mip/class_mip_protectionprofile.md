# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
Un'applicazione deve creare [ProtectionProfile](class_mip_protectionprofile.md) prima di eseguire qualsiasi operazione di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Avvia l'operazione di elenco motori.
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati completamente.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: [impostazioni](class_mip_protectionprofile_settings.md) usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica i parametri del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati completamente.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).