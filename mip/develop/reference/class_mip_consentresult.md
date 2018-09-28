# <a name="class-mipconsentresult"></a>Classe mip::ConsentResult 
Descrive i risultati della richiesta di consenso dopo l'interazione dell'utente.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public ConsentResult(bool accepted, bool showAgain, const std::string& userId)  |  Costruttore [ConsentResult](class_mip_consentresult.md).
 public bool Accepted() const  |  Ottiene un valore che indica se l'utente ha fornito il consenso per l'azione.
 public bool ShowAgain() const  |  Ottiene un valore che indica se per le richieste future è necessario il consenso esplicito.
 public const std::string& UserId() const  |  Ottiene l'utente (indirizzo e-mail) da cui è stato richiesto il consenso.
  
## <a name="members"></a>Membri
  
### <a name="consentresult"></a>ConsentResult
Costruttore [ConsentResult](class_mip_consentresult.md).

Parametri:  
* **accepted**: indica se l'utente ha o meno fornito il consenso per l'azione 


* **showAgain**: indica se per le richieste di azione future è necessario il consenso esplicito 


* **userId**: utente (indirizzo di posta elettronica) da cui è stato richiesto il consenso


  
### <a name="accepted"></a>Accettato
Ottiene un valore che indica se l'utente ha fornito il consenso per l'azione.

  
**Restituisce**: valore che indica se l'utente ha fornito il consenso per l'azione
  
### <a name="showagain"></a>ShowAgain
Ottiene un valore che indica se per le richieste future è necessario il consenso esplicito.

  
**Restituisce**: valore che indica se per le richieste future è necessario il consenso esplicito. Se è true, l'SDK ricorderà il risultato e in futuro non richiederà il consenso all'applicazione client.
  
### <a name="userid"></a>UserId
Ottiene l'utente (indirizzo e-mail) da cui è stato richiesto il consenso.

  
**Restituisce**: utente da cui è stato richiesto il consenso