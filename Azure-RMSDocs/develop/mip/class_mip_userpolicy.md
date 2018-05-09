# <a name="class-mipuserpolicy"></a>Classe mip::UserPolicy 
Rappresenta il criterio associato al contenuto protetto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public bool AccessCheck(const std::string& right) const  |  Controlla se il criterio concede all'utente l'accesso al diritto specificato.
public UserPolicyType GetType()  |  Ottiene il tipo di criterio.
public std::string GetName()  |  Ottiene il nome del criterio.
public std::string GetDescription()  |  Ottiene la descrizione del criterio.
public std::shared_ptr<TemplateDescriptor> GetTemplateDescriptor()  |  Ottiene [TemplateDescriptor](#classmip_1_1_template_descriptor) per un oggetto [UserPolicy](#classmip_1_1_user_policy) basato su modello.
public std::shared_ptr<PolicyDescriptor> GetPolicyDescriptor()  |  Ottiene [PolicyDescriptor](#classmip_1_1_policy_descriptor) per un oggetto [UserPolicy](#classmip_1_1_user_policy) ad hoc.
public std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
public std::string GetIssuedTo()  |  Ottiene l'utente associato al criterio di protezione.
public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è il proprietario del contenuto.
public std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
public const mip::AppDataHashMap GetEncryptedAppData()  |  Ottiene i dati specifici dell'app che sono stati crittografati.
public const mip::AppDataHashMap GetSignedAppData()  |  Ottiene i dati specifici dell'app che sono stati firmati.
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil()  |  Ottiene la scadenza del criterio.
public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il criterio usa algoritmi di crittografia deprecati (ECB) per compatibilità con le versioni precedenti.
public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il criterio concede all'utente il diritto "audited extract".
public const std::vector<unsigned char> GetSerializedPolicy()  |  Serializza [UserPolicy](#classmip_1_1_user_policy) in una licenza di pubblicazione
public std::shared_ptr<rmscore::core::ProtectionPolicy> GetImpl()  |  Ottiene l'implementazione della classe interna derivata [UserPolicy](#classmip_1_1_user_policy).
  
## <a name="members"></a>Membri
  
### <a name="accesscheck"></a>AccessCheck
Controlla se il criterio concede all'utente l'accesso al diritto specificato.
  
#### <a name="parameters"></a>Parametri
* right Diritto da controllare
  
#### <a name="returns"></a>Returns
Valore che indica se il criterio concede all'utente l'accesso al diritto specificato
  
### <a name="userpolicytype"></a>UserPolicyType
Ottiene il tipo di criterio.
  
#### <a name="returns"></a>Returns
Tipo di criteri
  
### <a name="getname"></a>GetName
Ottiene il nome del criterio.
  
#### <a name="returns"></a>Returns
Nome criteri
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione del criterio.
  
#### <a name="returns"></a>Returns
Descrizione del criterio
  
### <a name="templatedescriptor"></a>TemplateDescriptor
Ottiene [TemplateDescriptor](#classmip_1_1_template_descriptor) per un oggetto [UserPolicy](#classmip_1_1_user_policy) basato su modello.
  
#### <a name="returns"></a>Returns
[TemplateDescriptor](#classmip_1_1_template_descriptor) se [UserPolicy](#classmip_1_1_user_policy) è basato su modello, in caso contrario nullptr
  
### <a name="policydescriptor"></a>PolicyDescriptor
Ottiene [PolicyDescriptor](#classmip_1_1_policy_descriptor) per un oggetto [UserPolicy](#classmip_1_1_user_policy) ad hoc.
  
#### <a name="returns"></a>Returns
[PolicyDescriptor](#classmip_1_1_policy_descriptor) se [UserPolicy](#classmip_1_1_user_policy) è ad hoc, in caso contrario nullptr
  
### <a name="getowner"></a>GetOwner
Ottiene indirizzo e-mail del proprietario del contenuto.
  
#### <a name="returns"></a>Returns
Indirizzo e-mail del proprietario del contenuto
  
### <a name="getissuedto"></a>GetIssuedTo
Ottiene l'utente associato al criterio di protezione.
  
#### <a name="returns"></a>Returns
Utente associato al criterio di protezione
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Ottiene un valore che indica se l'utente corrente è il proprietario del contenuto.
  
#### <a name="returns"></a>Returns
Valore che indica se l'utente corrente è il proprietario del contenuto
  
### <a name="getcontentid"></a>GetContentId
Ottiene l'identificatore univoco del documento/contenuto.
  
#### <a name="returns"></a>Returns
Identificatore univoco del contenuto
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Ottiene i dati specifici dell'app che sono stati crittografati.
Un oggetto [UserPolicy](#classmip_1_1_user_policy) può contenere un dizionario di dati specifici dell'app che sono stati crittografati dal servizio RMS. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [UserPolicy::GetSignedAppData](#classmip_1_1_user_policy_1a1c8a284d50adcac1a0a09316afa1d43e)
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Ottiene i dati specifici dell'app che sono stati firmati.
Un oggetto [UserPolicy](#classmip_1_1_user_policy) può contenere un dizionario di dati specifici dell'app che sono stati firmati dal servizio RMS. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [UserPolicy::GetEncryptedAppData](#classmip_1_1_user_policy_1a610fbc799284ab0ce4354c0611ece0e8)
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Ottiene la scadenza del criterio.
  
#### <a name="returns"></a>Returns
Scadenza del criterio
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Ottiene un valore che indica se il criterio usa algoritmi di crittografia deprecati (ECB) per compatibilità con le versioni precedenti.
  
#### <a name="returns"></a>Returns
Valore che indica se il criterio usa algoritmi di crittografia deprecati
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Ottiene un valore che indica se il criterio concede all'utente il diritto "audited extract".
  
#### <a name="returns"></a>Returns
Valore che indica se il criterio concede all'utente il diritto "audited extract"
  
### <a name="getserializedpolicy"></a>GetSerializedPolicy
Serializza [UserPolicy](#classmip_1_1_user_policy) in una licenza di pubblicazione
  
#### <a name="returns"></a>Returns
[UserPolicy](#classmip_1_1_user_policy) serializzato
  
### <a name="getimpl"></a>GetImpl
Ottiene l'implementazione della classe interna derivata [UserPolicy](#classmip_1_1_user_policy).
  
#### <a name="returns"></a>Returns
Implementazione della classe derivata solo per uso interno [UserPolicy](#classmip_1_1_user_policy)