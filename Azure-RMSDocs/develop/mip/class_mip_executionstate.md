# <a name="class-mipexecutionstate"></a>Classe mip::ExecutionState 
Interfaccia per tutti gli stati necessari per eseguire il motore.
I client dovrebbero chiamare i metodi solo per ottenere lo stato necessario. Di conseguenza, per motivi di efficienza, è consigliabile che i client implementino questa interfaccia in modo che lo stato corrispondente sia calcolato in modo dinamico anziché in anticipo.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId | Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public bool IsDowngradeJustified | L'implementazione dovrebbe restituire un valore che indica se è stata fornita o meno una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod | Ottiene il metodo di assegnazione della nuova etichetta.
public std::vector< std::pair< std::string, std::string > > GetContentMetadata | Ottiene gli elementi dei metadati dal contenuto.
public std::string GetTemplateId | Ottiene l'ID del modello di protezione del servizio Rights Management.
public ContentFormat GetContentFormat | Ottiene il formato del contenuto.
public const ActionType GetSupportedActions
## <a name="members"></a>Membri
### <a name="getnewlabelid"></a>GetNewLabelId
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
#### <a name="returns"></a>Returns
ID dell'etichetta di riservatezza da applicare al contenuto se esistente, in caso contrario una stringa vuota per rimuovere l'etichetta.
### <a name="isdowngradejustified"></a>IsDowngradeJustified
L'implementazione dovrebbe restituire un valore che indica se è stata fornita o meno una giustificazione per effettuare il downgrade di un'etichetta esistente.
#### <a name="returns"></a>Returns
True se il downgrade è già giustificato, false se non è ancora stato giustificato. 
**Vedere anche**: [mip::JustifyAction](#classmip_1_1_justify_action)
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Ottiene il metodo di assegnazione della nuova etichetta.
#### <a name="returns"></a>Returns
Metodo di assegnazione STANDARD, PRIVILEGED, AUTO. 
**Vedere anche**: mip::AssignmentMethod
### <a name="getcontentmetadata"></a>GetContentMetadata
Ottiene gli elementi dei metadati dal contenuto.
#### <a name="returns"></a>Returns
Vettore di coppie chiave-valore che rappresenta i metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
### <a name="gettemplateid"></a>GetTemplateId
Ottiene l'ID del modello di protezione del servizio Rights Management.
#### <a name="returns"></a>Returns
ID del modello di protezione del servizio Rights Management se esistente in formato GUID senza parentesi graffe, in caso contrario restituisce una stringa vuota.
### <a name="getcontentformat"></a>GetContentFormat
Ottiene il formato del contenuto.
#### <a name="returns"></a>Returns
DEFAULT, EMAIL **Vedere anche**: mip::ContentFormat
### <a name="actiontype"></a>ActionType
Restituisce un elenco di azioni supportate dall'applicazione. Tutti i tipi di azioni sono elencati in [mip/upe/action.h](#action_8h).