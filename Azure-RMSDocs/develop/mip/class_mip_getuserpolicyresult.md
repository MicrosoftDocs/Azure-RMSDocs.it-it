# <a name="class-mipgetuserpolicyresult"></a>Classe mip::GetUserPolicyResult 
Descrive i risultati di una richiesta di acquisizione criteri utente.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public GetUserPolicyResultStatus GetResultStatus | Ottiene lo stato della richiesta di acquisizione criterio.
public std::shared_ptr< std::string > GetReferrer | Ottiene l'indirizzo del referrer del criterio.
public std::shared_ptr< UserPolicy > GetPolicy
## <a name="members"></a>Membri
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
Ottiene lo stato della richiesta di acquisizione criterio.
#### <a name="returns"></a>Returns
Stato della richiesta di acquisizione criterio
### <a name="getreferrer"></a>GetReferrer
Ottiene l'indirizzo del referrer del criterio.
#### <a name="returns"></a>Returns
Indirizzo del referrer del criterio. Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
### <a name="userpolicy"></a>UserPolicy
Ottiene un'istanza di [UserPolicy](#classmip_1_1_user_policy).
#### <a name="returns"></a>Returns
Istanza di [UserPolicy](#classmip_1_1_user_policy) se l'acquisizione ha avuto esito positivo, in caso contrario nullptr