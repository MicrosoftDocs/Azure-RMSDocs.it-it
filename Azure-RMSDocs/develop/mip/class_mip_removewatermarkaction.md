# <a name="class-mipremovewatermarkaction"></a>Classe mip::RemoveWatermarkAction 
Classe di azione che specifica la rimozione della filigrana dal documento.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementnames"></a>GetUIElementNames
Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.

  
**Restituisce**: un elenco di nomi di elementi dell'interfaccia utente.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.