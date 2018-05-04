# <a name="class-mippolicyengine"></a>Classe mip::PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings & GetSettings public const std::vector< std::shared_ptr< Label > > & ListSensitivityLabels | Elenca le etichette di riservatezza associate al motore dei criteri.
public std::shared_ptr< ContentLabel > GetSensitivityLabelExecutionState & state) | Ottiene l'etichetta di riservatezza dal contenuto esistente.
public std::shared_ptr< Label > GetDefaultSensitivityLabel | Ottiene l'etichetta di riservatezza predefinita.
public std::vector< std::shared_ptr< Action > > ComputeActionsExecutionState & state) | Esegue le regole nel motore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
## <a name="members"></a>Membri
### <a name="settings"></a>Impostazioni
Ottiene [Settings](#classmip_1_1_policy_engine_1_1_settings) del motore dei criteri.
#### <a name="returns"></a>Returns
Impostazioni del motore dei criteri. 
**Vedere anche**: [mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings)
### <a name="label"></a>Label
Elenca le etichette di riservatezza associate al motore dei criteri.
#### <a name="returns"></a>Returns
Elenco di etichette di riservatezza.
### <a name="contentlabel"></a>ContentLabel
Ottiene l'etichetta di riservatezza dal contenuto esistente.
Le informazioni necessarie per recuperare l'etichetta verranno ottenute usando lo stato di esecuzione specificato. 
#### <a name="parameters"></a>Parametri
* state 
#### <a name="returns"></a>Returns
Oggetto etichetta di contenuto che contiene l'etichetta di riservatezza e informazioni aggiuntive. Se non esiste, restituisce un valore vuoto. 
**Vedere anche**: [mip::ContentLabel](#classmip_1_1_content_label).
### <a name="label"></a>Label
Ottiene l'etichetta di riservatezza predefinita.
#### <a name="returns"></a>Returns
Etichetta di riservatezza predefinita se esistente, nullptr se non è impostata un'etichetta predefinita.
### <a name="action"></a>Azione
Esegue le regole nel motore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
#### <a name="parameters"></a>Parametri
* state Stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 
#### <a name="returns"></a>Returns
Elenco di azioni da applicare al contenuto.