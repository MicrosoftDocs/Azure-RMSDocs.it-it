# <a name="class-mipremovecontentheaderaction"></a>Classe mip::RemoveContentHeaderAction 
Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector< std::string > & GetUIElementNames | Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
public ActionType GetType
## <a name="members"></a>Membri
### <a name="getuielementnames"></a>GetUIElementNames
Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
#### <a name="returns"></a>Returns
Un elenco di nomi di elementi dell'interfaccia utente.
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](#classmip_1_1_action).
#### <a name="returns"></a>Returns
ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.