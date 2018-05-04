# <a name="class-mippolicyenginesettings"></a>Classe mip::PolicyEngine::Settings 
Un'istanza di questa classe con i parametri appropriati è necessaria per avviare un motore.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  Settings public inline  Settings public inline const std::string & GetId | Ottiene l'ID del motore. public inline void SetId | Imposta l'ID del motore. public inline const Identity & GetIdentity | Ottiene l'oggetto Identity.
public inline void SetIdentity | Imposta l'oggetto Identity.
public inline const std::string & GetClientData | Ottiene il set di dati client nelle impostazioni.
public inline void SetClientData | Imposta la stringa dei dati client.
public inline const std::string & GetLocale | Ottiene le impostazioni locali configurate nelle impostazioni.
public inline void SetCustomSettings | Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public inline const std::vector< std::pair< std::string, std::string > > & GetCustomSettings | Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public inline void SetSessionId | Imposta l'ID sessione, usato per la telemetria definita dal client.
public inline const std::string & GetSessionId | Ottiene l'ID sessione, un identificatore univoco.
## <a name="members"></a>Membri
### <a name="settings"></a>Impostazioni
Costruisce un'istanza con i parametri specificati. Usarlo per creare [Settings](#classmip_1_1_policy_engine_1_1_settings) per chiamare LoadEngineAsync per caricare un motore esistente.
#### <a name="parameters"></a>Parametri
* id Impostare sull'ID motore univoco generato da AddEngineAsync o su un valore generato automaticamente. Quando si carica un motore esistente, riutilizzare l'ID. In caso contrario verrà creato un nuovo motore. 
* clientData Dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 
* locale L'output localizzabile del motore verrà fornito con queste impostazioni locali. Il valore predefinito è "en-US".
### <a name="settings"></a>Impostazioni
Usarlo per creare [Settings](#classmip_1_1_policy_engine_1_1_settings) per chiamare AddEngineAsync per aggiungere un nuovo motore.
#### <a name="parameters"></a>Parametri
* identity Identificatore univoco dell'utente per il quale occorre aggiungere il motore. 
* clientData Dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 
* locale L'output localizzabile del motore verrà fornito con queste impostazioni locali. Il valore predefinito è "en-US".
### <a name="getid"></a>GetId
Ottiene l'ID del motore.
#### <a name="returns"></a>Returns
Stringa univoca che identifica il motore.
### <a name="setid"></a>SetId
Imposta l'ID del motore.
#### <a name="parameters"></a>Parametri
* id ID del motore.
### <a name="getidentity"></a>GetIdentity
Ottiene l'oggetto Identity.
#### <a name="returns"></a>Returns
Riferimento all'identità nell'oggetto Settings. 
**Vedere anche**: mip::Identity
### <a name="setidentity"></a>SetIdentity
Imposta l'oggetto Identity.
#### <a name="parameters"></a>Parametri
* identity Identificatore univoco di un utente. 
**Vedere anche**: mip::Identity
### <a name="getclientdata"></a>GetClientData
Ottiene il set di dati client configurato nelle impostazioni.
#### <a name="returns"></a>Returns
Stringa di dati specificata dal client.
### <a name="setclientdata"></a>SetClientData
Imposta la stringa di dati client.
#### <a name="parameters"></a>Parametri
* clientData Dati specificati dall'utente.
### <a name="getlocale"></a>GetLocale
Ottiene le impostazioni locali configurate nelle impostazioni.
#### <a name="returns"></a>Returns
Impostazioni locali.
### <a name="setcustomsettings"></a>SetCustomSettings
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
#### <a name="parameters"></a>Parametri
* customSettings Elenco di coppie nome/valore.
### <a name="getcustomsettings"></a>GetCustomSettings
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
#### <a name="parameters"></a>Parametri
* Elenco di coppie nome/valore.
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione, usato per la telemetria definita dal client.
#### <a name="parameters"></a>Parametri
* sessionId Stringa univoca che connette gli eventi di telemetria.
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione, un identificatore univoco.
#### <a name="returns"></a>Returns
ID sessione.