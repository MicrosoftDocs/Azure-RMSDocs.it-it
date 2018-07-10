# <a name="mip-sdk-for-c-preview-reference"></a>Informazioni di riferimento su MIP SDK per C++ (anteprima)

Microsoft Information Protection (MIP) SDK per C++ (anteprima) consente agli sviluppatori di gestire e applicare criteri di protezione dei dati a dati e altre risorse digitali.  

Per altre informazioni, vedere il [blog degli sviluppatori di MIP](https://aka.ms/MIPDevelopers) e gli [esempi di MIP](https://aka.ms/mipsdksamples).

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

| Nome classe | Descrizione |
| :----------|:------------|
[ConsentDelegate](class_consentdelegate.md)  |  Delegato per le operazioni relative al consenso.
[mip::AccessDeniedError](class_mip_accessdeniederror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni, contenuto revocato e così via.
[mip::Action](class_mip_action.md)  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
[mip::AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Classe di azione che specifica l'aggiunta di una filigrana.
[mip::ApplyLabelAction](class_mip_applylabelaction.md)  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
[mip::BadInputError](class_mip_badinputerror.md)  |  Errore di input errato, generato quando l'input per un'API SDK non è valido.
[mip::ClassificationResult](class_mip_classificationresult.md)  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
[mip::ContentLabel](class_mip_contentlabel.md)  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
[mip::CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
[mip::Error](class_mip_error.md)  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
[mip::ExecutionState](class_mip_executionstate.md)  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
[mip::FileEngine](class_mip_fileengine.md)  |  Interfaccia per tutte le funzioni del motore.
[mip::FileEngine::Settings](class_mip_fileengine::settings.md)  | _Non ancora documentato._
[mip::FileHandler](class_mip_filehandler.md)  |  Interfaccia per tutte le funzioni di gestione file.
[mip::FileHandler::Observer](class_mip_filehandler::observer.md)  |  Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero delle notifiche degli eventi correlati al gestore di file da parte dei client.
[mip::FileIOError](class_mip_fileioerror.md)  |  Errore di I/O file.
[mip::FileProfile](class_mip_fileprofile.md)  |  [FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md)  |  Interfaccia [Observer](class_mip_fileprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md)  |  Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
[mip::InternalError](class_mip_internalerror.md)  |  Si è verificato un errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md)  | _Non ancora documentato._
[mip::JustifyAction](class_mip_justifyaction.md)  |  Justify [Action](class_mip_action.md) richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
[mip::Label](class_mip_label.md)  |  Astrazione per una singola etichetta di Microsoft Information Protection.
[mip::LabelingOptions](class_mip_labelingoptions.md)  |  Interfaccia per la configurazione delle opzioni delle etichette per il metodo SetLabel.
[mip::LoggerDelegate](class_mip_loggerdelegate.md)  |  Classe che definisce l'interfaccia per il logger MIP SDK.
[mip::MetadataAction](class_mip_metadataaction.md)  |  Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
[mip::NetworkError](class_mip_networkerror.md)  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
[mip::NotSupportedError](class_mip_notsupportederror.md)  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
[mip::PolicyEngine](class_mip_policyengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  Un'istanza di questa classe con i parametri appropriati è necessaria per avviare un motore.
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
[mip::Profile](class_mip_profile.md)  |  [Profile](class_mip_profile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [Profile](class_mip_profile.md), ma se necessario può creare più profili.
[mip::Profile::Observer](class_mip_profile_observer.md)  |  Interfaccia [Observer](class_mip_profile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
[mip::Profile::Settings](class_mip_profile_settings.md)  |  Oggetto [Settings](class_mip_profile_settings.md) usato da [Profile](class_mip_profile.md) durante la creazione e per tutta la sua durata.
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
[mip::ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
[mip::ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Rappresenta un criterio ad hoc associato al contenuto protetto.
[mip::ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Rappresenta un criterio ad hoc associato al contenuto protetto.
[mip::ProtectionEngine](class_mip_protectionengine.md)  |  Esegue azioni correlate alla protezione relative a un'identità specifica.
[mip::ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
[mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  Oggetto [Settings](class_mip_protectionengine_settings.md) usato da [ProtectionEngine](class_mip_protectionengine.md) durante la creazione e per tutta la sua durata.
[mip::ProtectionHandler](class_mip_protectionhandler.md)  |  Esegue azioni correlate alla protezione per una configurazione di protezione specifica (ad esempio, utenti, diritti, ruoli e così via)
[mip::ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)  |  Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
[mip::ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante la creazione e per tutta la sua durata.
[mip::RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Classe di azione che specifica la rimozione della protezione dal documento.
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Classe di azione che specifica la rimozione della filigrana dal documento.
[mip::Stream](class_mip_stream.md)  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
[mip::UserRights](class_mip_userrights.md)  |  Rappresenta un gruppo di utenti e i diritti ad essi associati.
[mip::UserRoles](class_mip_userroles.md)  |  Rappresenta un gruppo di utenti e i ruoli ad essi associati.

 
