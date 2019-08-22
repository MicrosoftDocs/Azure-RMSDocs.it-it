---
title: SDK MIP per C++ riferimento
description: SDK MIP per C++ riferimento
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2fab85dfd5b5d0d1103f9c3ee4b0d3725a10cb8f
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884825"
---
# <a name="mip-sdk-for-c-reference"></a>SDK MIP per C++ riferimento

Microsoft Information Protection (MIP) SDK per C++ consente agli sviluppatori di gestire e applicare i criteri di protezione dei dati ai dati e ad altre risorse digitali.

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

 Classe                         | Descrizione                                
--------------------------------|---------------------------------------------
Classe mip::AccessDeniedError  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
Classe mip::Action  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
Classe MIP:: ActionData  | _Non ancora documentato._
Classe mip::AddContentFooterAction  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
Classe mip::AddContentHeaderAction  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
Classe mip::AddWatermarkAction  |  Classe di azione che specifica l'aggiunta di una filigrana.
Classe MIP:: AddWatermarkActionData  | _Non ancora documentato._
Classe MIP:: AdhocProtectionRequiredError  |  È necessario impostare la protezione ad hoc per completare l'azione sul file.
Classe MIP:: ApplicationActionState  | _Non ancora documentato._
Classe mip::ApplyLabelAction  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
Classe MIP:: ArgumentData  | _Non ancora documentato._
Classe MIP:: AuthDelegate  |  Delegato per le operazioni correlate all'autenticazione.
Classe mip::BadInputError  |  Errore di input non corretto, generato quando l'input per un'API SDK non è valido.
Classe MIP:: ClassificationData  | _Non ancora documentato._
Classe MIP:: ClassificationRequest  |  Classe che contiene la richiesta di una chiamata di classificazione sullo stato di esecuzione.
Classe mip::ClassificationResult  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
Classe MIP:: ComputeEngine  | _Non ancora documentato._
Classe MIP:: ComputeEngineContext  | _Non ancora documentato._
Classe MIP:: ConditionData  | _Non ancora documentato._
Classe MIP:: ConsentDelegate  |  Delegato per le operazioni relative al consenso.
Classe mip::ConsentDeniedError  |  Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
Classe mip::ContentLabel  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Classe MIP:: ContentMarkingActionData  | _Non ancora documentato._
Classe mip::CustomAction  |  [CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
Classe MIP::D eprecatedApiError  |  Il chiamante ha richiamato un'API deprecata.
Classe MIP::D ocumentState  | _Non ancora documentato._
Classe mip::Error  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
Classe mip::ExecutionState  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
Classe mip::FileEngine  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
Classe MIP:: FileExecutionState  | _Non ancora documentato._
Classe mip::FileHandler  |  Interfaccia per tutte le funzioni di gestione file.
Classe MIP:: fileinspector  | _Non ancora documentato._
Classe mip::FileIOError  |  Errore di I/O file.
Classe mip::FileProfile  |  [FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Classe mip::HttpDelegate  |  Interfaccia per l'override della gestione HTTP.
Classe MIP:: HttpOperation  |  Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di [HttpDelegate](class_mip_httpdelegate.md).
Classe mip::HttpRequest  |  Interfaccia che descrive una singola richiesta HTTP.
Classe mip::HttpResponse  |  Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
Classe MIP:: Identity  |  Astrazione per Identity.
Classe mip::InternalError  |  Si è verificato un errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
Classe mip::JustificationRequiredError  | _Non ancora documentato._
Classe mip::JustifyAction  |  Justify [Action](class_mip_action.md) richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
Classe mip::Label  |  Astrazione per una singola etichetta di Microsoft Information Protection.
Classe MIP:: LabelActionData  | _Non ancora documentato._
Classe MIP:: LabelDisabledError  |  [Label](class_mip_label.md) è disabilitato o inattivo.
Classe MIP:: LabelGroupData  | _Non ancora documentato._
Classe mip::LabelingOptions  |  Interfaccia per la configurazione delle opzioni delle etichette per i metodi SetLabel/DeleteLabel.
Classe MIP:: LabelNotFoundError  |  [Etichetta](class_mip_label.md) di ID non riconosciuto.
Classe mip::LoggerDelegate  |  Classe che definisce l'interfaccia per il logger MIP SDK.
Classe mip::MetadataAction  |  Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
Classe MIP:: MipContext  | MipContext rappresenta lo stato condiviso tra tutti i profili, i motori e i gestori.
Classe MIP:: MsgAttachmentData  | _Non ancora documentato._
Classe MIP:: MsgInspector  | _Non ancora documentato._
Classe mip::NetworkError  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
Classe MIP:: NoAuthTokenError  |  L'utente non è riuscito a ottenere l'accesso al contenuto a causa di un token di autenticazione mancante.
Classe MIP:: NoPermissionsError  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
Classe MIP:: NoPolicyError  |  I criteri del tenant non sono configurati per la classificazione o le etichette.
Classe mip::NotSupportedError  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
Classe MIP:: OperationCancelledError  |  Operazione annullata.
Classe mip::PolicyEngine  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
Classe mip::PolicyHandler  |  Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
Classe MIP::P olicyPackageData  | _Non ancora documentato._
Classe mip::PolicyProfile  |  [PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
Classe MIP::P olicyRuleData  | _Non ancora documentato._
Classe mip::PolicySyncError  |  Tentativo di sincronizzare i dati dei criteri non riuscito.
Classe mip::PrivilegedRequiredError  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
Classe MIP::P ropertyData  | _Non ancora documentato._
Classe mip::ProtectAdhocAction  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
Classe mip::ProtectByTemplateAction  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
Classe mip::ProtectDoNotForwardAction  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
Classe MIP::P rotectionActionData  | _Non ancora documentato._
Classe mip::ProtectionDescriptor  |  Descrizione della protezione associata a una parte del contenuto.
Classe mip::ProtectionDescriptorBuilder  |  Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
Classe mip::ProtectionEngine  |  Gestisce azioni correlate alla protezione relative a un'identità specifica.
Classe mip::ProtectionHandler  |  Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
Classe mip::ProtectionProfile  |  [ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
Classe MIP::P rotectionSettings  |  Interfaccia per la configurazione delle opzioni di protezione dati per il metodo selabel.
Classe MIP::P roxyAuthenticationError  |  Errore di autenticazione del proxy.
Classe MIP::P ublishingLicenseInfo  |  Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
Classe mip::RecommendLabelAction  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
Classe mip::RemoveContentFooterAction  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
Classe mip::RemoveContentHeaderAction  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
Classe mip::RemoveProtectionAction  |  Classe di azione che specifica la rimozione della protezione dal documento.
Classe mip::RemoveWatermarkAction  |  Classe di azione che specifica la rimozione della filigrana dal documento.
Classe MIP:: RulePackageData  | _Non ancora documentato._
Classe MIP:: SensitivityConditionData  | _Non ancora documentato._
Classe MIP:: SensitivityTypesRulePackage  | _Non ancora documentato._
Classe MIP:: ServiceDisabledError  |  L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione di un servizio.
Classe mip::Stream  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
Classe MIP:: SyncFileBaseData  | _Non ancora documentato._
Classe MIP:: SyncFilePolicyData  | _Non ancora documentato._
Classe MIP:: SyncFileSensitivityData  | _Non ancora documentato._
Classe MIP:: TaskDispatcherDelegate  |  Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
Classe MIP:: TemplateNotFoundError  |  ID modello non riconosciuto dal servizio RMS.
Classe mip::TransientNetworkError  |  Errore di rete temporaneo. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio. È possibile ripetere l'operazione dal momento che l'errore è temporaneo.
Classe mip::UserRights  |  Gruppo di utenti e diritti ad essi associati.
Classe mip::UserRoles  |  Gruppo di utenti e ruoli ad essi associati.
