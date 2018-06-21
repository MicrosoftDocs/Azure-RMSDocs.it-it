# <a name="class-mipprotectionprofilesettings"></a>Classe mip::ProtectionProfile::Settings 
Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).
 public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK di protezione.
 public bool GetSkipTelemetryInit() const  |  Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.
 public void SetSkipTelemetryInit()  |  Disabilita l'inizializzazione della telemetria.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).

Parametri:  
* **path**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione 


* **observer**: istanza di [Observer](class_mip_protectionprofile_observer.md) che riceverà le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: informazioni relative all'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="getpath"></a>GetPath
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.

  
**Restituisce**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md).

  
**Restituisce**: [observer](class_mip_protectionprofile_observer.md) che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK di protezione.

  
**Restituisce**: informazioni relative all'applicazione che sta utilizzando l'SDK di protezione
  
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