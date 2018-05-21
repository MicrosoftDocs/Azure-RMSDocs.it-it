# <a name="class-mipfileprofilesettings"></a>Classe mip::FileProfile::Settings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Interfaccia per la configurazione del profilo.
 public ~Settings()  | _Non ancora documentato._
 public const std::string& GetPath() const  | _Non ancora documentato._
 public bool GetUseInMemoryStorage() const  | _Non ancora documentato._
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  | _Non ancora documentato._
public std::shared_ptr<Observer> GetObserver() const  | _Non ancora documentato._
 public const ApplicationInfo GetApplicationInfo() const  | _Non ancora documentato._
 public bool GetSkipTelemetryInit() const  | _Non ancora documentato._
 public void SetSkipTelemetryInit()  | _Non ancora documentato._
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del profilo.
 public const std::string& GetSessionId() const  |  Restituisce l'ID sessione del profilo.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Interfaccia per la configurazione del profilo.

Parametri:  
* **observer**: classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). Può essere nullptr.


  
### <a name="settings"></a>~Settings
_Non ancora documentato._

  
### <a name="getpath"></a>GetPath
_Non ancora documentato._

  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
_Non ancora documentato._

  
### <a name="getauthdelegate"></a>GetAuthDelegate
_Non ancora documentato._

  
### <a name="observer"></a>Osservatore
_Non ancora documentato._

  
### <a name="applicationinfo"></a>ApplicationInfo
_Non ancora documentato._

  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
_Non ancora documentato._

  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
_Non ancora documentato._

  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione del profilo.
  
### <a name="getsessionid"></a>GetSessionId
Restituisce l'ID sessione del profilo.