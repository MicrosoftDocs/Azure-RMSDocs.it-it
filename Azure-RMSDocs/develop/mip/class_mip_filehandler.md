# <a name="class-mipfilehandler"></a>Classe mip::FileHandler 
Interfaccia per tutte le funzioni di gestione file.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void GetLabelAsync | Avvia il recupero dell'etichetta di riservatezza dal file.
public void GetProtectionAsync | Avvia il recupero dei criteri di protezione dal file.
public void SetLabelLabelingOptions & labelingOptions) | Imposta l'etichetta di riservatezza per il file.
public void DeleteLabel | Elimina l'etichetta di riservatezza dal file.
public void SetCustomPermissionsPolicyDescriptor > & policyDescriptor) | Imposta autorizzazioni personalizzate per il file.
public void RemoveProtection | Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
public void CommitAsync | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\|.
public void CommitAsyncStream > & outputStream,const std::shared_ptr< void > & context) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\|.
public std::string GetOutputFileName | Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
public inline virtual  ~FileHandler | 
protected inline  FileHandler | 
## <a name="members"></a>Membri
### <a name="getlabelasync"></a>GetLabelAsync
Avvia il recupero dell'etichetta di riservatezza dal file.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
#### <a name="parameters"></a>Parametri
* context Contesto client che verrà passato in maniera opaca all'observer.
### <a name="getprotectionasync"></a>GetProtectionAsync
Avvia il recupero dei criteri di protezione dal file.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
#### <a name="parameters"></a>Parametri
* context Contesto client che verrà passato in maniera opaca all'observer.
### <a name="setlabel"></a>SetLabel
Imposta l'etichetta di riservatezza per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
Genera [JustificationRequiredError](#classmip_1_1_justification_required_error) quando l'impostazione dell'etichetta richiede una giustificazione e tramite il parametro labelingOptions non è stato fornito alcun messaggio di giustificazione.
### <a name="deletelabel"></a>DeleteLabel
Elimina l'etichetta di riservatezza dal file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente Genera [JustificationRequiredError](#classmip_1_1_justification_required_error) quando l'impostazione dell'etichetta richiede una giustificazione e tramite il parametro justificationMessage non è stato fornito alcun messaggio di giustificazione.
### <a name="setcustompermissions"></a>SetCustomPermissions
Imposta autorizzazioni personalizzate per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
### <a name="removeprotection"></a>RemoveProtection
Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
### <a name="commitasync"></a>CommitAsync
Scrive le modifiche nel file specificato dal parametro |outputFilePath|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
### <a name="commitasync"></a>CommitAsync
Scrive le modifiche nel flusso specificato dal parametro |outputStream|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
### <a name="getoutputfilename"></a>GetOutputFileName
Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
### <a name="filehandler"></a>~FileHandler
### <a name="filehandler"></a>FileHandler