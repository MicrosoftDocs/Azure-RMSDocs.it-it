# <a name="class-mipstream"></a>Classe mip::Stream 
Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Legge in un buffer dal flusso.
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Scrive nel flusso da un buffer.
public bool Flush()  |  Scarica il flusso.
public void Seek(uint64_t position)  |  Cerca una posizione all'interno del flusso.
public bool CanRead() const  |  Verifica se il flusso è leggibile.
public bool CanWrite() const  |  Verifica se il flusso è scrivibile.
public uint64_t Position()  |  Ottiene la posizione corrente all'interno del flusso.
public uint64_t Size()  |  Ottiene le dimensioni del contenuto all'interno del flusso.
public void Size(uint64_t value)  |  Imposta le dimensioni del flusso.
public std::shared_ptr<Stream> Clone()  |  Clona il flusso.
  
## <a name="members"></a>Membri
  
### <a name="read"></a>Lettura
Legge in un buffer dal flusso.
  
#### <a name="parameters"></a>Parametri
* buffer Puntatore a un buffer 
* bufferLength Dimensioni del buffer. 
  
#### <a name="returns"></a>Returns
Numero di byte effettivamente letti.
  
### <a name="write"></a>Monitoraggio
Scrive nel flusso da un buffer.
  
#### <a name="parameters"></a>Parametri
* buffer Puntatore a un buffer 
* bufferLength Dimensioni del buffer. 
  
#### <a name="returns"></a>Returns
Numero di byte effettivamente letti.
  
### <a name="flush"></a>Svuotamento
Scarica il flusso.
  
#### <a name="returns"></a>Returns
True se l'operazione ha esito positivo, in caso contrario false.
  
### <a name="seek"></a>Seek
Cerca una posizione all'interno del flusso.
  
#### <a name="parameters"></a>Parametri
* Posizione da cercare nel flusso.
  
### <a name="canread"></a>CanRead
Verifica se il flusso è leggibile.
  
#### <a name="returns"></a>Returns
True se è leggibile, in caso contrario false.
  
### <a name="canwrite"></a>CanWrite
Verifica se il flusso è scrivibile.
  
#### <a name="returns"></a>Returns
True se è scrivibile, in caso contrario false.
  
### <a name="position"></a>Posizione
Ottiene la posizione corrente all'interno del flusso.
  
#### <a name="returns"></a>Returns
Posizione all'interno del flusso.
  
### <a name="size"></a>Dimensioni
Ottiene le dimensioni del contenuto all'interno del flusso.
  
#### <a name="returns"></a>Returns
Dimensioni del flusso.
  
### <a name="size"></a>Dimensioni
Imposta le dimensioni del flusso.
  
#### <a name="parameters"></a>Parametri
* Dimensioni del flusso.
  
### <a name="stream"></a>Flusso
Clona il flusso.
  
#### <a name="returns"></a>Returns
Nuovo flusso.