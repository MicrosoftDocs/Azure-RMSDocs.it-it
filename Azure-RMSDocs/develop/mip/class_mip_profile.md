# <a name="class-mipprofile"></a>Classe mip::Profile 
[Profile](#classmip_1_1_profile) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [Profile](#classmip_1_1_profile), ma se necessario può creare più profili.
  
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
  
#### <a name="returns"></a>Returns
Impostazioni configurate nel profilo.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.
  
#### <a name="parameters"></a>Parametri
* context Parametro che verrà passato alle funzioni observer. 
In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](#classmip_1_1_profile_1_1_observer).
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Avvia lo scaricamento del motore dei criteri con l'ID specificato.
  
#### <a name="parameters"></a>Parametri
* id ID univoco del motore. 
* context Parametro che verrà passato alle funzioni observer. 
In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](#classmip_1_1_profile_1_1_observer).
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
  
#### <a name="parameters"></a>Parametri
* settings Oggetto [mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings) che specifica i parametri del motore. 
* context Parametro che verrà passato alle funzioni observer. 
In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](#classmip_1_1_profile_1_1_observer).
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.
  
#### <a name="parameters"></a>Parametri
* id ID univoco del motore. 
* context Parametro che verrà passato alle funzioni observer. 
In base all'esito positivo o negativo dell'operazione verrà chiamato [Profile::Observer](#classmip_1_1_profile_1_1_observer).