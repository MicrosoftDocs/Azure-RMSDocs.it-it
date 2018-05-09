# <a name="class-mipprofilesettings"></a>Classe mip::Profile::Settings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaccia per la configurazione del profilo.
public inline const std::string& GetPath() const  |  Ottiene il percorso dello stato archiviato.
public inline bool GetUseInMemoryStorage() const  |  Ottiene il flag UseInMemoryStorage.
public inline const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione.
public inline const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Ottiene l'observer di eventi.
public inline const ApplicationInfo GetApplicationInfo() const  |  Ottiene le informazioni sull'applicazione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Interfaccia per la configurazione del profilo.
  
#### <a name="parameters"></a>Parametri
* path Percorso di una directory in cui l'SDK archivierà lo stato del profilo. 
* useInMemoryStorage Flag che indica se lo stato deve essere o meno archiviato su disco. 
* authDelegate Delegato dell'autenticazione usato dall'SDK per acquisire i token di autenticazione. 
* observer Classe che implementa l'interfaccia [Profile::Observer](#classmip_1_1_profile_1_1_observer). Può essere nullptr. 
* applicationInfo Identificatori dell'applicazione usati per l'accesso al servizio.
  
### <a name="getpath"></a>GetPath
Ottiene il percorso dello stato archiviato.
  
#### <a name="returns"></a>Returns
Percorso dello stato archiviato.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene il flag UseInMemoryStorage.
  
#### <a name="returns"></a>Returns
True se è impostato l'uso dell'archiviazione in memoria, false in caso contrario.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione.
  
#### <a name="returns"></a>Returns
Delegato dell'autenticazione.
  
### <a name="profileobserver"></a>Profile::Observer
Ottiene l'observer di eventi.
  
#### <a name="returns"></a>Returns
Observer di eventi.
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene le informazioni sull'applicazione.
  
#### <a name="returns"></a>Returns
Informazioni sull'applicazione.