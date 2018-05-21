# <a name="class-miprmsnetworkexception"></a>Classe mip::RMSNetworkException 
Eccezione di rete di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public RMSNetworkException(const std::string& message, Reason reason)  |  Costruttore [RMSNetworkException](class_mip_rmsnetworkexception.md).
 public RMSNetworkException(const char*const& message, Reason reason)  |  Costruttore [RMSNetworkException](class_mip_rmsnetworkexception.md).
 public virtual Reason reason() const  |  Ottiene la classificazione dell'errore di rete.
 public virtual const char* what() const  |  Ottiene il messaggio di eccezione.
 public virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
 public virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmsnetworkexception"></a>RMSNetworkException
Costruttore [RMSNetworkException](class_mip_rmsnetworkexception.md).

Parametri:  
* **message**: messaggio di eccezione 


* **reason**: classificazione dell'errore di rete


  
### <a name="rmsnetworkexception"></a>RMSNetworkException
Costruttore [RMSNetworkException](class_mip_rmsnetworkexception.md).

Parametri:  
* **message**: messaggio di eccezione 


* **reason**: classificazione dell'errore di rete


  
### <a name="reason"></a>Motivo
Ottiene la classificazione dell'errore di rete.

  
**Restituisce**: classificazione dell'errore di rete
  
### <a name="what"></a>what
Ottiene il messaggio di eccezione.

  
**Restituisce**: messaggio di eccezione
  
### <a name="exceptiontypes"></a>ExceptionTypes
Ottiene il tipo di eccezione.

  
**Restituisce**: tipo di eccezione
  
### <a name="error"></a>Errore
Ottiene il codice di errore.

  
**Restituisce**: codice [error](class_mip_error.md)