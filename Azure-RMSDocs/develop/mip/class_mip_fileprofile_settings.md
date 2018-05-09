# <a name="class-mipfileprofilesettings"></a>Classe mip::FileProfile::Settings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Interfaccia per la configurazione del profilo.
public inline ~Settings()  |  
public inline const std::string& GetPath() const  |  
public inline bool GetUseInMemoryStorage() const  |  
public inline std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  
public inline std::shared_ptr<Observer> GetObserver() const  |  
public inline const ApplicationInfo GetApplicationInfo() const  |  
public inline bool GetSkipTelemetryInit() const  |  
public inline void SetSkipTelemetryInit()  |  
public inline void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del profilo.
public inline const std::string& GetSessionId() const  |  Restituisce l'ID sessione del profilo.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Interfaccia per la configurazione del profilo.
  
#### <a name="parameters"></a>Parametri
* observer Classe che implementa l'interfaccia [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer). Può essere nullptr.
  
### <a name="settings"></a>~Settings
  
### <a name="getpath"></a>GetPath
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
  
### <a name="getauthdelegate"></a>GetAuthDelegate
  
### <a name="observer"></a>Osservatore
  
### <a name="applicationinfo"></a>ApplicationInfo
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione del profilo.
  
### <a name="getsessionid"></a>GetSessionId
Restituisce l'ID sessione del profilo.