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
  
#### <a name="returns"></a>Returns
Nome criteri
  
### <a name="setname"></a>SetName
Imposta il nome del criterio.
  
#### <a name="parameters"></a>Parametri
* value Nome del criterio
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione del criterio.
  
#### <a name="returns"></a>Returns
Descrizione del criterio
  
### <a name="setdescription"></a>SetDescription
Imposta la descrizione del criterio.
  
#### <a name="parameters"></a>Parametri
* value Descrizione del criterio
  
### <a name="userrights"></a>UserRights
Ottiene una raccolta di mapping dei diritti agli utenti.
  
#### <a name="returns"></a>Returns
Raccolta di mapping dei diritti agli utenti Il valore della proprietà UserRightsList sarà vuoto se l'utente corrente non ha accesso alle informazioni sui diritti utente, ad esempio non è il proprietario e non dispone del diritto VIEWRIGHTSDATA.
  
### <a name="mipuserroles"></a>mip::UserRoles
Ottiene una raccolta di mapping dei ruoli agli utenti.
  
#### <a name="returns"></a>Returns
Raccolta di mapping dei ruoli agli utenti
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Ottiene la scadenza del criterio.
  
#### <a name="returns"></a>Returns
Scadenza del criterio
  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Imposta la scadenza del criterio.
  
#### <a name="parameters"></a>Parametri
* value Scadenza del criterio
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Ottiene un valore che indica se il criterio consente l'accesso al contenuto offline.
  
#### <a name="returns"></a>Returns
Valore che indica se il criterio consente l'accesso al contenuto offline (impostazione predefinita = true)
  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Imposta un valore che indica se il criterio consente l'accesso al contenuto offline.
  
#### <a name="parameters"></a>Parametri
* value Valore che indica se il criterio consente l'accesso al contenuto offline
  
### <a name="getreferrer"></a>GetReferrer
Ottiene l'indirizzo del referrer del criterio.
  
#### <a name="returns"></a>Returns
Indirizzo del referrer del criterio. Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setreferrer"></a>SetReferrer
Imposta l'indirizzo del referrer del criterio.
  
#### <a name="parameters"></a>Parametri
* uri Indirizzo del referrer del criterio Il referrer è un URI che può essere visualizzato se l'acquisizione di un criterio non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="appdatahashmap"></a>AppDataHashMap
Ottiene i dati specifici dell'app che sono stati crittografati.
  
#### <a name="returns"></a>Returns
Dati specifici dell'app Un oggetto [UserPolicy](#classmip_1_1_user_policy) può contenere un dizionario di dati specifici dell'app che sono stati crittografati dal servizio RMS. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [PolicyDescriptor::GetSignedAppData](#classmip_1_1_policy_descriptor_1ad523870efc92f9f81c82121a054d74d4)
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Imposta i dati specifici dell'app da crittografare.
  
#### <a name="parameters"></a>Parametri
* value Dati specifici dell'app Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio RMS. Questi dati crittografati sono indipendenti dai dati firmati impostati da [PolicyDescriptor::SetSignedAppData](#classmip_1_1_policy_descriptor_1a00f35c0b91e48ccdcc6387466a61f362).
  
### <a name="appdatahashmap"></a>AppDataHashMap
Ottiene i dati specifici dell'app che sono stati firmati.
  
#### <a name="returns"></a>Returns
Dati specifici dell'app Un oggetto [UserPolicy](#classmip_1_1_user_policy) può contenere un dizionario di dati specifici dell'app che sono stati firmati dal servizio RMS. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [PolicyDescriptor::GetEncryptedAppData](#classmip_1_1_policy_descriptor_1a9a5bcf9d1bf7357de549429179197ab6)
  
### <a name="setsignedappdata"></a>SetSignedAppData
Imposta i dati specifici dell'app da firmare.
  
#### <a name="parameters"></a>Parametri
* value Dati specifici dell'app Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio RMS. Questi dati firmati sono indipendenti dai dati crittografati impostati da [PolicyDescriptor::SetEncryptedAppData](#classmip_1_1_policy_descriptor_1a5275224932dc17319092304497e59eb2).