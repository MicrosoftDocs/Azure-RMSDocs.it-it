# <a name="class-mipaddwatermarkaction"></a>Classe mip::AddWatermarkAction 
Classe di azione che specifica l'aggiunta di una filigrana.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento filigrana.
 public WatermarkLayout GetLayout() const  |  API usata per ottenere il layout della filigrana.
 public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nella filigrana.
 public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.
 public int GetFontSize() const  |  Ottiene le dimensioni del carattere usate per visualizzare la filigrana.
 public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare la filigrana.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementname"></a>GetUIElementName
API usata per contrassegnare l'elemento filigrana.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene la filigrana. Lo stesso nome verrà restituito in RemoveWatermarkingAction nel caso in cui la filigrana debba essere rimossa.
  
### <a name="getlayout"></a>GetLayout
API usata per ottenere il layout della filigrana.

  
**Restituisce**: WatermarkLayout Layout della filigrana nel formato di un'enumerazione HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext"></a>GetText
Ottiene il testo destinato a essere inserito nella filigrana.

  
**Restituisce**: testo dell'intestazione contenuto.
  
### <a name="getfontname"></a>GetFontName
Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.

  
**Restituisce**: nome del carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize"></a>GetFontSize
Ottiene le dimensioni del carattere usate per visualizzare la filigrana.

  
**Restituisce**: dimensioni del carattere come numero intero.
  
### <a name="getfontcolor"></a>GetFontColor
Ottiene il colore del carattere usato per visualizzare la filigrana.

  
**Restituisce**: colore del carattere in formato stringa (ad esempio "#000000").
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.