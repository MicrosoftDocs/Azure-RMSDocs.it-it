# <a name="functions"></a>Funzioni

 Funzioni (ambito)                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.
public const std::string& GetCustomSettingPolicyDataName()       |  Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.
**Funzioni mip** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  Crea un [flusso](class_mip_stream.md) da un buffer.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  Crea un [flusso](class_mip_stream.md) da std::iostream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  Crea un [flusso](class_mip_stream.md) da std::istream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  Crea un [flusso](class_mip_stream.md) da std::ostream.
**Funzioni mip::Rights**|
public std::string AuditedExtract()       |  Ottiene l'identificatore della stringa per il diritto "audited extract".
public std::string Comment()       |  Ottiene l'identificatore della stringa per il diritto "comment".
public std::vector<std::string> CommonRights()       |  Ottiene un elenco di diritti che si applicano in tutti gli scenari.
public std::string Edit()       |  Ottiene l'identificatore della stringa per il diritto "edit".
public std::vector<std::string> EditableDocumentRights()       |  Ottiene un elenco di diritti che si applicano ai documenti.
public std::vector<std::string> EmailRights()       |  Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.
public std::string Export()       |  Ottiene l'identificatore della stringa per il diritto "export".
public std::string Extract()       |  Ottiene l'identificatore della stringa per il diritto "extract".
public std::string Forward()       |  Ottiene l'identificatore della stringa per il diritto "forward".
public std::string Owner()       |  Ottiene l'identificatore della stringa per il diritto "owner".
public std::string Print()       |  Ottiene l'identificatore della stringa per il diritto "print".
public std::string Reply()       |  Ottiene l'identificatore della stringa per il diritto "reply".
public std::string ReplyAll()       |  Ottiene l'identificatore della stringa per il diritto "reply all".
public std::string View()       |  Ottiene l'identificatore della stringa per il diritto "view".
**Funzioni mip::Roles**|
public std::string Author()       |  Ottiene l'identificatore della stringa per il ruolo "author".
public std::string CoOwner()       |  Ottiene l'identificatore della stringa per il ruolo "co-owner".
public std::string Reviewer()       |  Ottiene l'identificatore della stringa per il ruolo "reviewer".
public std::string Viewer()       |  Ottiene l'identificatore della stringa per il ruolo "viewer".

  
## <a name="enumeration-details"></a>Dettagli dell'enumerazione
  
## <a name="functions-common"></a>Funzioni (comuni)

### <a name="getcustomsettingpolicydataname"></a>GetCustomSettingPolicyDataName
Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingexportpolicyfilename"></a>GetCustomSettingExportPolicyFileName
Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingpolicydatafile"></a>GetCustomSettingPolicyDataFile
Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.

  
**Restituisce**: chiave delle impostazioni personalizzate.

## <a name="functions-mip"></a>Funzioni (mip)

### <a name="mipstream-istream"></a>mip::Stream (istream)

Crea un [flusso](class_mip_stream.md) da std::istream.

Parametri:  

* **stdIStream**: std::istream sottostante
  
**Restituisce**: [flusso](class_mip_stream.md) che esegue il wrapping di std::istream
  
### <a name="mipstream-ostream"></a>mip::Stream (ostream)

Crea un [flusso](class_mip_stream.md) da std::ostream.

Parametri:  
* **stdOStream**: std::ostream sottostante

  
**Restituisce**: [flusso](class_mip_stream.md) che esegue il wrapping di std::ostream
  
### <a name="mipstream-iostream"></a>mip::Stream (iostream)

Crea un [flusso](class_mip_stream.md) da std::iostream.

Parametri:  
* **stdIOStream**: std::iostream sottostante
  
**Restituisce**: [flusso](class_mip_stream.md) che esegue il wrapping di std::iostream
  
### <a name="mipstream-buffer"></a>mip::Stream (buffer)

Crea un [flusso](class_mip_stream.md) da un buffer.

