---
title: SDK MIP per C++ riferimento
description: SDK MIP per C++ riferimento
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f1e5e06332cac6c0f8beba089d92654781ff6f71
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560429"
---
# <a name="mip-sdk-for-c-reference"></a>SDK MIP per C++ riferimento

Microsoft Information Protection (MIP) SDK per C++ consente agli sviluppatori di gestire e applicare i criteri di protezione dei dati ai dati e ad altre risorse digitali.

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

 Classe                         | Description                                
--------------------------------|---------------------------------------------
[Classe MIP:: AccessDeniedError](class_mip_accessdeniederror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[Classe MIP:: Action](class_mip_action.md)  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
[Classe MIP:: ActionData](class_mip_actiondata.md)  | Non ancora documentato.
[Classe MIP:: AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
[Classe MIP:: AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
[Classe MIP:: AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Classe di azione che specifica l'aggiunta di una filigrana.
[Classe MIP:: AddWatermarkActionData](class_mip_addwatermarkactiondata.md)  | Non ancora documentato.
[Classe MIP:: AdhocProtectionRequiredError](class_mip_adhocprotectionrequirederror.md)  |  È necessario impostare la protezione ad hoc per completare l'azione sul file.
[Classe MIP:: ApplicationActionState](class_mip_applicationactionstate.md)  | Non ancora documentato.
[Classe MIP:: ApplyLabelAction](class_mip_applylabelaction.md)  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
[Classe MIP:: ArgumentData](class_mip_argumentdata.md)  | Non ancora documentato.
[Classe MIP:: AuthDelegate](class_mip_authdelegate.md)  |  Delegato per le operazioni correlate all'autenticazione.
[Classe MIP:: AuthDelegate:: OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
[Classe MIP:: AuthDelegate:: OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  Classe che definisce il modo in cui l'SDK MIP prevede che il token OAuth2 venga passato nuovamente all'SDK.
[Classe MIP:: BadInputError](class_mip_badinputerror.md)  |  Errore di input non corretto, generato quando l'input per un'API SDK non è valido.
[Classe MIP:: ClassificationData](class_mip_classificationdata.md)  | Non ancora documentato.
[Classe MIP:: ClassificationRequest](class_mip_classificationrequest.md)  |  Classe che contiene la richiesta di una chiamata di classificazione sullo stato di esecuzione.
[Classe MIP:: ClassificationResult](class_mip_classificationresult.md)  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
[Classe MIP:: ComputeEngine](class_mip_computeengine.md)  | Non ancora documentato.
[Classe MIP:: ComputeEngine:: Settings](class_mip_computeengine_settings.md)  | Non ancora documentato.
[Classe MIP:: ComputeEngineContext](class_mip_computeenginecontext.md)  | Non ancora documentato.
[Classe MIP:: ConditionData](class_mip_conditiondata.md)  | Non ancora documentato.
[Classe MIP:: ConsentDelegate](class_mip_consentdelegate.md)  |  Delegato per le operazioni relative al consenso.
[Classe MIP:: ConsentDeniedError](class_mip_consentdeniederror.md)  |  Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
[Classe MIP:: ContentLabel](class_mip_contentlabel.md)  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
[Classe MIP:: ContentMarkingActionData](class_mip_contentmarkingactiondata.md)  | Non ancora documentato.
[Classe MIP:: CustomAction](class_mip_customaction.md)  |  CustomAction è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
[Classe MIP::D eprecatedApiError](class_mip_deprecatedapierror.md)  |  Il chiamante ha richiamato un'API deprecata.
[Classe MIP::D ocumentState](class_mip_documentstate.md)  | Non ancora documentato.
[Classe MIP:: Error](class_mip_error.md)  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
[Classe MIP:: ExecutionState](class_mip_executionstate.md)  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
[Classe MIP:: fileengine](class_mip_fileengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[Classe MIP:: fileengine:: Settings](class_mip_fileengine_settings.md)  | Non ancora documentato.
[Classe MIP:: FileExecutionState](class_mip_fileexecutionstate.md)  | Non ancora documentato.
[Classe MIP:: FileHandler](class_mip_filehandler.md)  |  Interfaccia per tutte le funzioni di gestione file.
[Classe MIP:: FileHandler:: Observer](class_mip_filehandler_observer.md)  |  Interfaccia Observer che consente ai client di ottenere gli eventi di notifica correlati al gestore di file.
[Classe MIP:: fileinspector](class_mip_fileinspector.md)  | Non ancora documentato.
[Classe MIP:: FileIOError](class_mip_fileioerror.md)  |  Errore di I/O file.
[Classe MIP:: fileprofile](class_mip_fileprofile.md)  |  Fileprofile Class è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
[Classe MIP:: fileprofile:: Observer](class_mip_fileprofile_observer.md)  |  Interfaccia Observer che consente ai client di ricevere notifiche per gli eventi correlati al profilo.
[Classe MIP:: fileprofile:: Settings](class_mip_fileprofile_settings.md)  |  Impostazioni utilizzate da fileprofile durante la sua creazione e per tutta la sua durata.
[Classe MIP:: HttpDelegate](class_mip_httpdelegate.md)  |  Interfaccia per l'override della gestione HTTP.
[Classe MIP:: HttpOperation](class_mip_httpoperation.md)  |  Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
[Classe MIP:: HttpRequest](class_mip_httprequest.md)  |  Interfaccia che descrive una singola richiesta HTTP.
[Classe MIP:: HttpResponse](class_mip_httpresponse.md)  |  Interfaccia che descrive una singola risposta HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
[Classe MIP:: Identity](class_mip_identity.md)  |  Astrazione per Identity.
[Classe MIP:: InternalError](class_mip_internalerror.md)  |  Si è verificato un errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
[Classe MIP:: JustificationRequiredError](class_mip_justificationrequirederror.md)  | Non ancora documentato.
[Classe MIP:: JustifyAction](class_mip_justifyaction.md)  |  Per giustificare l'azione è necessario fornire una giustificazione al downgrade di un'etichetta e impostare la risposta nello stato di esecuzione.
[Classe MIP:: Label](class_mip_label.md)  |  Astrazione per una singola etichetta di Microsoft Information Protection.
[Classe MIP:: LabelActionData](class_mip_labelactiondata.md)  | Non ancora documentato.
[Classe MIP:: LabelDisabledError](class_mip_labeldisablederror.md)  |  Label è disabilitato o inattivo.
[Classe MIP:: LabelGroupData](class_mip_labelgroupdata.md)  | Non ancora documentato.
[Classe MIP:: LabelingOptions](class_mip_labelingoptions.md)  |  Interfaccia per la configurazione delle opzioni delle etichette per i metodi SetLabel/DeleteLabel.
[Classe MIP:: LabelNotFoundError](class_mip_labelnotfounderror.md)  |  ID etichetta non riconosciuto.
[Classe MIP:: LoggerDelegate](class_mip_loggerdelegate.md)  |  Classe che definisce l'interfaccia per il logger MIP SDK.
[Classe MIP:: MetadataAction](class_mip_metadataaction.md)  |  Azione che aggiunge informazioni sui metadati al contenuto.
[Classe MIP:: MipContext](class_mip_mipcontext.md)  |  MipContext rappresenta lo stato condiviso tra tutti i profili, i motori e i gestori.
[Classe MIP:: MsgAttachmentData](class_mip_msgattachmentdata.md)  | Non ancora documentato.
[Classe MIP:: MsgInspector](class_mip_msginspector.md)  | Non ancora documentato.
[Classe MIP:: NetworkError](class_mip_networkerror.md)  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
[Classe MIP:: NoAuthTokenError](class_mip_noauthtokenerror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto a causa di un token di autenticazione mancante.
[Classe MIP:: NoPermissionsError](class_mip_nopermissionserror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[Classe MIP:: NoPolicyError](class_mip_nopolicyerror.md)  |  I criteri del tenant non sono configurati per la classificazione o le etichette.
[Classe MIP:: NotSupportedError](class_mip_notsupportederror.md)  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
[Classe MIP:: OperationCancelledError](class_mip_operationcancellederror.md)  |  Operazione annullata.
[Classe MIP::P olicyEngine](class_mip_policyengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[Classe MIP::P olicyEngine:: Settings](class_mip_policyengine_settings.md)  |  Definisce le impostazioni associate a un PolicyEngine.
[Classe MIP::P olicyHandler](class_mip_policyhandler.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
[Classe MIP::P olicyPackageData](class_mip_policypackagedata.md)  | Non ancora documentato.
[Classe MIP::P olicyProfile](class_mip_policyprofile.md)  |  La classe PolicyProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica richiederà solo un PolicyProfile, ma può creare più profili, se necessario.
[Classe MIP::P olicyProfile:: Observer](class_mip_policyprofile_observer.md)  |  Interfaccia Observer che consente ai client di ricevere notifiche per gli eventi correlati al profilo.
[Classe MIP::P olicyProfile:: Settings](class_mip_policyprofile_settings.md)  |  Impostazioni utilizzate da PolicyProfile durante la sua creazione e per tutta la sua durata.
[Classe MIP::P olicyRuleData](class_mip_policyruledata.md)  | Non ancora documentato.
[Classe MIP::P olicySyncError](class_mip_policysyncerror.md)  |  Tentativo di sincronizzare i dati dei criteri non riuscito.
[Classe MIP::P rivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
[Classe MIP::P ropertyData](class_mip_propertydata.md)  | Non ancora documentato.
[Classe MIP::P rotectAdhocAction](class_mip_protectadhocaction.md)  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
[Classe MIP::P rotectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
[Classe MIP::P rotectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
[Classe MIP::P rotectionActionData](class_mip_protectionactiondata.md)  | Non ancora documentato.
[Classe MIP::P rotectionDescriptor](class_mip_protectiondescriptor.md)  |  Descrizione della protezione associata a una parte del contenuto.
[Classe MIP::P rotectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Costruisce un ProtectionDescriptor che descrive la protezione associata a una porzione di contenuto.
[Classe MIP::P rotectionEngine](class_mip_protectionengine.md)  |  Gestisce azioni correlate alla protezione relative a un'identità specifica.
[Classe MIP::P rotectionEngine:: Observer](class_mip_protectionengine_observer.md)  |  Interfaccia che riceve le notifiche correlate a ProtectionEngine.
[Classe MIP::P rotectionEngine:: Settings](class_mip_protectionengine_settings.md)  |  Impostazioni utilizzate da ProtectionEngine durante la sua creazione e per tutta la sua durata.
[Classe MIP::P rotectionHandler](class_mip_protectionhandler.md)  |  Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
[Classe MIP::P rotectionHandler:: ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  Impostazioni utilizzate per creare un ProtectionHandler per utilizzare il contenuto esistente.
[Classe MIP::P rotectionHandler:: Observer](class_mip_protectionhandler_observer.md)  |  Interfaccia che riceve le notifiche correlate a ProtectionHandler.
[Classe MIP::P rotectionHandler::P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  Impostazioni usate per creare un ProtectionHandler per proteggere il nuovo contenuto.
[Classe MIP::P rotectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile è la classe radice per l'esecuzione di operazioni di protezione.
[Classe MIP::P rotectionProfile:: Observer](class_mip_protectionprofile_observer.md)  |  Interfaccia che riceve le notifiche correlate a ProtectionProfile.
[Classe MIP::P rotectionProfile:: Settings](class_mip_protectionprofile_settings.md)  |  Impostazioni utilizzate da ProtectionProfile durante la sua creazione e per tutta la sua durata.
[Classe MIP::P rotectionSettings](class_mip_protectionsettings.md)  |  Interfaccia per la configurazione delle opzioni di protezione dati per il metodo selabel.
[Classe MIP::P roxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  Errore di autenticazione del proxy.
[Classe MIP::P ublishingLicenseInfo](class_mip_publishinglicenseinfo.md)  |  Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
[Classe MIP:: RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
[Classe MIP:: RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
[Classe MIP:: RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
[Classe MIP:: RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Classe di azione che specifica la rimozione della protezione dal documento.
[Classe MIP:: RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Classe di azione che specifica la rimozione della filigrana dal documento.
[Classe MIP:: RulePackageData](class_mip_rulepackagedata.md)  | Non ancora documentato.
[Classe MIP:: SensitivityConditionData](class_mip_sensitivityconditiondata.md)  | Non ancora documentato.
[Classe MIP:: SensitivityTypesRulePackage](class_mip_sensitivitytypesrulepackage.md)  | Non ancora documentato.
[Classe MIP:: ServiceDisabledError](class_mip_servicedisablederror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione di un servizio.
[Classe MIP:: Stream](class_mip_stream.md)  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
[Classe MIP:: SyncFileBaseData](class_mip_syncfilebasedata.md)  | Non ancora documentato.
[Classe MIP:: SyncFilePolicyData](class_mip_syncfilepolicydata.md)  | Non ancora documentato.
[Classe MIP:: SyncFileSensitivityData](class_mip_syncfilesensitivitydata.md)  | Non ancora documentato.
[Classe MIP:: TaskDispatcherDelegate](class_mip_taskdispatcherdelegate.md)  |  Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
[Classe MIP:: TemplateNotFoundError](class_mip_templatenotfounderror.md)  |  ID modello non riconosciuto dal servizio RMS.
[Classe MIP:: TransientNetworkError](class_mip_transientnetworkerror.md)  |  Errore di rete temporaneo. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio. È possibile ripetere l'operazione dal momento che l'errore è temporaneo.
[Classe MIP:: UserRights](class_mip_userrights.md)  |  Gruppo di utenti e diritti ad essi associati.
[Classe MIP:: UserRoles](class_mip_userroles.md)  |  Gruppo di utenti e ruoli ad essi associati.