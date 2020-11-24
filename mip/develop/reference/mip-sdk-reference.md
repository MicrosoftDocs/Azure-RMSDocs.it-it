---
title: Guida di riferimento a MIP SDK per C++
description: Guida di riferimento a MIP SDK per C++
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: da5ee17fbb177fe9b6e37461a5d35425a3945e59
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566759"
---
# <a name="mip-sdk-for-c-reference"></a>Guida di riferimento a MIP SDK per C++

Microsoft Information Protection (MIP) SDK per C++ consente agli sviluppatori di gestire e applicare i criteri di protezione dei dati ai dati e ad altre risorse digitali.

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

## <a name="namespace-mip-classes"></a>classi MIP dello spazio dei nomi

 Classe                         | Descrizione                                
--------------------------------|---------------------------------------------
[Classe AccessDeniedError](class_mip_accessdeniederror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[Azione della classe](class_mip_action.md)  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
[Classe ActionData](class_mip_actiondata.md)  | Non ancora documentato.
[Classe AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
[Classe AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
[Classe AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Classe di azione che specifica l'aggiunta di una filigrana.
[Classe AddWatermarkActionData](class_mip_addwatermarkactiondata.md)  | Non ancora documentato.
[Classe AdhocProtectionRequiredError](class_mip_adhocprotectionrequirederror.md)  |  È necessario impostare la protezione ad hoc per completare l'azione sul file.
[Classe ApplicationActionState](class_mip_applicationactionstate.md)  | Non ancora documentato.
[Classe ApplyLabelAction](class_mip_applylabelaction.md)  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
[Classe ArgumentData](class_mip_argumentdata.md)  | Non ancora documentato.
[Classe AsyncControl](class_mip_asynccontrol.md)  |  Classe utilizzata per annullare l'operazione asincrona.
[Classe AuthDelegate](class_mip_authdelegate.md)  |  Delegato per le operazioni correlate all'autenticazione.
[Classe BadInputError](class_mip_badinputerror.md)  |  Errore di input non corretto, generato quando l'input per un'API SDK non è valido.
[Classe ClassificationData](class_mip_classificationdata.md)  | Non ancora documentato.
[Classe ClassificationRequest](class_mip_classificationrequest.md)  |  Classe che contiene la richiesta di una chiamata di classificazione sullo stato di esecuzione.
[Classe ClassificationResult](class_mip_classificationresult.md)  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
[Classe ComputeEngine](class_mip_computeengine.md)  | Non ancora documentato.
[Classe ComputeEngineContext](class_mip_computeenginecontext.md)  | Non ancora documentato.
[Classe ConditionData](class_mip_conditiondata.md)  | Non ancora documentato.
[Classe ConsentDelegate](class_mip_consentdelegate.md)  |  Delegato per le operazioni relative al consenso.
[Classe ConsentDeniedError](class_mip_consentdeniederror.md)  |  Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
[Classe ProtectionHandler:: ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  Impostazioni utilizzate per creare un ProtectionHandler per utilizzare il contenuto esistente.
[Classe ContentLabel](class_mip_contentlabel.md)  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
[Classe ContentMarkingActionData](class_mip_contentmarkingactiondata.md)  | Non ancora documentato.
[Classe CustomAction](class_mip_customaction.md)  |  CustomAction è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
[Classe DeprecatedApiError](class_mip_deprecatedapierror.md)  |  Il chiamante ha richiamato un'API deprecata.
[Classe DetailedClassificationResult](class_mip_detailedclassificationresult.md)  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
[Classe DocumentState](class_mip_documentstate.md)  | Non ancora documentato.
[Errore di classe](class_mip_error.md)  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
[Classe ExecutionState](class_mip_executionstate.md)  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
[Classe fileengine](class_mip_fileengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[Classe FileExecutionState](class_mip_fileexecutionstate.md)  | Non ancora documentato.
[Gestore della classe](class_mip_filehandler.md)  |  Interfaccia per tutte le funzioni di gestione file.
[fileinspector della classe](class_mip_fileinspector.md)  | Non ancora documentato.
[Classe FileIOError](class_mip_fileioerror.md)  |  Errore di I/O file.
[Classe fileprofile](class_mip_fileprofile.md)  |  FileProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
[Classe HttpDelegate](class_mip_httpdelegate.md)  |  Interfaccia per l'override della gestione HTTP.
[Classe HttpOperation](class_mip_httpoperation.md)  |  Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
[classe HttpRequest](class_mip_httprequest.md)  |  Interfaccia che descrive una singola richiesta HTTP.
[classe HttpResponse](class_mip_httpresponse.md)  |  Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di HttpDelegate.
[Identità della classe](class_mip_identity.md)  |  Astrazione per Identity.
[Classe InsufficientBufferError](class_mip_insufficientbuffererror.md)  |  Errore buffer insufficiente.
[Classe InternalError](class_mip_internalerror.md)  |  Errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
[Classe JustificationRequiredError](class_mip_justificationrequirederror.md)  | Non ancora documentato.
[Classe JustifyAction](class_mip_justifyaction.md)  |  Justify Action richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
[Etichetta classe](class_mip_label.md)  |  Astrazione per una singola etichetta di Microsoft Information Protection.
[Classe LabelActionData](class_mip_labelactiondata.md)  | Non ancora documentato.
[Classe LabelDisabledError](class_mip_labeldisablederror.md)  |  Label è disabilitato o inattivo.
[Classe LabelGroupData](class_mip_labelgroupdata.md)  | Non ancora documentato.
[Classe LabelingOptions](class_mip_labelingoptions.md)  |  Interfaccia per la configurazione delle opzioni delle etichette per i metodi SetLabel/DeleteLabel.
[Classe LabelNotFoundError](class_mip_labelnotfounderror.md)  |  ID etichetta non riconosciuto.
[Classe LicenseNotRegisteredError](class_mip_licensenotregisterederror.md)  |  La licenza non è registrata.
[Classe LoggerDelegate](class_mip_loggerdelegate.md)  |  Classe che definisce l'interfaccia per il logger MIP SDK.
[Classe MetadataAction](class_mip_metadataaction.md)  |  Classe Action che aggiunge informazioni sui metadati al contenuto.
[Classe MetadataEntry](class_mip_metadataentry.md)  |  Classe di astrazione per la voce di metadati.
[Classe MetadataVersion](class_mip_metadataversion.md)  |  Interfaccia per un MetadataVersion. MetadataVersion determina quali metadati sono attivi e come vengono elaborati.
[Classe MipContext](class_mip_mipcontext.md)  |  MipContext rappresenta lo stato condiviso tra tutti i profili, i motori e i gestori.
[Classe MsgAttachmentData](class_mip_msgattachmentdata.md)  | Non ancora documentato.
[Classe MsgInspector](class_mip_msginspector.md)  | Non ancora documentato.
[Classe NetworkError](class_mip_networkerror.md)  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
[Classe NoAuthTokenError](class_mip_noauthtokenerror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto a causa di un token di autenticazione mancante.
[Classe NoPermissionsError](class_mip_nopermissionserror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[Classe NoPolicyError](class_mip_nopolicyerror.md)  |  I criteri del tenant non sono configurati per la classificazione o le etichette.
[Classe NotSupportedError](class_mip_notsupportederror.md)  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
[Classe AuthDelegate:: OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
[Classe AuthDelegate:: OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  Classe che contiene le informazioni sul token di accesso fornite da un'applicazione.
[Classe FileHandler:: Observer](class_mip_filehandler_observer.md)  |  Interfaccia Observer per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
[Classe ProtectionEngine:: Observer](class_mip_protectionengine_observer.md)  |  Interfaccia che riceve le notifiche correlate a ProtectionEngine.
[Classe fileprofile:: Observer](class_mip_fileprofile_observer.md)  |  Interfaccia Observer per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
[Classe PolicyProfile:: Observer](class_mip_policyprofile_observer.md)  |  Interfaccia Observer per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
[Classe ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md)  |  Interfaccia che riceve le notifiche correlate a ProtectionHandler.
[Classe ProtectionProfile:: Observer](class_mip_protectionprofile_observer.md)  |  Interfaccia che riceve le notifiche correlate a ProtectionProfile.
[Classe OperationCancelledError](class_mip_operationcancellederror.md)  |  Operazione annullata.
[classe PolicyEngine](class_mip_policyengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[Classe PolicyHandler](class_mip_policyhandler.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
[Classe PolicyPackageData](class_mip_policypackagedata.md)  | Non ancora documentato.
[Classe PolicyProfile](class_mip_policyprofile.md)  |  PolicyProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo PolicyProfile, ma se necessario può creare più profili.
[Classe PolicyRuleData](class_mip_policyruledata.md)  | Non ancora documentato.
[Classe PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
[Classe PropertyData](class_mip_propertydata.md)  | Non ancora documentato.
[Classe ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
[Classe ProtectAdhocDkAction](class_mip_protectadhocdkaction.md)  |  Classe di azione che specifica l'aggiunta della protezione con chiave doppia ad hoc al documento.
[Classe ProtectByEncryptOnlyAction](class_mip_protectbyencryptonlyaction.md)  |  Classe di azione che specifica l'aggiunta della protezione solo crittografia al documento.
[Classe ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
[Classe ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
[Classe ProtectDoNotForwardDkAction](class_mip_protectdonotforwarddkaction.md)  |  Classe di azione che specifica l'aggiunta della protezione con chiave doppia al documento.
[Classe ProtectionActionData](class_mip_protectionactiondata.md)  | Non ancora documentato.
[Classe ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Descrizione della protezione associata a una parte del contenuto.
[Classe ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Costruisce un ProtectionDescriptor che descrive la protezione associata a una parte del contenuto.
[Classe ProtectionEngine](class_mip_protectionengine.md)  |  Gestisce azioni correlate alla protezione relative a un'identità specifica.
[Classe ProtectionHandler](class_mip_protectionhandler.md)  |  Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
[Classe ProtectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile è la classe radice per l'esecuzione di operazioni di protezione.
[Classe ProtectionSettings](class_mip_protectionsettings.md)  |  Interfaccia per la configurazione delle opzioni di protezione dati per il metodo selabel.
[Classe ProxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  Errore di autenticazione del proxy.
[Classe PublishingLicenseInfo](class_mip_publishinglicenseinfo.md)  |  Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
[Classe ProtectionHandler::P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  Impostazioni usate per creare un ProtectionHandler per proteggere il nuovo contenuto.
[Classe RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
[Classe RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
[Classe RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
[Classe RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Classe di azione che specifica la rimozione della protezione dal documento.
[Classe RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Classe di azione che specifica la rimozione della filigrana dal documento.
[Classe RulePackageData](class_mip_rulepackagedata.md)  | Non ancora documentato.
[Classe SensitiveTypeClassificationData](class_mip_sensitivetypeclassificationdata.md)  | Non ancora documentato.
[Classe SensitivityConditionData](class_mip_sensitivityconditiondata.md)  | Non ancora documentato.
[Classe SensitivityTypesRulePackage](class_mip_sensitivitytypesrulepackage.md)  | Non ancora documentato.
[Classe ServiceDisabledError](class_mip_servicedisablederror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione di un servizio.
[Classe fileengine:: Settings](class_mip_fileengine_settings.md)  | Non ancora documentato.
[classe PolicyEngine:: Settings](class_mip_policyengine_settings.md)  |  Definisce le impostazioni associate a un oggetto PolicyEngine.
[Classe PolicyProfile:: Settings](class_mip_policyprofile_settings.md)  |  Oggetto Settings usato da PolicyProfile durante la creazione e per tutta la sua durata.
[Classe ProtectionProfile:: Settings](class_mip_protectionprofile_settings.md)  |  Oggetto Settings usato da ProtectionProfile durante la creazione e per tutta la sua durata.
[Classe fileprofile:: Settings](class_mip_fileprofile_settings.md)  |  Oggetto Settings usato da FileProfile durante la creazione e per tutta la sua durata.
[Classe ComputeEngine:: Settings](class_mip_computeengine_settings.md)  | Non ancora documentato.
[Classe ProtectionEngine:: Settings](class_mip_protectionengine_settings.md)  |  Oggetto Settings usato da ProtectionEngine durante la creazione e per tutta la sua durata.
[Flusso di classi](class_mip_stream.md)  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
[Classe SyncFileBaseData](class_mip_syncfilebasedata.md)  | Non ancora documentato.
[Classe SyncFilePolicyData](class_mip_syncfilepolicydata.md)  | Non ancora documentato.
[Classe SyncFileSensitivityData](class_mip_syncfilesensitivitydata.md)  | Non ancora documentato.
[Classe TaskDispatcherDelegate](class_mip_taskdispatcherdelegate.md)  |  Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
[Classe TemplateDescriptor](class_mip_templatedescriptor.md)  | Non ancora documentato.
[Classe TemplateNotFoundError](class_mip_templatenotfounderror.md)  |  ID modello non riconosciuto dal servizio RMS.
[Classe UserRights](class_mip_userrights.md)  |  Gruppo di utenti e diritti ad essi associati.
[Classe UserRoles](class_mip_userroles.md)  |  Un gruppo di utenti e i ruoli ad essi associati.