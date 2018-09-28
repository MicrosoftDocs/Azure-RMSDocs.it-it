# <a name="class-mipfileprofile"></a>Classe mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione tipica avrà bisogno di un solo [Profile](class_mip_profile.md), ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Restituisce le impostazioni del profilo.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Avvia lo scaricamento del motore di file con l'ID specificato. In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore di file al profilo.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati completamente.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).