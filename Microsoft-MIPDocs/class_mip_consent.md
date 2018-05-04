# <a name="class-mipconsent"></a>Classe mip::Consent 
Rappresenta l'accettazione o il rifiuto dell'esecuzione di un'azione da parte di un utente.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const mip::ConsentResult & Result | Ottiene il risultato di una richiesta di consenso.
public void ResultConsentResult & value) | Imposta il risultato di una richiesta di consenso.
public mip::ConsentType Type | Ottiene il tipo di consenso.
public const std::vector< std::string > Urls | Ottiene gli URL coinvolti nella richiesta di consenso.
public const std::string User | Ottiene l'utente (indirizzo e-mail) da cui è richiesto il consenso.
public const std::string Domain | Ottiene il dominio associato all'utente da cui è richiesto il consenso.
## <a name="members"></a>Membri
### <a name="mipconsentresult"></a>mip::ConsentResult
Ottiene il risultato di una richiesta di consenso.
#### <a name="returns"></a>Returns
Risultato della richiesta di consenso
### <a name="result"></a>Risultato
Imposta il risultato di una richiesta di consenso.
#### <a name="parameters"></a>Parametri
* value Risultato della richiesta di consenso
### <a name="mipconsenttype"></a>mip::ConsentType
Ottiene il tipo di consenso.
#### <a name="returns"></a>Returns
Tipo di consenso
### <a name="urls"></a>Urls
Ottiene gli URL coinvolti nella richiesta di consenso.
#### <a name="returns"></a>Returns
URL coinvolti nella richiesta di consenso
### <a name="user"></a>Utente
Ottiene l'utente (indirizzo e-mail) da cui è richiesto il consenso.
#### <a name="returns"></a>Returns
Utente da cui è richiesto il consenso
### <a name="domain"></a>Dominio
Ottiene il dominio associato all'utente da cui è richiesto il consenso.
#### <a name="returns"></a>Returns
Dominio associato all'utente da cui è richiesto il consenso