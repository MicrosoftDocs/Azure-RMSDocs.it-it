# <a name="class-mipmetadataaction"></a>Classe mip::MetadataAction 
Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Ottiene l'elenco dei nomi di metadati da rimuovere dal contenuto.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Ottiene l'elenco dei metadati come coppie chiave-valore. I metadati devono essere aggiunti ai metadati del contenuto.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Ottiene l'elenco dei nomi di metadati da rimuovere dal contenuto.

  
**Restituisce**: vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta di metadati.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Ottiene l'elenco dei metadati come coppie chiave-valore. I metadati devono essere aggiunti ai metadati del contenuto.

  
**Restituisce**: const std::vector<std::pair<std::string, std::string>>& La rimozione dei metadati deve essere eseguita prima dell'aggiunta di metadati.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.