Parametri:  
* **buffer**: puntatore a un buffer

**Restituisce**: dimensioni del buffer
  
## <a name="functions-miprights"></a>Funzioni (mip::rights)

### <a name="auditedextract"></a>AuditedExtract
Ottiene l'identificatore della stringa per il diritto "audited extract".

  
**Restituisce**: identificatore della stringa per il diritto "audited extract"
  
### <a name="comment"></a>Commento
Ottiene l'identificatore della stringa per il diritto "comment".

  
**Restituisce**: identificatore della stringa per il diritto "comment"
  
### <a name="commonrights"></a>CommonRights
Ottiene un elenco di diritti che si applicano in tutti gli scenari.

  
**Restituisce**: elenco di diritti che si applicano in tutti gli scenari

### <a name="edit"></a>Modifica
Ottiene l'identificatore della stringa per il diritto "edit".

  
**Restituisce**: identificatore della stringa per il diritto "edit"
  
### <a name="editabledocumentrights"></a>EditableDocumentRights
Ottiene un elenco di diritti che si applicano ai documenti.

  
**Restituisce**: elenco di diritti che si applicano ai documenti
  
### <a name="emailrights"></a>EmailRights
Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.

  
**Restituisce**: elenco di diritti che si applicano ai messaggi di posta elettronica
  
### <a name="export"></a>Export
Ottiene l'identificatore della stringa per il diritto "export".

  
**Restituisce**: identificatore della stringa per il diritto "export"
  
### <a name="extract"></a>Estrai
Ottiene l'identificatore della stringa per il diritto "extract".

  
**Restituisce**: identificatore della stringa per il diritto "extract"
  

### <a name="forward"></a>Inoltra
Ottiene l'identificatore della stringa per il diritto "forward".

  
**Restituisce**: identificatore della stringa per il diritto "forward"
  
### <a name="owner"></a>Proprietario
Ottiene l'identificatore della stringa per il diritto "owner".

  
**Restituisce**: identificatore della stringa per il diritto "owner"
  
### <a name="print"></a>Stampa
Ottiene l'identificatore della stringa per il diritto "print".

  
**Restituisce**: identificatore della stringa per il diritto "print"
  
### <a name="reply"></a>Rispondi
Ottiene l'identificatore della stringa per il diritto "reply".

  
**Restituisce**: identificatore della stringa per il diritto "reply"
  
### <a name="replyall"></a>Rispondi a tutti
Ottiene l'identificatore della stringa per il diritto "reply all".

  
**Restituisce**: identificatore della stringa per il diritto "reply all"
  
### <a name="view"></a>Visualizza
Ottiene l'identificatore della stringa per il diritto "view".

  
**Restituisce**: identificatore della stringa per il diritto "view"
  
## <a name="functions-miproles"></a>Funzioni (mip::roles)

### <a name="author"></a>Autore
Ottiene l'identificatore della stringa per il ruolo "author".

  
**Restituisce**: identificatore della stringa per il ruolo "author". Un autore può visualizzare, modificare, copiare e stampare il contenuto.
  
### <a name="coowner"></a>CoOwner
Ottiene l'identificatore della stringa per il ruolo "co-owner".

  
**Restituisce**: identificatore della stringa per il ruolo "co-owner". Un comproprietario ha tutte le autorizzazioni

### <a name="reviewer"></a>Revisore
Ottiene l'identificatore della stringa per il ruolo "reviewer".

  
**Restituisce**: identificatore della stringa per il ruolo "reviewer". Un revisore può visualizzare e modificare il contenuto. Non può copiarlo o stamparlo.

### <a name="viewer"></a>Visualizzatore
Ottiene l'identificatore della stringa per il ruolo "viewer".

  
**Restituisce**: identificatore della stringa per il ruolo "viewer". Un visualizzatore può solo visualizzare il contenuto. Non può modificarlo, copiarlo o stamparlo.
  
  
