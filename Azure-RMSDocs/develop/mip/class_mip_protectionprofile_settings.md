# <a name="class-mipprotectionprofilesettings"></a>Classe mip::ProtectionProfile::Settings 
Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).
 public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.
 public bool GetUseInMemoryStorage() const  |  Ottiene un valore indicante se le cache vengono archiviate o meno solo nella memoria (invece che su disco)
 public bool IsLicenseCachingEnabled() const  |  Ottiene un valore indicante se la memorizzazione nella cache delle licenze è abilitata o meno.
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per la connessione ai servizi.
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK di protezione.
 public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
 public bool IsTelemetryOptedOut() const  |  Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Usa l'implementazione del logger esterno.
 public bool GetSkipTelemetryInit() const  |  Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.
 public void SetSkipTelemetryInit()  |  Disabilita l'inizializzazione della telemetria.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).

Parametri:  
* **path**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione 


* **useInMemoryStorage**: archivia nella memoria invece che su disco gli stati memorizzati nella cache 


* **isLicenseCachingEnabled**: abilita o disabilita la memorizzazione nella cache delle licenze dell'SDK di protezione 


* **authDelegate**: oggetto di callback da usare per l'autenticazione, implemento dall'applicazione client 


* **observer**: istanza di [Observer](class_mip_protectionprofile_observer.md) che riceverà le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: informazioni relative all'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="getpath"></a>GetPath
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.

  
**Restituisce**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene un valore indicante se le cache vengono archiviate o meno solo nella memoria (invece che su disco)

  
**Restituisce**: true se le cache vengono archiviate solo nella memoria
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
Ottiene un valore indicante se la memorizzazione nella cache delle licenze è abilitata o meno.

  
**Restituisce**: true se la memorizzazione nella cache dell'SDK di protezione è abilitata
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="consentdelegate"></a>ConsentDelegate
Ottiene il delegato del consenso usato per la connessione ai servizi.

  
**Restituisce**: delegato del consenso usato per la connessione ai servizi
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md).

  
**Restituisce**: [observer](class_mip_protectionprofile_observer.md) che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK di protezione.

  
**Restituisce**: informazioni relative all'applicazione che sta utilizzando l'SDK di protezione
  
### <a name="optouttelemetry"></a>OptOutTelemetry
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno
  
### <a name="loggerdelegate"></a>LoggerDelegate
Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.

  
**Restituisce**: delegato del logger da usare per la registrazione
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Usa l'implementazione del logger esterno.
Deve essere chiamato dalle applicazioni client se vogliono usare l'implementazione del proprio logger
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.

  
**Restituisce**: valore che indica se l'inizializzazione della telemetria deve essere ignorata
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Disabilita l'inizializzazione della telemetria.
Normalmente non viene chiamato dalle applicazioni client, bensì usato dall'SDK per i file (che già inizializza la telemetria) per impedire la doppia inizializzazione
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione.

Parametri:  
* **sessionId**: ID sessione che verrà usato per la correlazione di log e telemetria


  
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione.

  
**Restituisce**:ID sessione che verrà usato per la correlazione di log e telemetria