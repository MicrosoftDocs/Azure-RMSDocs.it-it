---
title: Microsoft Information Protection SDK per C++ Reference
description: Microsoft Information Protection SDK per C++ Reference
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 7e041062b92bad8b853bf5bcf55a23c6ad88a4b7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256602"
---
# <a name="mip-sdk-for-c-reference"></a>Microsoft Information Protection SDK per C++ Reference

Microsoft Information Protection (MIP) SDK per C++ consente agli sviluppatori di gestire e applicare i criteri di protezione dei dati ai dati e altre risorse digitali.  

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

| Nome namespace::Class | Descrizione |
| :----------|:------------|
[mip::AccessDeniedError](class_mip_AccessDeniedError.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[mip::Action](class_mip_Action.md)  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
[mip::AddContentFooterAction](class_mip_AddContentFooterAction.md)  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
[mip::AddContentHeaderAction](class_mip_AddContentHeaderAction.md)  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
[mip::AddWatermarkAction](class_mip_AddWatermarkAction.md)  |  Classe di azione che specifica l'aggiunta di una filigrana.
[mip::ApplyLabelAction](class_mip_ApplyLabelAction.md)  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
[mip::AuthDelegate](class_mip_AuthDelegate.md)  |  Delegato per l'autenticazione di operazioni correlate.
[mip::BadInputError](class_mip_BadInputError.md)  |  Errore di input non corretto, generato quando l'input per un'API SDK non è valido.
[mip::ClassificationRequest](class_mip_ClassificationRequest.md)  |  Classe che contiene la richiesta di una chiamata di classificazione dello stato di esecuzione.
[mip::ClassificationResult](class_mip_ClassificationResult.md)  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
[mip::ConsentDelegate](class_mip_ConsentDelegate.md)  |  Delegato per le operazioni relative al consenso.
[mip::ConsentDeniedError](class_mip_ConsentDeniedError.md)  |  Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
[mip::ContentLabel](class_mip_ContentLabel.md)  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
[mip::CustomAction](class_mip_CustomAction.md)  |  [CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
[mip::Error](class_mip_Error.md)  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
[mip::ExecutionState](class_mip_ExecutionState.md)  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
[mip::FileEngine](class_mip_FileEngine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[mip::FileExecutionState](class_mip_FileExecutionState.md)  | _Non ancora documentato._
[mip::FileHandler](class_mip_FileHandler.md)  |  Interfaccia per tutte le funzioni di gestione file.
[mip::FileIOError](class_mip_FileIOError.md)  |  Errore di I/O file.
[mip::FileProfile](class_mip_FileProfile.md)  |  [FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
[mip::HttpDelegate](class_mip_HttpDelegate.md)  |  Interfaccia per l'override della gestione HTTP.
[mip::HttpRequest](class_mip_HttpRequest.md)  |  Interfaccia che descrive una singola richiesta HTTP.
[mip::HttpResponse](class_mip_HttpResponse.md)  |  Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
[mip::Identity](class_mip_Identity.md)  |  Astrazione per l'identità.
[mip::InternalError](class_mip_InternalError.md)  |  Errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
[mip::JustificationRequiredError](class_mip_JustificationRequiredError.md)  | _Non ancora documentato._
[mip::JustifyAction](class_mip_JustifyAction.md)  |  Justify [Action](class_mip_action.md) richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
[mip::Label](class_mip_Label.md)  |  Astrazione per una singola etichetta di Microsoft Information Protection.
[mip::LabelingOptions](class_mip_LabelingOptions.md)  |  Interfaccia per la configurazione delle opzioni delle etichette per i metodi SetLabel/DeleteLabel.
[mip::LoggerDelegate](class_mip_LoggerDelegate.md)  |  Classe che definisce l'interfaccia per il logger MIP SDK.
[mip::MetadataAction](class_mip_MetadataAction.md)  |  Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
[mip::NetworkError](class_mip_NetworkError.md)  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
[mip::NoAuthTokenError](class_mip_NoAuthTokenError.md)  |  L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un token di autenticazione mancante.
[mip::NoPermissionsError](class_mip_NoPermissionsError.md)  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
[mip::NoPolicyError](class_mip_NoPolicyError.md)  |  Criteri del tenant non sono configurato per le etichette di classificazione /.
[mip::NotSupportedError](class_mip_NotSupportedError.md)  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
[mip::PolicyEngine](class_mip_PolicyEngine.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
[mip::PolicyHandler](class_mip_PolicyHandler.md)  |  Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
[mip::PolicyProfile](class_mip_PolicyProfile.md)  |  [PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
[mip::PolicySyncError](class_mip_PolicySyncError.md)  |  Tentativo di sincronizzare i dati dei criteri non riuscito.
[mip::PrivilegedRequiredError](class_mip_PrivilegedRequiredError.md)  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
[mip::ProtectAdhocAction](class_mip_ProtectAdhocAction.md)  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
[mip::ProtectByTemplateAction](class_mip_ProtectByTemplateAction.md)  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
[mip::ProtectDoNotForwardAction](class_mip_ProtectDoNotForwardAction.md)  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
[mip::ProtectionDescriptor](class_mip_ProtectionDescriptor.md)  |  Descrizione della protezione associata a una parte del contenuto.
[mip::ProtectionDescriptorBuilder](class_mip_ProtectionDescriptorBuilder.md)  |  Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
[mip::ProtectionEngine](class_mip_ProtectionEngine.md)  |  Gestisce azioni correlate alla protezione relative a un'identità specifica.
[mip::ProtectionHandler](class_mip_ProtectionHandler.md)  |  Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
[mip::ProtectionProfile](class_mip_ProtectionProfile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
[mip::ProxyAuthenticationError](class_mip_ProxyAuthenticationError.md)  |  Errore di autenticazione proxy.
[mip::RecommendLabelAction](class_mip_RecommendLabelAction.md)  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
[mip::RemoveContentFooterAction](class_mip_RemoveContentFooterAction.md)  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
[mip::RemoveContentHeaderAction](class_mip_RemoveContentHeaderAction.md)  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
[mip::RemoveProtectionAction](class_mip_RemoveProtectionAction.md)  |  Classe di azione che specifica la rimozione della protezione dal documento.
[mip::RemoveWatermarkAction](class_mip_RemoveWatermarkAction.md)  |  Classe di azione che specifica la rimozione della filigrana dal documento.
[mip::SensitivityTypesRulePackage](class_mip_SensitivityTypesRulePackage.md)  | _Non ancora documentato._
[mip::ServiceDisabledError](class_mip_ServiceDisabledError.md)  |  L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un servizio viene disabilitato.
[mip::Stream](class_mip_Stream.md)  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
[mip::TransientNetworkError](class_mip_TransientNetworkError.md)  |  Errore di rete temporaneo. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio. È possibile ripetere l'operazione dal momento che l'errore è temporaneo.
[mip::UserRights](class_mip_UserRights.md)  |  Gruppo di utenti e diritti ad essi associati.
[mip::UserRoles](class_mip_UserRoles.md)  |  Gruppo di utenti e ruoli ad essi associati.
