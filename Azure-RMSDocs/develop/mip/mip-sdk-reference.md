# <a name="mip-sdk-for-c-preview-reference"></a>Informazioni di riferimento su MIP SDK per C++ (anteprima)

Microsoft Information Protection (MIP) SDK per C++ (anteprima) consente agli sviluppatori di gestire e applicare criteri di protezione dei dati a dati e altre risorse digitali.  

Per altre informazioni, vedere il [blog degli sviluppatori di MIP](https://aka.ms/MIPDevelopers) e gli [esempi di MIP](https://aka.ms/mipsdksamples).

Microsoft Information Protection SDK per C++ include le classi seguenti:

| Nome classe | Descrizione |
| :----------|:------------|
[mip::Action](class_mip_action.md) | Classe di base per tutte le azioni. |
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md) | Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
[mip::addContentHeaderAction](class_mip_addcontentheaderaction.md) | Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md) | Classe di azione che specifica l'aggiunta di una filigrana.
[mip::BadInputError](class_mip_badinputerror.md) | Errore di input errato, l'input per l'API non è valido.
[mip::CommonRights](class_mip_commonrights.md) | Diritti supportati a livello universale.
[mip::Consent](class_mip_consent.md) | Rappresenta l'accettazione o il rifiuto dell'esecuzione di un'azione da parte di un utente.
[mip::ConsentCallback](class_mip_consentcallback.md) | Interfaccia per le notifiche di richiesta di consenso.
[mip::ConsentResult](class_mip_consentresult.md) | Descrive i risultati della richiesta di consenso dopo l'interazione dell'utente.
[mip::ContentLabel](class_mip_contentlabel.md) | Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
[mip::CustomAction](class_mip_customaction.md) | Classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà.
[mip::CustomProtectedStream](class_mip_customprotectedstream.md) | Esegue il wrapping di un flusso per fornire crittografia e decrittografia trasparenti in lettura e scrittura.
[mip::EditableDocumentRights](class_mip_editabledocumentrights.md) | Diritti che si applicano ai documenti modificabili.
[mip::EmailRights](class_mip_emailrights.md) | Diritti che si applicano alla posta elettronica.
[mip::Error](class_mip_error.md) | Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
[mip::ExecutionState](class_mip_executionstate.md) | Interfaccia per tutti gli stati necessari per eseguire il motore.
[mip::FileEngine](class_mip_fileengine.md) | Interfaccia per tutte le funzioni del motore.
[mip::FileEngine::Settings](class_mip_fileengine_settings.md) | 
[mip::FileHandler](class_mip_filehandler.md) | Interfaccia per tutte le funzioni di gestione file.
[mip::FileHandler::Observer](class_mip_filehandler_observer.md) | Interfaccia Observer per il recupero delle notifiche degli eventi correlati al gestore di file da parte dei client.
[mip::FileIOError](class_mip_fileioerror.md) | Errore di I/O file.
[mip::FileProfile](class_mip_fileprofile.md) | Classe radice per le operazioni di Microsoft Information Protection.
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md) | Interfaccia Observer usata per ricevere notifiche degli eventi relativi al profilo.
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md) | Interfaccia per la gestione delle impostazioni del profilo di file.
[mip::GetUserPolicyResult](class_mip_getuserpolicyresult.md) | Descrive i risultati di una richiesta di acquisizione criteri utente.
[mip::InternalError](class_mip_internalerror.md) | Errore interno dell'SDK. Si è verificato un evento imprevisto.
[mip::IStream](class_mip_istream.md) | Interfaccia di base per i flussi protetti.
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md) | La modifica richiesta richiede una spiegazione.
[mip::JustifyAction](class_mip_justifyaction.md) | La richiesta richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
[mip::Label](class_mip_label.md) | Astrazione per una singola etichetta di Microsoft Information Protection.
[mip::LabelingOptions](class_mip_labelingoptions.md) | Interfaccia per la configurazione delle opzioni delle etichette per il metodo SetLabel.
[mip::MetadataAction](class_mip_metadataaction.md) | Azione che specifica le informazioni sui metadati da aggiungere al contenuto.
[mip::NetworkError](class_mip_networkerror.md) | Errore di rete.
[mip::NotSupportedError](class_mip_notsupportederror.md) | Errore di operazione non supportata.
[mip::PolicyDescriptor](class_mip_policydescriptor.md) | Rappresenta un criterio ad hoc associato al contenuto protetto.
[mip::PolicyEngine](class_mip_policyengine.md) | Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) | Un'istanza di questa classe con i parametri appropriati è necessaria per avviare un motore.
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md) | L'etichetta corrente è stata impostata tramite il metodo di assegnazione dei privilegi e l'override non è possibile.
[mip::Profile](class_mip_profile.md) | Classe radice per le operazioni di Microsoft Information Protection.
[mip::Profile::Observer](class_mip_profile_observer.md) | Interfaccia usata per ricevere notifiche degli eventi correlati al profilo.
[mip::Profile::Settings](class_mip_profile_settings.md) | Configura le impostazioni del profilo.
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md) | Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.  
[mip::ProtectbyTemplateAction](class_mip_protectbytemplateaction.md) | Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md) | Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
[mip::ProtectionProfile](class_mip_protectionprofile.md) | Classe di base usata per eseguire operazioni di protezione.
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) | Usare per ricevere le notifiche relative al profilo di protezione.
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) | Impostazioni del profilo di protezione usate per l'intera durata dell'istanza.
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md) | Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) | Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md) | Classe di azione che specifica la rimozione della protezione dal documento.
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md) | Classe di azione che specifica la rimozione della filigrana dal documento.
[mip::RMSCryptographyException](class_mip_rmscryptographyexception.md) | Eccezione di crittografia di RMS.
[mip::RMSException](class_mip_rmsexception.md) | Eccezione di base di RMS.
[mip::RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) | Eccezione di argomento non valido di RMS.
[mip::RMSLogicException](class_mip_rmslogicexception.md) | Eccezione logica di RMS.
[mip::RMSNetworkException](class_mip_rmsnetworkexception.md) | Eccezione di rete di RMS.
[mip::RMSNotFoundException](class_mip_rmsnotfoundexception.md) | Eccezione elemento non trovato di RMS.
[mip::RMSNullPointerException](class_mip_rmsnullpointerexception.md) | Eccezione puntatore nullo di RMS.
[mip::RMSOfficeFileException](class_mip_rmsofficefileexception.md) | Eccezione file di Office di RMS.
[mip::RMSPFileException](class_mip_rmspfileexception.md) | Eccezione PFile di RMS.
[mip::RMSRightsException](class_mip_rmsrightsexception.md) | Eccezione diritti di RMS.
[mip::RMSStreamException](class_mip_rmsstreamexception.md) | Eccezione flusso di RMS.
[mip::Roles](class_mip_roles.md) | Definisce i ruoli per la protezione dei dati.
[mip::Stream](class_mip_stream.md) | Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
[mip::TemplateDescriptor](class_mip_templatedescriptor.md) | Descrive un modello RMS.
[mip::UserPolicy](class_mip_userpolicy.md) | Rappresenta il criterio associato al contenuto protetto.
[mip::UserRights](class_mip_userrights.md) | Rappresenta un gruppo di utenti e i diritti ad essi associati.
[mip::UserRoles](class_mip_userroles.md) | Rappresenta un gruppo di utenti e i ruoli ad essi associati.
 
