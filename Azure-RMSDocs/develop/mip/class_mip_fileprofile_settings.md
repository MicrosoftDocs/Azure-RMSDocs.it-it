# <a name="class-mipfileprofilesettings"></a>Classe mip::FileProfile::Settings 
Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).
 public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
 public bool GetUseInMemoryStorage() const  |  Ottiene un valore indicante se tutti gli stati devono essere archiviati o meno in memoria (invece che su disco)
 public bool IsLicenseCachingEnabled() const  |  Ottiene un valore indicante se la memorizzazione nella cache delle licenze è abilitata o meno.
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.
public std::shared_ptr<Observer> GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).
 public const ApplicationInfo GetApplicationInfo() const  |  Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK.
 public bool GetSkipTelemetryInit() const  |  Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.
 public void SetSkipTelemetryInit()  |  Disabilita l'inizializzazione della telemetria.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Usa l'implementazione del logger esterno.
 public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
 public bool IsTelemetryOptedOut() const  |  Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parametri:  
* **path**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti 


* **useInMemoryStorage**: valore indicante se tutti gli stati devono essere archiviati o meno in memoria (invece che su disco) 


* **isLicenseCachingEnabled**: abilita o disabilita la memorizzazione nella cache delle licenze di protezione 


* **authDelegate**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione 


* **observer**: istanza di [Observer](class_mip_fileprofile_observer.md) che riceverà le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md)


* **applicationInfo**: informazioni relative all'applicazione che sta utilizzando l'SDK


  
### <a name="getpath"></a>GetPath
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.

  
**Restituisce**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene un valore indicante se tutti gli stati devono essere archiviati o meno in memoria (invece che su disco)

  
**Restituisce**: valore indicante se tutti gli stati devono essere archiviati o meno in memoria (invece che su disco)
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
Ottiene un valore indicante se la memorizzazione nella cache delle licenze è abilitata o meno.

  
**Restituisce**: true se le cache vengono archiviate solo nella memoria
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="consentdelegate"></a>ConsentDelegate
Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.

  
**Restituisce**: delegato del consenso usato per richiedere il consenso dell'utente
  
### <a name="observer"></a>Osservatore
Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).

  
**Restituisce**: [observer](class_mip_fileprofile_observer.md) che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK.

  
**Restituisce**: informazioni relative all'applicazione che sta utilizzando l'SDK
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.

  
**Restituisce**: valore che indica se l'inizializzazione della telemetria deve essere ignorata
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Disabilita l'inizializzazione della telemetria.
Normalmente non viene chiamato dalle applicazioni client, bensì usato dall'SDK per i file (che già inizializza la telemetria) per impedire la doppia inizializzazione
  
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
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione.

Parametri:  
* **sessionId**: ID sessione che verrà usato per la correlazione di log e telemetria


  
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione.

  
**Restituisce**:ID sessione che verrà usato per la correlazione di log e telemetria