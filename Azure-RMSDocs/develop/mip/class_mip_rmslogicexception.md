# <a name="class-miprmslogicexception"></a>Classe mip::RMSLogicException 
Eccezione logica di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public RMSLogicException(const ErrorTypes error, const std::string& message)  |  Costruttore [RMSLogicException](class_mip_rmslogicexception.md).
 public RMSLogicException(const ErrorTypes error, const char*const& message)  |  Costruttore [RMSLogicException](class_mip_rmslogicexception.md).
 public virtual const char* what() const  |  Ottiene il messaggio di eccezione.
 public virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
 public virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmslogicexception"></a>RMSLogicException
Costruttore [RMSLogicException](class_mip_rmslogicexception.md).

Parametri:  
* **error**: codice [Error](class_mip_error.md) 


* **message**: messaggio di eccezione


  
### <a name="rmslogicexception"></a>RMSLogicException
Costruttore [RMSLogicException](class_mip_rmslogicexception.md).

Parametri:  
* **error**: codice [Error](class_mip_error.md) 


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