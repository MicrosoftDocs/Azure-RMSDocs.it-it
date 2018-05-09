# <a name="class-miprmsofficefileexception"></a>Classe mip::RMSOfficeFileException 
Eccezione file di Office di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline RMSOfficeFileException(const std::string& message, Reason reason)  |  Costruttore [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
public inline RMSOfficeFileException(const char*const& message, Reason reason)  |  Costruttore [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
public inline virtual Reason reason() const  |  Ottiene la classificazione dell'errore file di Office.
public inline virtual const char* what() const  |  Ottiene il messaggio di eccezione.
public inline virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
public inline virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Costruttore [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
  
#### <a name="parameters"></a>Parametri
* message Messaggio di eccezione 
* reason Classificazione dell'errore file di Office
  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Costruttore [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
  
#### <a name="parameters"></a>Parametri
* message Messaggio di eccezione 
* reason Classificazione dell'errore file di Office
  
### <a name="reason"></a>Motivo
Ottiene la classificazione dell'errore file di Office.
  
#### <a name="returns"></a>Returns
Classificazione dell'errore file di Office
  
### <a name="what"></a>what
Ottiene il messaggio di eccezione.
  
#### <a name="returns"></a>Returns
Messaggio di eccezione
  
### <a name="exceptiontypes"></a>ExceptionTypes
Ottiene il tipo di eccezione.
  
#### <a name="returns"></a>Returns
Tipo di eccezione
  
### <a name="error"></a>Errore
Ottiene il codice di errore.
  
#### <a name="returns"></a>Returns
Codice di [errore](#classmip_1_1_error)