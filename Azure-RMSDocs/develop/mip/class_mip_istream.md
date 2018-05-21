# <a name="class-mipistream"></a>Classe mip::IStream 
Interfaccia di base per i flussi protetti.
Convertita da Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream e Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream. [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::shared_future<int64_t> ReadAsync(uint8_t* pbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  Legge un blocco di dati dal flusso in modo asincrono.
public std::shared_future<int64_t> WriteAsync(const uint8_t* cpbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  Scrive un blocco di dati nel flusso in modo asincrono.
public std::future<bool> FlushAsync(std::launch launchType)  |  Scarica il buffer del flusso di output in modo asincrono.
 public int64_t Read(uint8_t* pbBuffer, int64_t cbBuffer)  |  Legge un blocco di dati dal flusso in modo sincrono.
 public int64_t Write(const uint8_t* cpbBuffer, int64_t cbBuffer)  |  Scrive un blocco di dati nel flusso in modo sincrono.
 public bool Flush()  |  Scarica il buffer del flusso di output in modo sincrono.
 public SharedStream Clone()  |  Clona il flusso.
 public void Seek(uint64_t u64Position)  |  Cerca una posizione all'interno del flusso.
 public bool CanRead() const  |  Ottiene un valore che indica se il flusso può essere letto.
 public bool CanWrite() const  |  Ottiene un valore che indica se il flusso può essere scritto.
 public uint64_t Position()  |  Ottiene la posizione corrente del flusso dall'inizio (in byte)
 public uint64_t Size()  |  Ottiene le dimensioni del flusso (in byte)
 public void Size(uint64_t u64Value)  |  Imposta le dimensioni del flusso (in byte)
public virtual std::vector<uint8_t> Read(uint64_t u64size)  |  Legge un blocco di dati dal flusso in modo sincrono.
  
## <a name="members"></a>Membri
  
### <a name="readasync"></a>ReadAsync
Legge un blocco di dati dal flusso in modo asincrono.

Parametri:  
* **pbBuffer**: buffer in cui deve essere letto il flusso 


* **cbBuffer**: dimensioni del buffer 


* **cbOffset**: offset dall'inizio del flusso di input in cui deve iniziare la lettura 


* **launchType**: tipo di avvio asincrono



  
**Restituisce**: oggetto future asincrono che contiene il numero effettivo di byte letti. Assicurarsi che il buffer esista finché il risultato non viene recuperato da std:: future
  
### <a name="writeasync"></a>WriteAsync
Scrive un blocco di dati nel flusso in modo asincrono.

Parametri:  
* **cpbBuffer**: buffer di dati da scrivere 


* **cbBuffer**: dimensioni del buffer 


* **cbOffset**: offset dall'inizio del flusso di output in cui deve iniziare la scrittura 


* **launchType**: tipo di avvio asincrono



  
**Restituisce**: oggetto future asincrono che contiene il numero effettivo di byte scritti. Assicurarsi che il buffer esista finché il risultato non viene recuperato da std:: future
  
### <a name="flushasync"></a>FlushAsync
Scarica il buffer del flusso di output in modo asincrono.

Parametri:  
* **launchType**: tipo di avvio asincrono



  
**Restituisce**: oggetto future asincrono contenente un valore che indica se lo scaricamento ha avuto esito positivo
  
### <a name="read"></a>Lettura
Legge un blocco di dati dal flusso in modo sincrono.

Parametri:  
* **pbBuffer**: buffer in cui deve essere letto il flusso 


* **cbBuffer**: dimensioni del buffer



  
**Restituisce**: numero effettivo di byte letti
  
### <a name="write"></a>Monitoraggio
Scrive un blocco di dati nel flusso in modo sincrono.

Parametri:  
* **cpbBuffer**: buffer di dati da scrivere 


* **cbBuffer**: dimensioni del buffer



  
**Restituisce**: numero effettivo di byte scritti
  
### <a name="flush"></a>Svuotamento
Scarica il buffer del flusso di output in modo sincrono.

  
**Restituisce**: valore che indica se lo scaricamento ha avuto esito positivo
  
### <a name="sharedstream"></a>SharedStream
Clona il flusso.

  
**Restituisce**: flusso clonato
  
### <a name="seek"></a>Seek
Cerca una posizione all'interno del flusso.

Parametri:  
* **u64Position**: offset di byte dall'inizio del flusso


  
### <a name="canread"></a>CanRead
Ottiene un valore che indica se il flusso può essere letto.

  
**Restituisce**: valore che indica se il flusso può essere letto
  
### <a name="canwrite"></a>CanWrite
Ottiene un valore che indica se il flusso può essere scritto.

  
**Restituisce**: valore che indica se il flusso può essere scritto
  
### <a name="position"></a>Posizione
Ottiene la posizione corrente del flusso dall'inizio (in byte)

  
**Restituisce**: posizione corrente del flusso dall'inizio (in byte)
  
### <a name="size"></a>Dimensioni
Ottiene le dimensioni del flusso (in byte)

  
**Restituisce**: dimensioni del flusso (in byte)
  
### <a name="size"></a>Dimensioni
Imposta le dimensioni del flusso (in byte)

Parametri:  
* **u64Value**: dimensioni del flusso (in byte)


  
### <a name="read"></a>Lettura
Legge un blocco di dati dal flusso in modo sincrono.

Parametri:  
* **u64size**: dimensioni dei dati da leggere (in byte)



  
**Restituisce**: vettore dei dati effettivamente letti