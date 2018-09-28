# <a name="class-mipconsent"></a>Classe mip::Consent 
Rappresenta l'accettazione o il rifiuto dell'esecuzione di un'azione da parte di un utente.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const mip::ConsentResult& Result() const  |  Ottiene il risultato di una richiesta di consenso.
 public void Result(const ConsentResult& value)  |  Imposta il risultato di una richiesta di consenso.
 public mip::ConsentType Type() const  |  Ottiene il tipo di consenso.
public const std::vector<std::string> Urls() const  |  Ottiene gli URL coinvolti nella richiesta di consenso.
 public const std::string User() const  |  Ottiene l'utente (indirizzo e-mail) da cui è richiesto il consenso.
 public const std::string Domain() const  |  Ottiene il dominio associato all'utente da cui è richiesto il consenso.
  
## <a name="members"></a>Membri
  
### <a name="mipconsentresult"></a>mip::ConsentResult
Ottiene il risultato di una richiesta di consenso.

  
**Restituisce**: risultato della richiesta di consenso
  
### <a name="result"></a>Risultato
Imposta il risultato di una richiesta di consenso.

Parametri:  
* **value**: risultato della richiesta di consenso


  
### <a name="mipconsenttype"></a>mip::ConsentType
Ottiene il tipo di consenso.

  
**Restituisce**: tipo di consenso
  
### <a name="urls"></a>Urls
Ottiene gli URL coinvolti nella richiesta di consenso.

  
**Restituisce**: URL coinvolti nella richiesta di consenso
  
### <a name="user"></a>Utente
Ottiene l'utente (indirizzo e-mail) da cui è richiesto il consenso.

  
**Restituisce**: utente da cui è richiesto il consenso
  
### <a name="domain"></a>Dominio
Ottiene il dominio associato all'utente da cui è richiesto il consenso.

  
**Restituisce**: dominio associato all'utente da cui è richiesto il consenso