# <a name="class-mipprofilesettings"></a>Classe mip::Profile::Settings 
Oggetto [Settings](class_mip_profile_settings.md) usato da [Profile](class_mip_profile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaccia per la configurazione del profilo.
 public const std::string& GetPath() const  |  Ottiene il percorso dello stato archiviato.
 public bool GetUseInMemoryStorage() const  |  Ottiene il flag UseInMemoryStorage.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione.
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Ottiene l'observer di eventi.
 public const ApplicationInfo GetApplicationInfo() const  |  Ottiene le informazioni sull'applicazione.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Usa l'implementazione del logger esterno.
 public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
 public bool IsTelemetryOptedOut() const  |  Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.
  
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
  
### <a name="loggerdelegate"></a>LoggerDelegate
Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.

  
**Restituisce**: delegato del logger da usare per la registrazione
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Usa l'implementazione del logger esterno.
Deve essere chiamato dalle applicazioni client se vogliono usare l'implementazione del proprio logger
  
### <a name="optouttelemetry"></a>OptOutTelemetry
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno