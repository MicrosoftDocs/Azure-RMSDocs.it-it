# <a name="class-mipaddwatermarkaction"></a>Classe mip::AddWatermarkAction 
Classe di azione che specifica l'aggiunta di una filigrana.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento filigrana.
public WatermarkLayout GetLayout() const  |  API usata per ottenere il layout della filigrana.
public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nell'intestazione contenuto.
public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.
public int GetFontSize() const  |  Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.
public const std::string& GetFontColor() const  |  Ottiene il colore carattere usato per visualizzare l'intestazione contenuto.
public ActionType GetType() const  |  Specifica il tipo di [Action](#classmip_1_1_action).
  
## <a name="members"></a>Membri
  
### <a name="getuielementname"></a>GetUIElementName
API usata per contrassegnare l'elemento filigrana.
  
#### <a name="returns"></a>Returns
Nome da usare per l'elemento dell'interfaccia utente che contiene la filigrana. Lo stesso nome verrà restituito in RemoveWatermarkingAction nel caso in cui la filigrana debba essere rimossa.
  
### <a name="getlayout"></a>GetLayout
API usata per ottenere il layout della filigrana.
  
#### <a name="returns"></a>Returns
WatermarkLayout Layout della filigrana nel formato di un'enumerazione HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext"></a>GetText
Ottiene il testo destinato a essere inserito nell'intestazione contenuto.
  
#### <a name="returns"></a>Returns
Testo dell'intestazione contenuto.
  
### <a name="getfontname"></a>GetFontName
Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.
  
#### <a name="returns"></a>Returns
Nome del tipo di carattere, il valore predefinito se non definito da criteri è Calibri.
  
### <a name="getfontsize"></a>GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.
  
#### <a name="returns"></a>Returns
Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor"></a>GetFontColor
Ottiene il colore carattere usato per visualizzare l'intestazione contenuto.
  
#### <a name="returns"></a>Returns
Colore del carattere in formato stringa (ad esempio "#000000").
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](#classmip_1_1_action).
  
#### <a name="returns"></a>Returns
ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.