# <a name="class-miprmslogicexception"></a>Classe mip::RMSLogicException 
Eccezione logica di RMS.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  RMSLogicExceptionErrorTypes error,const std::string & message) public inline  RMSLogicExceptionErrorTypes error,const char *const & message) public inline virtual const char * what | Ottiene il messaggio di eccezione.
public inline virtual ExceptionTypes type | Ottiene il tipo di eccezione.
public inline virtual int error | Ottiene il codice di errore.
## <a name="members"></a>Membri
### <a name="rmslogicexception"></a>RMSLogicException
Costruttore [RMSLogicException](#classmip_1_1_r_m_s_logic_exception).
#### <a name="parameters"></a>Parametri
* errore Codice [Error](#classmip_1_1_error) 
* message Messaggio di eccezione
### <a name="rmslogicexception"></a>RMSLogicException
Costruttore [RMSLogicException](#classmip_1_1_r_m_s_logic_exception).
#### <a name="parameters"></a>Parametri
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