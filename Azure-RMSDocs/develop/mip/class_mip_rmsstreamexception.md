# <a name="class-miprmsstreamexception"></a>Classe mip::RMSStreamException 
Eccezione flusso di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public RMSStreamException(const std::string& message)  |  Costruttore [RMSStreamException](class_mip_rmsstream_exception.md).
 public RMSStreamException(const char*const& message)  |  Costruttore [RMSStreamException](class_mip_rmsstream_exception.md).
 public virtual const char* what() const  |  Ottiene il messaggio di eccezione.
 public virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
 public virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmsstreamexception"></a>RMSStreamException
Costruttore [RMSStreamException](class_mip_rmsstream_exception.md).

Parametri:  
* **message**: messaggio di eccezione


  
### <a name="rmsstreamexception"></a>RMSStreamException
Costruttore [RMSStreamException](class_mip_rmsstream_exception.md).

Parametri:  
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