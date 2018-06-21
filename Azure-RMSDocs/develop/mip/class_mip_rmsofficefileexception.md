# <a name="class-miprmsofficefileexception"></a>Classe mip::RMSOfficeFileException 
Eccezione file di Office di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public RMSOfficeFileException(const std::string& message, Reason reason)  |  Costruttore [RMSOfficeFileException](class_mip_rmsofficefileexception.md).
 public RMSOfficeFileException(const char*const& message, Reason reason)  |  Costruttore [RMSOfficeFileException](class_mip_rmsofficefileexception.md).
 public virtual Reason reason() const  |  Ottiene la classificazione dell'errore file di Office.
 public virtual const char* what() const  |  Ottiene il messaggio di eccezione.
 public virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
 public virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Costruttore [RMSOfficeFileException](class_mip_rmsofficefileexception.md).

Parametri:  
* **message**: messaggio di eccezione 


* **reason**: classificazione dell'errore file di Office


  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Costruttore [RMSOfficeFileException](class_mip_rmsofficefileexception.md).

Parametri:  
* **message**: messaggio di eccezione 


* **reason**: classificazione dell'errore file di Office


  
### <a name="reason"></a>Motivo
Ottiene la classificazione dell'errore file di Office.

  
**Restituisce**: classificazione dell'errore file di Office
  
### <a name="what"></a>what
Ottiene il messaggio di eccezione.

  
**Restituisce**: messaggio di eccezione
  
### <a name="exceptiontypes"></a>ExceptionTypes
Ottiene il tipo di eccezione.

  
**Restituisce**: tipo di eccezione
  
### <a name="error"></a>Errore
Ottiene il codice di errore.

  
**Restituisce**: codice [error](class_mip_error.md)