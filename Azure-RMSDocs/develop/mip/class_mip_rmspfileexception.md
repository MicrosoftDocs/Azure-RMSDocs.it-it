# <a name="class-miprmspfileexception"></a>Classe mip::RMSPFileException 
Eccezione PFile di RMS.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  RMSPFileExceptionReason reason) public inline  RMSPFileExceptionReason reason) public inline virtual Reason reason | Ottiene la classificazione dell'errore PFile.
public inline virtual const char * what | Ottiene il messaggio di eccezione.
public inline virtual ExceptionTypes type | Ottiene il tipo di eccezione.
public inline virtual int error | Ottiene il codice di errore.
## <a name="members"></a>Membri
### <a name="rmspfileexception"></a>RMSPFileException
Costruttore [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception).
#### <a name="parameters"></a>Parametri
* message Messaggio di eccezione 
* reason Classificazione dell'errore PFile
### <a name="rmspfileexception"></a>RMSPFileException
Costruttore [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception).
#### <a name="parameters"></a>Parametri
* message Messaggio di eccezione 
* reason Classificazione dell'errore PFile
### <a name="reason"></a>Motivo
Ottiene la classificazione dell'errore PFile.
#### <a name="returns"></a>Returns
Classificazione dell'errore PFile
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