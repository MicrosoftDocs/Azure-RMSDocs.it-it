# <a name="class-mipjustificationrequirederror"></a>Classe mip::JustificationRequiredError 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline JustificationRequiredError()  |  
public inline virtual std::shared_ptr<Error> Clone() const  |  Clona l'errore.
public inline char const* what() const  |  Ottiene un messaggio di errore cstring.
public inline virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public inline virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public inline virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public inline virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="justificationrequirederror"></a>JustificationRequiredError
  
### <a name="error"></a>Errore
Clona l'errore.
  
#### <a name="returns"></a>Returns
Un clone dell'errore.
  
### <a name="what"></a>what
Ottiene un messaggio di errore cstring.
  
#### <a name="returns"></a>Returns
Messaggio di errore cstring
  
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