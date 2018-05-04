# <a name="class-mipistream"></a>Classe mip::IStream 
Interfaccia di base per i flussi protetti.
Convertita da Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream e Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream. [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::shared_future< int64_t > ReadAsync | Legge un blocco di dati dal flusso in modo asincrono.
public std::shared_future< int64_t > WriteAsync | Scrive un blocco di dati nel flusso in modo asincrono.
public std::future< bool > FlushAsync | Scarica il buffer del flusso di output in modo asincrono.
public int64_t Read | Legge un blocco di dati dal flusso in modo sincrono.
public int64_t Write | Scrive un blocco di dati nel flusso in modo sincrono.
public bool Flush | Scarica il buffer del flusso di output in modo sincrono.
public SharedStream Clone | Clona il flusso.
public void Seek | Cerca una posizione all'interno del flusso.
public bool CanRead | Ottiene un valore che indica se il flusso può essere letto.
public bool CanWrite | Ottiene un valore che indica se il flusso può essere scritto.
public uint64_t Position | Ottiene la posizione corrente del flusso dall'inizio (in byte)
public uint64_t Size | Ottiene le dimensioni del flusso (in byte)
public void Size | Imposta le dimensioni del flusso (in byte)
public inline virtual std::vector< uint8_t > Read | Legge un blocco di dati dal flusso in modo sincrono.
## <a name="members"></a>Membri
### <a name="readasync"></a>ReadAsync
Legge un blocco di dati dal flusso in modo asincrono.
#### <a name="parameters"></a>Parametri
* pbBuffer Buffer in cui deve essere letto il flusso 
* cbBuffer Dimensioni del buffer 
* cbOffset Offset dall'inizio del flusso di input in cui deve iniziare la lettura 
* launchType Tipo di avvio asincrono
#### <a name="returns"></a>Returns
Oggetto future Async che contiene il numero effettivo di byte letti. Assicurarsi che il buffer esista finché il risultato non viene recuperato da std:: future
### <a name="writeasync"></a>WriteAsync
Scrive un blocco di dati nel flusso in modo asincrono.
#### <a name="parameters"></a>Parametri
* cpbBuffer Buffer di dati da scrivere 
* cbBuffer Dimensioni del buffer 
* cbOffset Offset dall'inizio del flusso di output in cui deve iniziare la scrittura 
* launchType Tipo di avvio asincrono
#### <a name="returns"></a>Returns
Oggetto future Async che contiene il numero effettivo di byte scritti. Assicurarsi che il buffer esista finché il risultato non viene recuperato da std:: future
### <a name="flushasync"></a>FlushAsync
Scarica il buffer del flusso di output in modo asincrono.
#### <a name="parameters"></a>Parametri
* launchType Tipo di avvio asincrono
#### <a name="returns"></a>Returns
Oggetto future Async contenente un valore che indica se lo scaricamento ha avuto esito positivo
### <a name="read"></a>Lettura
Legge un blocco di dati dal flusso in modo sincrono.
#### <a name="parameters"></a>Parametri
* pbBuffer Buffer in cui deve essere letto il flusso 
* cbBuffer Dimensioni del buffer
#### <a name="returns"></a>Returns
Numero effettivo di byte letti
### <a name="write"></a>Monitoraggio
Scrive un blocco di dati nel flusso in modo sincrono.
#### <a name="parameters"></a>Parametri
* cpbBuffer Buffer di dati da scrivere 
* cbBuffer Dimensioni del buffer
#### <a name="returns"></a>Returns
Numero effettivo di byte scritti
### <a name="flush"></a>Svuotamento
Scarica il buffer del flusso di output in modo sincrono.
#### <a name="returns"></a>Returns
Valore che indica se lo scaricamento ha avuto esito positivo
### <a name="sharedstream"></a>SharedStream
Clona il flusso.
#### <a name="returns"></a>Returns
Flusso clonato
### <a name="seek"></a>Seek
Cerca una posizione all'interno del flusso.
#### <a name="parameters"></a>Parametri
* u64Position Offset di byte dall'inizio del flusso
### <a name="canread"></a>CanRead
Ottiene un valore che indica se il flusso può essere letto.
#### <a name="returns"></a>Returns
Valore che indica se il flusso può essere letto
### <a name="canwrite"></a>CanWrite
Ottiene un valore che indica se il flusso può essere scritto.
#### <a name="returns"></a>Returns
Valore che indica se il flusso può essere scritto
### <a name="position"></a>Posizione
Ottiene la posizione corrente del flusso dall'inizio (in byte)
#### <a name="returns"></a>Returns
Posizione corrente del flusso dall'inizio (in byte)
### <a name="size"></a>Dimensioni
Ottiene le dimensioni del flusso (in byte)
#### <a name="returns"></a>Returns
Dimensioni del flusso (in byte)
### <a name="size"></a>Dimensioni
Imposta le dimensioni del flusso (in byte)
#### <a name="parameters"></a>Parametri
* u64Value Dimensioni del flusso (in byte)
### <a name="read"></a>Lettura
Legge un blocco di dati dal flusso in modo sincrono.
#### <a name="parameters"></a>Parametri
* u64size Dimensioni dei dati da leggere (in byte)
#### <a name="returns"></a>Returns
Vettore dei dati effettivamente letti