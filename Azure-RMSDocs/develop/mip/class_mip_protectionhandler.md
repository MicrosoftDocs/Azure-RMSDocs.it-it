# <a name="class-mipprotectionhandler"></a>Classe mip::ProtectionHandler 
Esegue azioni correlate alla protezione per una configurazione di protezione specifica (ad esempio, utenti, diritti, ruoli e così via)
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, uint64_t contentStartPosition, uint64_t contentSize)  |  Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Crittografa un buffer.
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Decrittografa un buffer.
 public uint64_t GetProtectedContentLength(uint64_t size)  |  Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).
 public uint64_t GetBlockSize()  |  Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).
 public bool AccessCheck(const std::string& right) const  |  Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.
 public const std::string GetIssuedTo()  |  Ottiene l'utente associato al gestore di protezione.
 public const std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
 public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è il proprietario del contenuto.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  Ottiene i dettagli della protezione.
 public const std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
 public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il gestore di protezione usa algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.
 public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il gestore di protezione concede all'utente il diritto "audited extract".
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione
  
## <a name="members"></a>Membri
  
### <a name="stream"></a>Flusso
Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.

Parametri:  
* **backingStream**: flusso sottostante da cui leggere/scrivere 


* **contentStartPosition**: posizione di inizio (in byte) all'interno del flusso sottostante dove inizia il contenuto protetto 


* **contentSize**: dimensione (in byte) del contenuto protetto all'interno del flusso sottostante



  
**Restituisce**: flusso protetto
  
### <a name="encryptbuffer"></a>EncryptBuffer
Crittografa un buffer.

Parametri:  
* **offsetFromStart**: posizione relativa di inputBuffer dall'inizio del contenuto di testo non crittografato 


* **inputBuffer**: buffer di contenuto di testo non crittografato che verrà crittografato 


* **inputBufferSize**: dimensione (in byte) del buffer di input 


* **outputBuffer**: buffer in cui verrà copiato il contenuto crittografato 


* **outputBufferSize**: dimensione (in byte) del buffer di output 


* **isFinal**: ottiene un valore indicante se il buffer di input contiene o meno i byte di testo non crittografato finali



  
**Restituisce**: dimensione effettiva (in byte) del contenuto crittografato
  
### <a name="decryptbuffer"></a>DecryptBuffer
Decrittografa un buffer.

Parametri:  
* **offsetFromStart**: posizione relativa di inputBuffer dall'inizio del contenuto crittografato 


* **inputBuffer**: buffer di contenuto crittografato che verrà decrittografato 


* **inputBufferSize**: dimensione (in byte) del buffer di input 


* **outputBuffer**: buffer in cui verrà copiato il contenuto decrittografato 


* **outputBufferSize**: dimensione (in byte) del buffer di output 


* **isFinal**: ottiene un valore indicante se il buffer di input contiene o meno i byte crittografati finali



  
**Restituisce**: dimensione effettiva (in byte) del contenuto decrittografato
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).

Parametri:  
* **contentLength**: dimensione (in byte) del contenuto non protetto



  
**Restituisce**: dimensione (in byte) del contenuto protetto
  
### <a name="getblocksize"></a>GetBlockSize
Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: dimensione del blocco (in byte)
  
### <a name="accesscheck"></a>AccessCheck
Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.

Parametri:  
* **right**: diritto da controllare



  
**Restituisce**: valore indicante se il gestore di protezione concede l'accesso utente al diritto specificato
  
### <a name="getissuedto"></a>GetIssuedTo
Ottiene l'utente associato al gestore di protezione.

  
**Restituisce**: utente associato al gestore di protezione
  
### <a name="getowner"></a>GetOwner
Ottiene indirizzo e-mail del proprietario del contenuto.

  
**Restituisce**: indirizzo di posta elettronica del proprietario del contenuto
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Ottiene un valore che indica se l'utente corrente è il proprietario del contenuto.

  
**Restituisce**: valore che indica se l'utente corrente è il proprietario del contenuto
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Ottiene i dettagli della protezione.

  
**Restituisce**: dettagli della protezione
  
### <a name="getcontentid"></a>GetContentId
Ottiene l'identificatore univoco del documento/contenuto.

  
**Restituisce**: identificatore univoco del contenuto
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Ottiene un valore che indica se il gestore di protezione usa algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.

  
**Restituisce**: valore che indica se il gestore di protezione usa algoritmi di crittografia deprecati
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Ottiene un valore che indica se il gestore di protezione concede all'utente il diritto "audited extract".

  
**Restituisce**: valore che indica se il gestore di protezione concede all'utente il diritto "audited extract"
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione

  
**Restituisce**: licenza di pubblicazione serializzata