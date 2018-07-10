# <a name="class-mipprotectiondescriptor"></a>Classe mip::ProtectionDescriptor 
Rappresenta un criterio ad hoc associato al contenuto protetto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.
 public const std::string& GetName() const  |  Ottiene il nome del criterio.
 public const std::string& GetDescription() const  |  Ottiene la descrizione del criterio.
 public const std::string& GetTemplateId() const  |  Ottiene l'ID del modello di protezione.
public const std::vector<UserRights>& GetUserRights() const  |  Ottiene una raccolta di mapping dei diritti agli utenti.
public const std::vector<UserRoles>& GetUserRoles() const  |  Ottiene una raccolta di mapping dei ruoli agli utenti.
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil() const  |  Ottiene la scadenza del criterio.
 public bool DoesAllowOfflineAccess() const  |  Ottiene un valore che indica se il criterio consente l'accesso al contenuto offline.
 public const std::string& GetReferrer() const  |  Ottiene l'indirizzo del referrer del criterio.
public const std::map<std::string, std::string>& GetEncryptedAppData() const  |  Ottiene i dati specifici dell'app che sono stati crittografati.
public const std::map<std::string, std::string>& GetSignedAppData() const  |  Ottiene i dati specifici dell'app che sono stati firmati.
  
## <a name="members"></a>Membri
  
### <a name="protectiontype"></a>ProtectionType
Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.

  
**Restituisce**: tipo di protezione
  
### <a name="getname"></a>GetName
Ottiene il nome del criterio.

  
**Restituisce**: nome del criterio
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione del criterio.

  
**Restituisce**: descrizione del criterio
  
### <a name="gettemplateid"></a>GetTemplateId
Ottiene l'ID del modello di protezione.

  
**Restituisce**: ID del modello
  
### <a name="userrights"></a>UserRights
Ottiene una raccolta di mapping dei diritti agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai diritti. Il valore della proprietà [UserRights](class_mip_userrights.md) sarà vuoto se l'utente corrente non ha accesso alle informazioni sui diritti utente, ad esempio non è il proprietario e non ha il diritto VIEWRIGHTSDATA.
  
### <a name="userroles"></a>UserRoles
Ottiene una raccolta di mapping dei ruoli agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai ruoli
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Ottiene la scadenza del criterio.

  
**Restituisce**: scadenza del criterio
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Ottiene un valore che indica se il criterio consente l'accesso al contenuto offline.

  
**Restituisce**: valore che indica se il criterio consente l'accesso al contenuto offline (impostazione predefinita = true)
  
### <a name="getreferrer"></a>GetReferrer
Ottiene l'indirizzo del referrer del criterio.

  
**Restituisce**: indirizzo del referrer del criterio Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
Ottiene i dati specifici dell'app che sono stati crittografati.

  
**Restituisce**: dati specifici dell'app. [ProtectionHandler](class_mip_protectionhandler.md) può contenere un dizionario di dati specifici dell'app crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata)
  
### <a name="getsignedappdata"></a>GetSignedAppData
Ottiene i dati specifici dell'app che sono stati firmati.

  
**Restituisce**: dati specifici dell'app. Un oggetto [ProtectionHandler](class_mip_protectionhandler.md) può contenere un dizionario di dati specifici dell'app che sono stati firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata)