# <a name="class-mipgetuserpolicyresult"></a>Classe mip::GetUserPolicyResult 
Descrive i risultati di una richiesta di acquisizione criteri utente.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public GetUserPolicyResultStatus GetResultStatus()  |  Ottiene lo stato della richiesta di acquisizione criterio.
public std::shared_ptr<std::string> GetReferrer()  |  Ottiene l'indirizzo del referrer del criterio.
public std::shared_ptr<UserPolicy> GetPolicy()  |  Ottiene un'istanza di [UserPolicy](class_mip_userpolicy.md).
  
## <a name="members"></a>Membri
  
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
Ottiene lo stato della richiesta di acquisizione criterio.

  
**Restituisce**: stato della richiesta di acquisizione criterio
  
### <a name="getreferrer"></a>GetReferrer
Ottiene l'indirizzo del referrer del criterio.

  
**Restituisce**: indirizzo del referrer del criterio. Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="userpolicy"></a>UserPolicy
Ottiene un'istanza di [UserPolicy](class_mip_userpolicy.md).

  
**Restituisce**: istanza di [UserPolicy](class_mip_userpolicy.md) se l'acquisizione ha avuto esito positivo, in caso contrario nullptr