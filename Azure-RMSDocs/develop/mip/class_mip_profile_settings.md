# <a name="class-mipprofilesettings"></a>Classe mip::Profile::Settings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaccia per la configurazione del profilo.
 public const std::string& GetPath() const  |  Ottiene il percorso dello stato archiviato.
 public bool GetUseInMemoryStorage() const  |  Ottiene il flag UseInMemoryStorage.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione.
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Ottiene l'observer di eventi.
 public const ApplicationInfo GetApplicationInfo() const  |  Ottiene le informazioni sull'applicazione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Interfaccia per la configurazione del profilo.

Parametri:  
* **path**: percorso di una directory in cui l'SDK archivierà lo stato del profilo. 


* **useInMemoryStorage**: flag che indica se lo stato deve essere o meno archiviato su disco. 


* **authDelegate**: delegato dell'autenticazione usato dall'SDK per acquisire i token di autenticazione. 


* **observer**: classe che implementa l'interfaccia [Profile::Observer](class_mip_profile_observer.md). Può essere nullptr. 


* **applicationInfo**: identificatori dell'applicazione usati per l'accesso al servizio.


  
### <a name="getpath"></a>GetPath
Ottiene il percorso dello stato archiviato.

  
**Restituisce**: percorso dello stato archiviato.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene il flag UseInMemoryStorage.

  
**Restituisce**: true se è impostato l'uso dell'archiviazione in memoria, false in caso contrario.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione.

  
**Restituisce**: delegato dell'autenticazione.
  
### <a name="profileobserver"></a>Profile::Observer
Ottiene l'observer di eventi.

  
**Restituisce**: observer di eventi.
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene le informazioni sull'applicazione.

  
**Restituisce**: informazioni sull'applicazione.