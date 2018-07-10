# <a name="class-mippolicyengine"></a>Classe mip::PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene [Settings](class_mip_policyengine_settings.md) del motore dei criteri.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Elenca le etichette di riservatezza associate al motore dei criteri.
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state) const  |  Ottiene l'etichetta di riservatezza dal contenuto esistente.
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  Ottiene l'etichetta di riservatezza predefinita.
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  Esegue le regole nel motore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene [Settings](class_mip_policyengine_settings.md) del motore dei criteri.

  
**Restituisce**: impostazioni del motore dei criteri. 
  
**Vedere anche**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Label
Elenca le etichette di riservatezza associate al motore dei criteri.

  
**Restituisce**: elenco di etichette di riservatezza.
  
### <a name="contentlabel"></a>ContentLabel
Ottiene l'etichetta di riservatezza dal contenuto esistente.
Le informazioni necessarie per recuperare l'etichetta verranno ottenute usando lo stato di esecuzione specificato. 

Parametri:  
* **state**: 



  
**Restituisce**: oggetto etichetta di contenuto che contiene l'etichetta di riservatezza e informazioni aggiuntive. Se non esiste, restituisce un valore vuoto. 
  
**Vedere anche**: [mip::ContentLabel](class_mip_contentlabel.md).
  
### <a name="label"></a>Label
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: etichetta di riservatezza predefinita se esistente, nullptr se non è impostata un'etichetta predefinita.
  
### <a name="action"></a>Azione
Esegue le regole nel motore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 



  
**Restituisce**: elenco di azioni da applicare al contenuto.