# <a name="class-miperror"></a>Classe mip::Error 
Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline char const  * what | Ottiene un messaggio di errore cstring.
public std::shared_ptr< Error > Clone | Clona l'errore.
public inline virtual ErrorType GetErrorType | Ottiene il tipo di errore.
public inline virtual const std::string & GetErrorName | Ottiene il nome dell'errore.
public inline virtual const std::string & GetMessage | Ottiene il messaggio di errore.
public inline virtual void SetMessage | Imposta il messaggio di errore.
## <a name="members"></a>Membri
### <a name="what"></a>what
Ottiene un messaggio di errore cstring.
#### <a name="returns"></a>Returns
Messaggio di errore cstring
### <a name="error"></a>Errore
Clona l'errore.
#### <a name="returns"></a>Returns
Un clone dell'errore.
### <a name="errortype"></a>ErrorType
Ottiene il tipo di errore.
#### <a name="returns"></a>Returns
Il tipo di errore.
### <a name="geterrorname"></a>GetErrorName
Ottiene il nome dell'errore.
#### <a name="returns"></a>Returns
Il nome dell'errore.
### <a name="getmessage"></a>GetMessage
Ottiene il messaggio di errore.
#### <a name="returns"></a>Returns
Il messaggio di errore.
### <a name="setmessage"></a>SetMessage
Imposta il messaggio di errore.
#### <a name="parameters"></a>Parametri
* msg Messaggio di errore.