# <a name="class-miprmsexception"></a>Classe mip::RMSException 
Eccezione di base di RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  Costruttore [RMSException](#classmip_1_1_r_m_s_exception).
public inline RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  Costruttore [RMSException](#classmip_1_1_r_m_s_exception).
public inline virtual const char* what() const  |  Ottiene il messaggio di eccezione.
public inline virtual ExceptionTypes type() const  |  Ottiene il tipo di eccezione.
public inline virtual int error() const  |  Ottiene il codice di errore.
  
## <a name="members"></a>Membri
  
### <a name="rmsexception"></a>RMSException
Costruttore [RMSException](#classmip_1_1_r_m_s_exception).
  
#### <a name="parameters"></a>Parametri
* type Tipo di eccezione 
* errore Codice [Error](#classmip_1_1_error) 
* message Messaggio di eccezione
  
### <a name="rmsexception"></a>RMSException
Costruttore [RMSException](#classmip_1_1_r_m_s_exception).
  
#### <a name="parameters"></a>Parametri
* type Tipo di eccezione 
* errore Codice [Error](#classmip_1_1_error) 
* message Messaggio di eccezione
  
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