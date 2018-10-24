---
title: Informazioni di riferimento su MIP SDK per C++ (anteprima)
description: Informazioni di riferimento su MIP SDK per C++ (anteprima)
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06d8bb26a8e3026562006d68d4ae8d1630eba81c
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446329"
---
# <a name="mip-sdk-for-c-preview-reference"></a>Informazioni di riferimento su MIP SDK per C++ (anteprima)

Microsoft Information Protection (MIP) SDK per C++ (anteprima) consente agli sviluppatori di gestire e applicare criteri di protezione dei dati a dati e altre risorse digitali.  

Per altre informazioni, vedere il [blog degli sviluppatori di MIP](https://aka.ms/MIPDevelopers)<!-- and [MIP samples](https://aka.ms/mipsdksamples)-->.

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

| Nome classe | Descrizione |
| :----------|:------------|
[AccessDeniedError](class_mip_accessdeniederror.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[Azione](class_mip_action.md)  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
[AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
[AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
[AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Classe di azione che specifica l'aggiunta di una filigrana.
[ApplyLabelAction](class_mip_applylabelaction.md)  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
[BadInputError](class_mip_badinputerror.md)  |  Errore di input non corretto, generato quando l'input per un'API SDK non è valido.
[ClassificationResult](class_mip_classificationresult.md)  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
[ConsentDelegate](class_consentdelegate.md)  |  Delegato per le operazioni relative al consenso.
[ConsentDeniedError](class_mip_consentdeniederror.md)  |  Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
[ContentLabel](class_mip_contentlabel.md)  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
[CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
[Erroree](class_mip_error.md)  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
[ExecutionState](class_mip_executionstate.md)  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
[FileEngine::Settings](class_mip_fileengine_settings.md)  | _Non ancora documentato._
[FileEngine](class_mip_fileengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[FileHandler::Observer](class_mip_filehandler_observer.md)  |  Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
[FileHandler](class_mip_filehandler.md)  |  Interfaccia per tutte le funzioni di gestione file.
[FileIOError](class_mip_fileioerror.md)  |  Errore di I/O file.
[FileProfile::Observer](class_mip_fileprofile_observer.md)  |  Interfaccia [Observer](class_mip_fileprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
[FileProfile::Settings](class_mip_fileprofile_settings.md)  |  Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
[FileProfile](class_mip_fileprofile.md)  |  [FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
[HttpDelegate](class_mip_httpdelegate.md)  |  Interfaccia per l'override della gestione HTTP.
[HttpRequest](class_mip_httprequest.md)  |  Interfaccia che descrive una singola richiesta HTTP.
[HttpResponse](class_mip_httpresponse.md)  |  Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
[InternalError](class_mip_internalerror.md)  |  Si è verificato un errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
[JustificationRequiredError](class_mip_justificationrequirederror.md)  | _Non ancora documentato._
[JustifyAction](class_mip_justifyaction.md)  |  Justify [Action](class_mip_action.md) richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
[Label](class_mip_label.md)  |  Astrazione per una singola etichetta di Microsoft Information Protection.
[LabelingOptions](class_mip_labelingoptions.md)  |  Interfaccia per la configurazione delle opzioni delle etichette per i metodi SetLabel/DeleteLabel.
[LoggerDelegate](class_mip_loggerdelegate.md)  |  Classe che definisce l'interfaccia per il logger MIP SDK.
[MetadataAction](class_mip_metadataaction.md)  |  Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
[NetworkError](class_mip_networkerror.md)  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
[NotSupportedError](class_mip_notsupportederror.md)  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
[PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  Definisce le impostazioni associate a un oggetto [PolicyEngine](class_mip_policyengine.md).
[PolicyEngine](class_mip_policyengine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[PolicyHandler](class_mip_policyhandler.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
[PolicyProfile::Observer](class_mip_policyprofile_observer.md)  |  Interfaccia [Observer](class_mip_policyprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
[PolicyProfile::Settings](class_mip_policyprofile_settings.md)  |  Oggetto [Settings](class_mip_policyprofile_settings.md) usato da [PolicyProfile](class_mip_policyprofile.md) durante la creazione e per tutta la sua durata.
[PolicyProfile](class_mip_policyprofile.md)  |  [PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
[PolicySyncError](class_mip_policysyncerror.md)  |  Tentativo di sincronizzare i dati dei criteri non riuscito.
[PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
[ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
[ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
[ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
[ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Descrizione della protezione associata a una parte del contenuto.
[ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
[ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  Oggetto [Settings](class_mip_protectionengine_settings.md) usato da [ProtectionEngine](class_mip_protectionengine.md) durante la creazione e per tutta la sua durata.
[ProtectionEngine](class_mip_protectionengine.md)  |  Gestisce azioni correlate alla protezione relative a un'identità specifica.
[ProtectionHandler::Observer](class_mip_protectionhandler.md)  |  Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
[ProtectionHandler](class_mip_protectionhandler.md)  |  Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante la creazione e per tutta la sua durata.
[ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
[RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
[RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
[RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Classe di azione che specifica la rimozione della protezione dal documento.
[RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Classe di azione che specifica la rimozione della filigrana dal documento.
[Stream](class_mip_stream.md)  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
[TransientNetworkError](class_mip_transientnetworkerror.md)  |  Errore di rete temporaneo. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio. È possibile ripetere l'operazione dal momento che l'errore è temporaneo.
[UserRights](class_mip_userrights.md)  |  Gruppo di utenti e diritti ad essi associati.
[UserRoles](class_mip_userroles.md)  |  Gruppo di utenti e ruoli ad essi associati.
