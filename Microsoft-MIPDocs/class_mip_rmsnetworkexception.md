# <a name="class-miprmsnetworkexception"></a>Classe mip::RMSNetworkException 
Eccezione di rete di RMS.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  RMSNetworkExceptionReason reason) public inline  RMSNetworkExceptionReason reason) public inline virtual Reason reason | Ottiene la classificazione di un errore di rete.
public inline virtual const char * what | Ottiene il messaggio di eccezione.
public inline virtual ExceptionTypes type | Ottiene il tipo di eccezione.
public inline virtual int error | Ottiene il codice di errore.
## <a name="members"></a>Membri
### <a name="rmsnetworkexception"></a>RMSNetworkException
Costruttore [RMSNetworkException](#classmip_1_1_r_m_s_network_exception).
#### <a name="parameters"></a>Parametri
* message Messaggio di eccezione 
* reason Classificazione dell'errore di rete
### <a name="rmsnetworkexception"></a>RMSNetworkException
Costruttore [RMSNetworkException](#classmip_1_1_r_m_s_network_exception).
#### <a name="parameters"></a>Parametri
* message Messaggio di eccezione 
* reason Classificazione dell'errore di rete
### <a name="reason"></a>Motivo
Ottiene la classificazione dell'errore di rete.
#### <a name="returns"></a>Returns
Classificazione dell'errore di rete
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