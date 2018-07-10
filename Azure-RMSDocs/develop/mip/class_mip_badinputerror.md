# <a name="class-mipbadinputerror"></a>Classe mip::BadInputError 
Errore di input errato, generato quando l'input per un'API SDK non è valido.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public char const* what() const  |  Ottiene un messaggio di errore cstring.
public std::shared_ptr<Error> Clone() const  |  Clona l'errore.
 public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
 public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
 public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
 public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="what"></a>what
Ottiene un messaggio di errore cstring.

  
**Restituisce**: messaggio di errore cstring
  
### <a name="error"></a>Errore
Clona l'errore.

  
**Restituisce**: clone dell'errore.
  
### <a name="errortype"></a>ErrorType
Ottiene il tipo di errore.

  
**Restituisce**: tipo di errore.
  
### <a name="geterrorname"></a>GetErrorName
Ottiene il nome dell'errore.

  
**Restituisce**: nome dell'errore.
  
### <a name="getmessage"></a>GetMessage
Ottiene il messaggio di errore.

  
**Restituisce**: messaggio di errore.
  
### <a name="setmessage"></a>SetMessage
Imposta il messaggio di errore.

Parametri:  
* **msg**: messaggio di errore.

