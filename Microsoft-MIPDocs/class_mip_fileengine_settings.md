# <a name="class-mipfileenginesettings"></a>Classe mip::FileEngine::Settings 
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  Settings | Crea un'istanza con i parametri specificati.
public inline  Settings | Crea un'istanza con i parametri specificati.
public inline const std::string & GetId | Restituisce l'ID motore.
public inline const Identity & GetIdentity | Restituisce l'identità del motore.
public inline void SetIdentity | Imposta l'identità del motore.
public inline const std::string & GetClientData | Restituisce i dati client del motore.
public inline const std::string & GetLocale | Restituisce le impostazioni locali del motore.
public inline void SetCustomSettings | Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public inline const std::vector< std::pair< std::string, std::string > > & GetCustomSettings | Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public inline void SetSessionId | Imposta l'ID sessione del motore.
public inline const std::string & GetSessionId | Restituisce l'ID sessione del motore.
## <a name="members"></a>Membri
### <a name="settings"></a>Impostazioni
Crea un'istanza con i parametri specificati.
Usarlo per creare [Settings](#classmip_1_1_file_engine_1_1_settings) per chiamare LoadEngineAsync per caricare un motore esistente (in precedenza l'aggiunta si eseguiva con AddEngineAsync).
#### <a name="parameters"></a>Parametri
* id Impostare sull'ID motore univoco generato da AddEngineAsync.
### <a name="settings"></a>Impostazioni
Crea un'istanza con i parametri specificati.
Usarlo per creare [Settings](#classmip_1_1_file_engine_1_1_settings) per chiamare AddEngineAsync per aggiungere un nuovo motore.
#### <a name="parameters"></a>Parametri
* identity Informazioni di identità relative all'utente per il quale occorre aggiungere il motore.
### <a name="getid"></a>GetId
Restituisce l'ID motore.
### <a name="getidentity"></a>GetIdentity
Restituisce l'identità del motore.
### <a name="setidentity"></a>SetIdentity
Imposta l'identità del motore.
### <a name="getclientdata"></a>GetClientData
Restituisce i dati client del motore.
### <a name="getlocale"></a>GetLocale
Restituisce le impostazioni locali del motore.
### <a name="setcustomsettings"></a>SetCustomSettings
Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
### <a name="getcustomsettings"></a>GetCustomSettings
Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione del motore.
### <a name="getsessionid"></a>GetSessionId
Restituisce l'ID sessione del motore.