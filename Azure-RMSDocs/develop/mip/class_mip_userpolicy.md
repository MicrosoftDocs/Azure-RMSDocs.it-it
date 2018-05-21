# <a name="class-mipuserpolicy"></a>Classe mip::UserPolicy 
Rappresenta il criterio associato al contenuto protetto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public bool AccessCheck(const std::string& right) const  |  Controlla se il criterio concede all'utente l'accesso al diritto specificato.
 public UserPolicyType GetType()  |  Ottiene il tipo di criterio.
 public std::string GetName()  |  Ottiene il nome del criterio.
 public std::string GetDescription()  |  Ottiene la descrizione del criterio.
public std::shared_ptr<TemplateDescriptor> GetTemplateDescriptor()  |  Ottiene [TemplateDescriptor](class_mip_templatedescriptor.md) per un oggetto [UserPolicy](class_mip_userpolicy.md) basato su modello.
public std::shared_ptr<PolicyDescriptor> GetPolicyDescriptor()  |  Ottiene [PolicyDescriptor](class_mip_policydescriptor.md) per un oggetto [UserPolicy](class_mip_userpolicy.md) ad hoc.
 public std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
 public std::string GetIssuedTo()  |  Ottiene l'utente associato al criterio di protezione.
 public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è il proprietario del contenuto.
 public std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
 public const mip::AppDataHashMap GetEncryptedAppData()  |  Ottiene i dati specifici dell'app che sono stati crittografati.
 public const mip::AppDataHashMap GetSignedAppData()  |  Ottiene i dati specifici dell'app che sono stati firmati.
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil()  |  Ottiene la scadenza del criterio.
 public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il criterio usa algoritmi di crittografia deprecati (ECB) per compatibilità con le versioni precedenti.
 public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il criterio concede all'utente il diritto "audited extract".
public const std::vector<unsigned char> GetSerializedPolicy()  |  Serializza [UserPolicy](class_mip_userpolicy.md) in una licenza di pubblicazione
public std::shared_ptr<rmscore::core::ProtectionPolicy> GetImpl()  |  Ottiene l'implementazione della classe interna derivata [UserPolicy](class_mip_userpolicy.md).
  
## <a name="members"></a>Membri
  
### <a name="accesscheck"></a>AccessCheck
Controlla se il criterio concede all'utente l'accesso al diritto specificato.

Parametri:  
* **right**: diritto da controllare



  
**Restituisce**: valore che indica se il criterio concede all'utente l'accesso al diritto specificato
  
### <a name="userpolicytype"></a>UserPolicyType
Ottiene il tipo di criterio.

  
**Restituisce**: tipo di criterio
  
### <a name="getname"></a>GetName
Ottiene il nome del criterio.

  
**Restituisce**: nome del criterio
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione del criterio.

  
**Restituisce**: descrizione del criterio
  
### <a name="templatedescriptor"></a>TemplateDescriptor
Ottiene [TemplateDescriptor](class_mip_templatedescriptor.md) per un oggetto [UserPolicy](class_mip_userpolicy.md) basato su modello.

  
**Restituisce**: [TemplateDescriptor](class_mip_templatedescriptor.md) se [UserPolicy](class_mip_userpolicy.md) è basato su modello, in caso contrario nullptr
  
### <a name="policydescriptor"></a>PolicyDescriptor
Ottiene [PolicyDescriptor](class_mip_policydescriptor.md) per un oggetto [UserPolicy](class_mip_userpolicy.md) ad hoc.

  
**Restituisce**: [PolicyDescriptor](class_mip_policydescriptor.md) se [UserPolicy](class_mip_userpolicy.md) è ad hoc, in caso contrario nullptr
  
### <a name="getowner"></a>GetOwner
Ottiene indirizzo e-mail del proprietario del contenuto.

  
**Restituisce**: indirizzo di posta elettronica del proprietario del contenuto
  
### <a name="getissuedto"></a>GetIssuedTo
Ottiene l'utente associato al criterio di protezione.

  
**Restituisce**: utente associato al criterio di protezione
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Ottiene un valore che indica se l'utente corrente è il proprietario del contenuto.

  
**Restituisce**: valore che indica se l'utente corrente è il proprietario del contenuto
  
### <a name="getcontentid"></a>GetContentId
Ottiene l'identificatore univoco del documento/contenuto.

  
**Restituisce**: identificatore univoco del contenuto
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Ottiene i dati specifici dell'app che sono stati crittografati.
Un oggetto [UserPolicy](class_mip_userpolicy.md) può contenere un dizionario di dati specifici dell'app che sono stati crittografati dal servizio RMS. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [UserPolicy::GetSignedAppData](class_mip_userpolicy.md#getsignedappdata)
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Ottiene i dati specifici dell'app che sono stati firmati.
Un oggetto [UserPolicy](class_mip_userpolicy.md) può contenere un dizionario di dati specifici dell'app che sono stati firmati dal servizio RMS. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [UserPolicy::GetEncryptedAppData](class_mip_userpolicy.md#getencryptedappdata)
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Ottiene la scadenza del criterio.

  
**Restituisce**: scadenza del criterio
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Ottiene un valore che indica se il criterio usa algoritmi di crittografia deprecati (ECB) per compatibilità con le versioni precedenti.

  
**Restituisce**: valore che indica se il criterio usa algoritmi di crittografia deprecati
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Ottiene un valore che indica se il criterio concede all'utente il diritto "audited extract".

  
**Restituisce**: valore che indica se il criterio concede all'utente il diritto 'audited extract'
  
### <a name="getserializedpolicy"></a>GetSerializedPolicy
Serializza [UserPolicy](class_mip_userpolicy.md) in una licenza di pubblicazione

  
**Restituisce**: [UserPolicy](class_mip_userpolicy.md) serializzato
  
### <a name="getimpl"></a>GetImpl
Ottiene l'implementazione della classe interna derivata [UserPolicy](class_mip_userpolicy.md).

  
**Restituisce**: implementazione della classe derivata solo per uso interno [UserPolicy](class_mip_userpolicy.md)