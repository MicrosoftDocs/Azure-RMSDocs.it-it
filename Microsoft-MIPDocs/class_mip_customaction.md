# <a name="class-mipcustomaction"></a>Classe mip::CustomAction 
[CustomAction](#classmip_1_1_custom_action) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector< std::pair< std::string, std::string > > & GetProperties | Ottiene l'elenco di coppie valore-chiave delle proprietà.
public ActionType GetType
## <a name="members"></a>Membri
### <a name="getproperties"></a>GetProperties
Ottiene l'elenco di coppie valore-chiave delle proprietà.
#### <a name="returns"></a>Returns
Elenco di coppie valore-chiave.
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](#classmip_1_1_action).
#### <a name="returns"></a>Returns
ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.