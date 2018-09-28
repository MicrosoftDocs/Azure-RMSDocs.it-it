# <a name="class-mipprofile"></a>Classe mip::Profile 
[Profile](class_mip_profile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [Profile](class_mip_profile.md), ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni configurate nel profilo.

  
**Restituisce**: impostazioni configurate nel profilo.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](class_mip_profile_observer.md).
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](class_mip_profile_observer.md).
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore dei criteri al profilo.

Parametri:  
* **settings**: the [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) object that specifies the engines parameters. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](class_mip_profile_observer.md).
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](class_mip_profile_observer.md).