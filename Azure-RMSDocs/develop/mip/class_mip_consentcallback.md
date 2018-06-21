# <a name="class-mipconsentcallback"></a>Classe mip::ConsentCallback 
Interfaccia per le notifiche di richiesta di consenso.
Questo callback viene implementato da un'applicazione client per sapere quando è necessario mostrare all'utente una notifica di consenso.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public ConsentList Consents(ConsentList& consents)  |  Viene chiamato quando l'SDK richiede il consenso dell'utente per un'operazione.
  
## <a name="members"></a>Membri
  
### <a name="consentlist"></a>ConsentList
Viene chiamato quando l'SDK richiede il consenso dell'utente per un'operazione.

Parametri:  
* **consents**: elenco di consensi richiesti dall'SDK



  
**Restituisce**: risultati [Consent](class_mip_consent.md) Quando l'SDK richiede consensi, l'applicazione client deve ottenere il consenso da parte dell'utente, i risultati di ogni consenso devono essere archiviati tramite [Consent::Result(const ConsentResult&)](class_mip_consent.md#result) e deve essere restituito un elenco dei consensi risolti.