# <a name="class-mipprotectionprofileobserver"></a>Classe mip::ProtectionProfile::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionProfile](#classmip_1_1_protection_profile).
Questa interfaccia deve implementata dalle applicazioni che usano l'SDK di protezione
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProtectionProfile > & profile,const std::shared_ptr< void > & context) | Viene chiamato quando il profilo è stato caricato correttamente.
public inline virtual void OnLoadFailure | Viene chiamato quando il caricamento di un profilo ha causato un errore.
## <a name="members"></a>Membri
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.
#### <a name="parameters"></a>Parametri
* profile Riferimento all'oggetto [ProtectionProfile](#classmip_1_1_protection_profile) appena creato
* context Lo stesso contesto passato a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) o [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.
#### <a name="parameters"></a>Parametri
* error Evento [Error](#classmip_1_1_error) che si è verificato durante il caricamento 
* context Lo stesso contesto passato a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function e così via) a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) o [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)