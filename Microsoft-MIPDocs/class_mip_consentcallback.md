# <a name="class-mipconsentcallback"></a>Classe mip::ConsentCallback 
Interfaccia per le notifiche di richiesta di consenso.
Questo callback viene implementato da un'applicazione client per sapere quando è necessario mostrare all'utente una notifica di consenso.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public ConsentList ConsentsConsentList & consents) | Viene chiamato quando l'SDK richiede il consenso dell'utente per un'operazione.
## <a name="members"></a>Membri
### <a name="consentlist"></a>ConsentList
Viene chiamato quando l'SDK richiede il consenso dell'utente per un'operazione.
#### <a name="parameters"></a>Parametri
* consents Elenco di consensi richiesti dall'SDK
#### <a name="returns"></a>Returns
Risultati [Consent](#classmip_1_1_consent) Quando l'SDK richiede consensi, l'applicazione client deve ottenere il consenso da parte dell'utente, i risultati di ogni consenso devono essere archiviati tramite [Consent::Result(const ConsentResult&)](#classmip_1_1_consent_1ad6c17d9af548a40b2fe854fe0d9bca64) e deve essere restituito un elenco dei consensi risolti.