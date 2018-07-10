# <a name="class-mipexecutionstate"></a>Classe mip::ExecutionState 
Interfaccia per tutti gli stati necessari per eseguire il motore.
I client dovrebbero chiamare i metodi solo per ottenere lo stato necessario. Di conseguenza, per motivi di efficienza, è consigliabile che i client implementino questa interfaccia in modo che lo stato corrispondente sia calcolato in modo dinamico anziché in anticipo.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
 public bool IsDowngradeJustified() const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita o meno una giustificazione per effettuare il downgrade di un'etichetta esistente.
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  Restituisce le proprietà estese della nuova etichetta.
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
 public std::string GetTemplateId() const  |  Ottiene l'ID del modello di protezione del servizio Rights Management.
 public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
 public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che rappresenta tutti i tipi di azioni supportati.
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  Restituisce una mappa dei risultati della classificazione.
  
## <a name="members"></a>Membri
  
### <a name="getnewlabelid"></a>GetNewLabelId
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID dell'etichetta di riservatezza da applicare al contenuto se esistente, in caso contrario una stringa vuota per rimuovere l'etichetta.
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
L'implementazione dovrebbe restituire un valore che indica se è stata fornita o meno una giustificazione per effettuare il downgrade di un'etichetta esistente.

  
**Restituisce**: true se il downgrade è già giustificato, false se non è ancora stato giustificato. 
  
**Vedere anche**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Ottiene il metodo di assegnazione della nuova etichetta.

  
**Restituisce**: metodo di assegnazione STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
Restituisce le proprietà estese della nuova etichetta.

  
**Restituisce**: vettore di coppie chiave-valore che rappresentano le proprietà estese applicate al contenuto.
  
### <a name="getcontentmetadata"></a>GetContentMetadata
Ottiene gli elementi dei metadati dal contenuto.

  
**Restituisce**: vettore di coppie chiave-valore che rappresentano i metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
  
### <a name="gettemplateid"></a>GetTemplateId
Ottiene l'ID del modello di protezione del servizio Rights Management.

  
**Restituisce**: ID del modello di protezione del servizio Rights Management se esistente in formato GUID senza parentesi graffe, in caso contrario restituisce una stringa vuota.
  
### <a name="getcontentformat"></a>GetContentFormat
Ottiene il formato del contenuto.

  
**Restituisce**: DEFAULT, EMAIL 
  
**Vedere anche**: mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
Ottiene un'enumerazione mascherata che rappresenta tutti i tipi di azioni supportati.

  
**Restituisce**: enumerazione mascherata che rappresenta tutti i tipi di azioni supportati.
  
### <a name="classificationresult"></a>ClassificationResult
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **classificationId**: elenco di ID classificazione. 



  
**Restituisce**: elenco di risultati della classificazione.