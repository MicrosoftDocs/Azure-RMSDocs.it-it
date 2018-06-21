# <a name="class-miprmsexception"></a>Classe mip::RMSException 
Eccezione di base di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  Costruttore [RMSException](class_mip_rmsexception.md).
 public RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  Costruttore [RMSException](class_mip_rmsexception.md).
 public virtual const char* what() const  |  Ottiene il messaggio di eccezione.
 public virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
 public virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmsexception"></a>RMSException
Costruttore [RMSException](class_mip_rmsexception.md).

Parametri:  
* **type**: tipo di eccezione 


* **error**: codice [error](class_mip_error.md) 


* **message**: messaggio di eccezione


  
### <a name="rmsexception"></a>RMSException
Costruttore [RMSException](class_mip_rmsexception.md).

Parametri:  
* **type**: tipo di eccezione 


* **error**: codice [error](class_mip_error.md) 


* **message**: messaggio di eccezione


  
### <a name="what"></a>what
Ottiene il messaggio di eccezione.

  
**Restituisce**: messaggio di eccezione
  
### <a name="exceptiontypes"></a>ExceptionTypes
Ottiene il tipo di eccezione.

  
**Restituisce**: tipo di eccezione
  
### <a name="error"></a>Errore
Ottiene il codice di errore.

  
**Restituisce**: codice [error](class_mip_error.md)