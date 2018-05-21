# <a name="class-mippolicydescriptor"></a>Classe mip::PolicyDescriptor 
Rappresenta un criterio ad hoc associato al contenuto protetto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetName()  |  Ottiene il nome del criterio.
 public void SetName(const std::string& value)  |  Imposta il nome del criterio.
 public const std::string& GetDescription()  |  Ottiene la descrizione del criterio.
 public void SetDescription(const std::string& value)  |  Imposta la descrizione del criterio.
public const std::vector<UserRights>& GetUserRightsList() const  |  Ottiene una raccolta di mapping dei diritti agli utenti.
public const std::vector<mip::UserRoles>& GetUserRolesList()  |  Ottiene una raccolta di mapping dei ruoli agli utenti.
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil()  |  Ottiene la scadenza del criterio.
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  Imposta la scadenza del criterio.
 public bool DoesAllowOfflineAccess()  |  Ottiene un valore che indica se il criterio consente l'accesso al contenuto offline.
 public void SetAllowOfflineAccess(bool value)  |  Imposta un valore che indica se il criterio consente l'accesso al contenuto offline.
 public const std::string& GetReferrer() const  |  Ottiene l'indirizzo del referrer del criterio.
 public void SetReferrer(const std::string& uri)  |  Imposta l'indirizzo del referrer del criterio.
 public const AppDataHashMap& GetEncryptedAppData()  |  Ottiene i dati specifici dell'app che sono stati crittografati.
 public void SetEncryptedAppData(const AppDataHashMap& value)  |  Imposta i dati specifici dell'app da crittografare.
 public const AppDataHashMap& GetSignedAppData()  |  Ottiene i dati specifici dell'app che sono stati firmati.
 public void SetSignedAppData(const AppDataHashMap& value)  |  Imposta i dati specifici dell'app da firmare.
  
## <a name="members"></a>Membri
  
### <a name="getname"></a>GetName
Ottiene il nome del criterio.

  
**Restituisce**: nome del criterio
  
### <a name="setname"></a>SetName
Imposta il nome del criterio.

Parametri:  
* **value**: nome del criterio


  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione del criterio.

  
**Restituisce**: descrizione del criterio
  
### <a name="setdescription"></a>SetDescription
Imposta la descrizione del criterio.

Parametri:  
* **value**: descrizione del criterio


  
### <a name="userrights"></a>UserRights
Ottiene una raccolta di mapping dei diritti agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai diritti Il valore della proprietà UserRightsList sarà vuoto se l'utente corrente non ha accesso alle informazioni sui diritti utente, ad esempio non è il proprietario e non dispone del diritto VIEWRIGHTSDATA.
  
### <a name="mipuserroles"></a>mip::UserRoles
Ottiene una raccolta di mapping dei ruoli agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai ruoli
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Ottiene la scadenza del criterio.

  
**Restituisce**: scadenza del criterio
  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Imposta la scadenza del criterio.

Parametri:  
* **value**: scadenza del criterio


  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Ottiene un valore che indica se il criterio consente l'accesso al contenuto offline.

  
**Restituisce**: valore che indica se il criterio consente l'accesso al contenuto offline (impostazione predefinita = true)
  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Imposta un valore che indica se il criterio consente l'accesso al contenuto offline.

Parametri:  
* **value**: valore che indica se il criterio consente l'accesso al contenuto offline


  
### <a name="getreferrer"></a>GetReferrer
Ottiene l'indirizzo del referrer del criterio.

  
**Restituisce**: indirizzo del referrer del criterio Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setreferrer"></a>SetReferrer
Imposta l'indirizzo del referrer del criterio.

Parametri:  
* **uri**: indirizzo del referrer del criterio


Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="appdatahashmap"></a>AppDataHashMap
Ottiene i dati specifici dell'app che sono stati crittografati.

  
**Restituisce**: dati specifici dell'app Un oggetto [UserPolicy](class_mip_userpolicy.md) può contenere un dizionario di dati specifici dell'app che sono stati crittografati dal servizio RMS. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [PolicyDescriptor::GetSignedAppData](class_mip_policydescriptor.md#getsignedappdata)
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Imposta i dati specifici dell'app da crittografare.

Parametri:  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio RMS. Questi dati crittografati sono indipendenti dai dati firmati impostati da [PolicyDescriptor::SetSignedAppData](class_mip_policydescriptor.md#setsignedappdata).
  
### <a name="appdatahashmap"></a>AppDataHashMap
Ottiene i dati specifici dell'app che sono stati firmati.

  
**Restituisce**: dati specifici dell'app Un oggetto [UserPolicy](class_mip_userpolicy.md) può contenere un dizionario di dati specifici dell'app che sono stati firmati dal servizio RMS. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [PolicyDescriptor::GetEncryptedAppData](class_mip_policydescriptor.md#getencryptedappdata)
  
### <a name="setsignedappdata"></a>SetSignedAppData
Imposta i dati specifici dell'app da firmare.

Parametri:  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio RMS. Questi dati firmati sono indipendenti dai dati crittografati impostati da [PolicyDescriptor::SetEncryptedAppData](class_mip_policydescriptor.md#setencryptedappdata).