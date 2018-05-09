# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
[ProtectionProfile](#classmip_1_1_protection_profile) è la classe radice per l'esecuzione di operazioni di protezione.
Un'applicazione deve creare [ProtectionProfile](#classmip_1_1_protection_profile) prima di eseguire qualsiasi operazione di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni usate da [ProtectionProfile](#classmip_1_1_protection_profile) durante l'inizializzazione e per tutta la sua durata.
public void ClearCaches()  |  Elimina le cache (ad esempio i database dei consensi e così via)
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni usate da [ProtectionProfile](#classmip_1_1_protection_profile) durante l'inizializzazione e per tutta la sua durata.
  
#### <a name="returns"></a>Returns
Oggetto [Settings](#classmip_1_1_protection_profile_1_1_settings) usato da [ProtectionProfile](#classmip_1_1_protection_profile) durante l'inizializzazione e per tutta la sua durata
  
### <a name="clearcaches"></a>ClearCaches
Elimina le cache (ad esempio i database dei consensi e così via) Utile a scopi di debug e test