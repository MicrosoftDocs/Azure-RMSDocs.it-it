# <a name="class-mipfileprofile"></a>Classe mip::FileProfile 
[FileProfile](#classmip_1_1_file_profile) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione tipica avrà bisogno di un solo [Profile](#classmip_1_1_profile), ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline virtual ~FileProfile()  |  
public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.
protected inline FileProfile()  |  
  
## <a name="members"></a>Membri
  
### <a name="fileprofile"></a>~FileProfile
  
### <a name="settings"></a>Impostazioni
Restituisce le impostazioni del profilo.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer).
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Avvia lo scaricamento del motore di file con l'ID specificato. In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer).
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore di file al profilo.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer).
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer).
  
### <a name="fileprofile"></a>FileProfile