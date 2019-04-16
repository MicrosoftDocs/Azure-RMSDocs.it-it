---
title: Microsoft Information Protection SDK per C++ Reference
description: Microsoft Information Protection SDK per C++ Reference
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1db2faeca6c2ff00a0053a7d65d16872190d306f
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574058"
---
# <a name="mip-sdk-for-c-reference"></a>Microsoft Information Protection SDK per C++ Reference

Microsoft Information Protection (MIP) SDK per C++ consente agli sviluppatori di gestire e applicare i criteri di protezione dei dati ai dati e altre risorse digitali.

MIP SDK per C++ include:

- [Enumerazioni e strutture](mip-enums-and-structs.md)
- [Funzioni](mip-functions.md)
- Le classi seguenti:

 Classe                         | Descrizione                                
--------------------------------|---------------------------------------------
Classe mip::AccessDeniedError  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
Classe mip::Action  |  Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
Classe mip::AddContentFooterAction  |  Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
Classe mip::AddContentHeaderAction  |  Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
Classe mip::AddWatermarkAction  |  Classe di azione che specifica l'aggiunta di una filigrana.
classe mip::AdhocProtectionRequiredError  |  Protezione ad hoc deve essere impostata per completare l'azione sul file.
Classe mip::ApplyLabelAction  |  Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
classe mip::AuthDelegate  |  Delegato per l'autenticazione di operazioni correlate.
classe mip::AuthDelegate::OAuth2Challenge  |  una classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token oauth2.
classe mip::AuthDelegate::OAuth2Token  |  Una classe che definisce come Microsoft Information Protection SDK prevede che il token oauth2 da passare nuovamente nel SDK.
Classe mip::BadInputError  |  Errore di input non corretto, generato quando l'input per un'API SDK non è valido.
classe mip::ClassificationRequest  |  Classe che contiene la richiesta di una chiamata di classificazione dello stato di esecuzione.
Classe mip::ClassificationResult  |  Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
classe mip::ConsentDelegate  |  Delegato per le operazioni relative al consenso.
Classe mip::ConsentDeniedError  |  Non è stato concesso il consenso per un'operazione che ha richiesto il consenso dell'utente.
Classe mip::ContentLabel  |  Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Classe mip::CustomAction  |  [CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
Classe mip::Error  |  Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
Classe mip::ExecutionState  |  Interfaccia per tutti gli stati necessari per eseguire il motore.
Classe mip::FileEngine  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
Classe mip::FileEngine::Settings  | _Non ancora documentato._
class mip::FileExecutionState  | _Non ancora documentato._
Classe mip::FileHandler  |  Interfaccia per tutte le funzioni di gestione file.
Classe mip::FileHandler::Observer  |  Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
Classe mip::FileIOError  |  Errore di I/O file.
Classe mip::FileProfile  |  [FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Classe mip::FileProfile::Observer  |  Interfaccia [Observer](class_mip_fileprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Classe mip::FileProfile::Settings  |  Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
Classe mip::HttpDelegate  |  Interfaccia per l'override della gestione HTTP.
classe mip::HttpOperation  |  Interfaccia che descrive una singola operazione HTTP implementata dall'app client quando si esegue l'override [HttpDelegate](class_mip_httpdelegate.md).
Classe mip::HttpRequest  |  Interfaccia che descrive una singola richiesta HTTP.
Classe mip::HttpResponse  |  Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
classe MIP  |  Astrazione per l'identità.
Classe mip::InternalError  |  Si è verificato un errore interno. Questo errore viene generato quando un evento imprevisto si verifica durante l'esecuzione.
Classe mip::JustificationRequiredError  | _Non ancora documentato._
Classe mip::JustifyAction  |  Justify [Action](class_mip_action.md) richiede la giustificazione del downgrade di un'etichetta e l'impostazione della risposta nello stato di esecuzione.
Classe mip::Label  |  Astrazione per una singola etichetta di Microsoft Information Protection.
Classe mip::LabelingOptions  |  Interfaccia per la configurazione delle opzioni delle etichette per i metodi SetLabel/DeleteLabel.
Classe mip::LoggerDelegate  |  Classe che definisce l'interfaccia per il logger MIP SDK.
Classe mip::MetadataAction  |  Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
Classe mip::NetworkError  |  Errore di rete. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio.
classe mip::NoAuthTokenError  |  L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un token di autenticazione mancante.
classe mip::NoPermissionsError  |  L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
classe mip::NoPolicyError  |  Criteri del tenant non sono configurato per le etichette di classificazione /.
Classe mip::NotSupportedError  |  L'operazione richiesta dall'applicazione non è supportata dall'SDK.
classe mip::OperationCancelledError  |  Operazione annullata.
Classe mip::PolicyEngine  |  Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
Classe mip::PolicyEngine::Settings  |  Definisce le impostazioni associate a un oggetto [PolicyEngine](class_mip_policyengine.md).
Classe mip::PolicyHandler  |  Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
Classe mip::PolicyProfile  |  [PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
Classe mip::PolicyProfile::Observer  |  Interfaccia [Observer](class_mip_policyprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Classe mip::PolicyProfile::Settings  |  Oggetto [Settings](class_mip_policyprofile_settings.md) usato da [PolicyProfile](class_mip_policyprofile.md) durante la creazione e per tutta la sua durata.
Classe mip::PolicySyncError  |  Tentativo di sincronizzare i dati dei criteri non riuscito.
Classe mip::PrivilegedRequiredError  |  L'etichetta corrente è stata assegnata come operazione con privilegi (equivalente a un'operazione dell'amministratore), quindi non è possibile eseguirne l'override.
Classe mip::ProtectAdhocAction  |  Classe di azione che specifica l'aggiunta della protezione ad hoc al documento.
Classe mip::ProtectByTemplateAction  |  Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
Classe mip::ProtectDoNotForwardAction  |  Classe di azione che specifica l'aggiunta della protezione Non inoltrare al documento.
Classe mip::ProtectionDescriptor  |  Descrizione della protezione associata a una parte del contenuto.
Classe mip::ProtectionDescriptorBuilder  |  Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
Classe mip::ProtectionEngine  |  Gestisce azioni correlate alla protezione relative a un'identità specifica.
Classe mip::ProtectionEngine::Observer  |  Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
Classe mip::ProtectionEngine::Settings  |  Oggetto [Settings](class_mip_protectionengine_settings.md) usato da [ProtectionEngine](class_mip_protectionengine.md) durante la creazione e per tutta la sua durata.
Classe mip::ProtectionHandler  |  Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
Classe mip::ProtectionHandler::Observer  |  Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
Classe mip::ProtectionProfile  |  [ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
Classe mip::ProtectionProfile::Observer  |  Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
Classe mip::ProtectionProfile::Settings  |  Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante la creazione e per tutta la sua durata.
classe mip::ProxyAuthenticationError  |  Errore di autenticazione proxy.
Classe mip::RecommendLabelAction  |  Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
Classe mip::RemoveContentFooterAction  |  Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
Classe mip::RemoveContentHeaderAction  |  Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
Classe mip::RemoveProtectionAction  |  Classe di azione che specifica la rimozione della protezione dal documento.
Classe mip::RemoveWatermarkAction  |  Classe di azione che specifica la rimozione della filigrana dal documento.
classe mip::SensitivityTypesRulePackage  | _Non ancora documentato._
classe mip::ServiceDisabledError  |  L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un servizio viene disabilitato.
Classe mip::Stream  |  Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
class mip::TaskDispatcherDelegate  |  Una classe che definisce l'interfaccia per il dispatcher attività MIP SDK.
Classe mip::TransientNetworkError  |  Errore di rete temporaneo. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio. È possibile ripetere l'operazione dal momento che l'errore è temporaneo.
Classe mip::UserRights  |  Gruppo di utenti e diritti ad essi associati.
Classe mip::UserRoles  |  Gruppo di utenti e ruoli ad essi associati.