# <a name="class-miploggerdelegate"></a>Classe mip::LoggerDelegate 
Classe che definisce l'interfaccia per il logger MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath)  |  Inizializza il logger.
 public void Flush()  |  Scarica il logger.
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const uint64_t line)  |  Scrive un'istruzione log in file di log.
  
## <a name="members"></a>Membri
  
### <a name="init"></a>Init
Inizializza il logger.

Parametri:  
* **storagePath**: percorso della posizione in cui è possibile archiviare lo stato persistente, inclusi i log.


  
### <a name="flush"></a>Svuotamento
Scarica il logger.
  
### <a name="writetolog"></a>WriteToLog
Scrive un'istruzione log in file di log.

Parametri:  
* **level**: loglevel per l'istruzione log. 


* **message**: messaggio per l'istruzione log. 


* **function**: nome della funzione per l'istruzione log. 


* **file**: nome file in cui è stata generata l'istruzione log. 


* **line**: numero di riga in cui è stata generata l'istruzione log.

