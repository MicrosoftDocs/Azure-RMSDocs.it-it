# <a name="class-miprmspfileexception"></a>Classe mip::RMSPFileException 
Eccezione PFile di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public RMSPFileException(const std::string& message, Reason reason)  |  Costruttore [RMSPFileException](class_mip_rmspfileexception.md).
 public RMSPFileException(const char*const& message, Reason reason)  |  Costruttore [RMSPFileException](class_mip_rmspfileexception.md).
 public virtual Reason reason() const  |  Ottiene la classificazione dell'errore PFile.
 public virtual const char* what() const  |  Ottiene il messaggio di eccezione.
 public virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
 public virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmspfileexception"></a>RMSPFileException
Costruttore [RMSPFileException](class_mip_rmspfileexception.md).

Parametri:  
* **message**: messaggio di eccezione 


* **reason**: classificazione dell'errore PFile


  
### <a name="rmspfileexception"></a>RMSPFileException
Costruttore [RMSPFileException](class_mip_rmspfileexception.md).

Parametri:  
* **message**: messaggio di eccezione 


* **reason**: classificazione dell'errore PFile


  
### <a name="reason"></a>Motivo
Ottiene la classificazione dell'errore PFile.

  
**Restituisce**: classificazione dell'errore PFile
  
### <a name="what"></a>what
Ottiene il messaggio di eccezione.

  
**Restituisce**: messaggio di eccezione
  
### <a name="exceptiontypes"></a>ExceptionTypes
Ottiene il tipo di eccezione.

  
**Restituisce**: tipo di eccezione
  
### <a name="error"></a>Errore
Ottiene il codice di errore.

  
**Restituisce**: codice [error](class_mip_error.md)