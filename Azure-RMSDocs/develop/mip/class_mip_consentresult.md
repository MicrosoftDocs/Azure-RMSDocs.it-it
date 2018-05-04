# <a name="class-mipconsentresult"></a>Classe mip::ConsentResult 
Descrive i risultati della richiesta di consenso dopo l'interazione dell'utente.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  ConsentResult public inline bool Accepted | Ottiene un valore che indica se l'utente ha fornito il consenso per l'azione.
public inline bool ShowAgain |Ottiene un valore che indica se per le richieste future è necessario il consenso esplicito.
public inline const std::string & UserId | Ottiene l'utente (indirizzo e-mail) da cui è stato richiesto il consenso.
## <a name="members"></a>Membri
### <a name="consentresult"></a>ConsentResult
Costruttore [ConsentResult](#classmip_1_1_consent_result).
#### <a name="parameters"></a>Parametri
* accepted Indica se l'utente ha o meno fornito il consenso per l'azione 
* showAgain Indica se per le richieste di azione future è necessario il consenso esplicito 
* userId Utente (indirizzo e-mail) da cui è stato richiesto il consenso
### <a name="accepted"></a>Accettato
Ottiene un valore che indica se l'utente ha fornito il consenso per l'azione.
#### <a name="returns"></a>Returns
Valore che indica se l'utente ha fornito il consenso per l'azione
### <a name="showagain"></a>ShowAgain
Ottiene un valore che indica se per le richieste future è necessario il consenso esplicito.
#### <a name="returns"></a>Returns
Ottiene un valore che indica se per le richieste future è necessario il consenso esplicito. Se è True, l'SDK ricorderà il risultato e in futuro non richiederà il consenso all'applicazione client.
### <a name="userid"></a>UserId
Ottiene l'utente (indirizzo e-mail) da cui è stato richiesto il consenso.
#### <a name="returns"></a>Returns
Utente da cui è stato richiesto il consenso