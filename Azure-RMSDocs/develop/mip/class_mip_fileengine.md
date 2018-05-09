# <a name="class-mipfileengine"></a>Classe mip::FileEngine 
Interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline virtual ~FileEngine()  |  
public const Settings& GetSettings() const  |  Restituisce le impostazioni del motore.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Restituisce un elenco di etichette di riservatezza.
public std::shared_ptr<FileHandler> CreateFileHandler(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  Restituisce il gestore di file per un determinato percorso file.
public std::shared_ptr<FileHandler> CreateFileHandler(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  Restituisce il gestore di file per un determinato flusso di file.
protected inline FileEngine()  |  
  
## <a name="members"></a>Membri
  
### <a name="fileengine"></a>~FileEngine
  
### <a name="settings"></a>Impostazioni
Restituisce le impostazioni del motore.
  
### <a name="label"></a>Label
Restituisce un elenco di etichette di riservatezza.
  
### <a name="filehandler"></a>FileHandler
Restituisce il gestore di file per un determinato percorso file.
  
#### <a name="parameters"></a>Parametri
* File da aprire. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 
* Classe che implementa l'interfaccia [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
  
### <a name="filehandler"></a>FileHandler
Restituisce il gestore di file per un determinato flusso di file.
  
#### <a name="parameters"></a>Parametri
* Flusso che rappresenta il file. 
* Percorso del file. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 
* Classe che implementa l'interfaccia [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
  
### <a name="fileengine"></a>FileEngine