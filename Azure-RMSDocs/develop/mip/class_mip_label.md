# <a name="class-miplabel"></a>Classe mip::Label 
Astrazione per una singola etichetta di Microsoft Information Protection.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID dell'etichetta.
public const std::string& GetName() const  |  Ottiene il nome dell'etichetta.
public const std::string& GetDescription() const  |  Ottiene la descrizione dell'etichetta.
public const std::string& GetColor() const  |  Ottiene il colore in cui deve essere visualizzata l'etichetta.
public const std::string& GetOrder() const  |  Ottiene l'ordine dell'etichetta.
public const std::string& GetTooltip() const  |  Ottiene la descrizione comando dell'etichetta.
public bool IsActive() const  |  Ottiene un valore booleano che indica se l'etichetta è attiva.
public std::weak_ptr<Label> GetParent() const  |  Ottiene l'etichetta padre.
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  Ottiene le etichette figlio dell'etichetta corrente.
  
## <a name="members"></a>Membri
  
### <a name="getid"></a>GetId
Ottiene l'ID dell'etichetta.
  
#### <a name="returns"></a>Returns
ID dell'etichetta.
  
### <a name="getname"></a>GetName
Ottiene il nome dell'etichetta.
  
#### <a name="returns"></a>Returns
Nome dell'etichetta.
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione dell'etichetta.
  
#### <a name="returns"></a>Returns
Descrizione dell'etichetta.
  
### <a name="getcolor"></a>GetColor
Ottiene il colore in cui deve essere visualizzata l'etichetta.
  
#### <a name="returns"></a>Returns
Valore del colore in formato stringa. "#RRGGBB", dove RR, GG, BB sono valori esadecimali di due cifre compresi nell'intervallo 0-F.
  
### <a name="getorder"></a>GetOrder
Ottiene l'ordine dell'etichetta.
  
#### <a name="returns"></a>Returns
Valore numerico in formato stringa.
  
### <a name="gettooltip"></a>GetTooltip
Ottiene la descrizione comando dell'etichetta.
  
#### <a name="returns"></a>Returns
Stringa di descrizione comando.
  
### <a name="isactive"></a>IsActive
Ottiene un valore booleano che indica se l'etichetta è attiva.
Possono essere applicate solo le etichette attive. Le etichette inattive non possono essere applicate e sono usate solo a scopo di visualizzazione. 
  
#### <a name="returns"></a>Returns
True se l'etichetta è attiva, in caso contrario false.
  
### <a name="label"></a>Label
Ottiene l'etichetta padre.
  
#### <a name="returns"></a>Returns
Puntatore debole all'etichetta padre se esistente, in caso contrario un puntatore vuoto.
  
### <a name="label"></a>Label
Ottiene le etichette figlio dell'etichetta corrente.
  
#### <a name="returns"></a>Returns
Vettore di puntatori condivisi a etichette.