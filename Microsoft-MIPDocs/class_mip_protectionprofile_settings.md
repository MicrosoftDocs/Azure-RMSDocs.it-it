# <a name="class-mipprotectionprofilesettings"></a>Classe mip::ProtectionProfile::Settings 
Oggetto [Settings](#classmip_1_1_protection_profile_1_1_settings) usato da [ProtectionProfile](#classmip_1_1_protection_profile) durante la creazione e per tutta la sua durata.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  SettingsProtectionProfile::Observer > & observer,const ApplicationInfo & applicationInfo) public inline const std::string & GetPath | Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.
public inline const std::shared_ptr< ProtectionProfile::Observer > & GetObserver public inline const ApplicationInfo & GetApplicationInfo | Ottiene informazioni sull'applicazione che sta utilizzando l'SDK di protezione.
public inline bool GetSkipTelemetryInit | Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.
public inline void SetSkipTelemetryInit | Disabilita l'inizializzazione della telemetria.
public inline void SetSessionId | Imposta l'ID sessione. public inline const std::string & GetSessionId | Ottiene l'ID sessione.
## <a name="members"></a>Membri
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionProfile::Settings](#classmip_1_1_protection_profile_1_1_settings).
#### <a name="parameters"></a>Parametri
* path Percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione 
* observer Istanza di [Observer](#classmip_1_1_protection_profile_1_1_observer) che riceverà le notifiche degli eventi correlati a [ProtectionProfile](#classmip_1_1_protection_profile)
* applicationInfo Informazioni relative all'applicazione che sta utilizzando l'SDK di protezione
### <a name="getpath"></a>GetPath
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.
#### <a name="returns"></a>Returns
Percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](#classmip_1_1_protection_profile).
#### <a name="returns"></a>Returns
[Observer](#classmip_1_1_protection_profile_1_1_observer) che riceve le notifiche degli eventi correlati a [ProtectionProfile](#classmip_1_1_protection_profile)
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene informazioni relative all'applicazione che sta utilizzando l'SDK di protezione.
#### <a name="returns"></a>Returns
Informazioni relative all'applicazione che sta utilizzando l'SDK di protezione
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata.
#### <a name="returns"></a>Returns
Valore che indica se l'inizializzazione della telemetria deve essere ignorata
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Disabilita l'inizializzazione della telemetria.
Normalmente non viene chiamato dalle applicazioni client, bensì usato dall'SDK per i file (che già inizializza la telemetria) per impedire la doppia inizializzazione
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione.
#### <a name="parameters"></a>Parametri
* sessionId ID sessione che verrà usato per la correlazione di log e telemetria
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione.
#### <a name="returns"></a>Returns
ID sessione che verrà usato per la correlazione di log e telemetria