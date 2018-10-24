---
title: Classe mip ProtectionEngine
description: Riferimento per la classe mip ProtectionEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ddc8cfd58acb2a80d024978084b625f3d3728c87
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446737"
---
# <a name="class-mipprotectionengine"></a>Classe mip::ProtectionEngine 
Gestisce azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public std::vector<std::string> GetTemplates(const std::shared_ptr<void>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public void GetRightsForLabelIdAsync(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.
public std::vector<std::string> GetRightsForLabelId(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<void>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un labelId.
public void GetGrantingLabelIdsAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Ottiene la raccolta di ID etichetta disponibili per un utente.
public std::vector<std::string> GetGrantingLabelIds(const std::shared_ptr<void>& context)  |  Ottiene la raccolta di ID etichetta disponibili per un utente.
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromDescriptor(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicense(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata.
public void CreateProtectionHandlerFromPublishingLicenseContextAsync(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione da un contesto di licenza di pubblicazione.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicenseContext(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crea un gestore di protezione da un contesto di licenza di pubblicazione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni del motore.

  
**Restituisce**: impostazioni del motore
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **observer**: classe che implementa l'interfaccia [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer e all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo


  
### <a name="gettemplates"></a>GetTemplates
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **context**: contesto client che verrà passato in maniera opaca all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: elenco di ID modello
  
### <a name="getrightsforlabelidasync"></a>GetRightsForLabelIdAsync
Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **labelId**: ID [etichetta](class_mip_label.md) associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **observer**: classe che implementa l'interfaccia [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: questo stesso contesto verrà inoltrato a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)


  
### <a name="getrightsforlabelid"></a>GetRightsForLabelId
Ottiene la raccolta di diritti disponibili per un utente per un labelId.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **labelId**: ID [etichetta](class_mip_label.md) associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **context**: questo stesso contesto verrà inoltrato all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: elenco di diritti
  
### <a name="getgrantinglabelidsasync"></a>GetGrantingLabelIdsAsync
Ottiene la raccolta di ID etichetta disponibili per un utente.

Parametri:  
* **observer**: classe che implementa l'interfaccia [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: questo stesso contesto verrà inoltrato a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o ProtectionEngine::Observer::OnGrantingLabelIdsFailure


  
### <a name="getgrantinglabelids"></a>GetGrantingLabelIds
Ottiene la raccolta di ID etichetta disponibili per un utente.

Parametri:  
* **context**: questo stesso contesto verrà inoltrato all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: elenco di ID etichetta
  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **descriptor**: [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer e all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo


  
### <a name="protectionhandler"></a>ProtectionHandler
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **descriptor**: [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **options**: opzioni di creazione 


* **context**: contesto client che verrà nuovamente passato in maniera opaca all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
Crea un gestore di protezione da una licenza di pubblicazione serializzata.

Parametri:  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer e all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo


  
### <a name="protectionhandler"></a>ProtectionHandler
Crea un gestore di protezione da una licenza di pubblicazione serializzata.

Parametri:  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: contesto client che verrà nuovamente passato in maniera opaca all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync
Crea un gestore di protezione da un contesto di licenza di pubblicazione.

Parametri:  
* **publishingLicenseContext**: modulo pre-elaborato della licenza di pubblicazione serializzata 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer e all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo


  
### <a name="protectionhandler"></a>ProtectionHandler
Crea un gestore di protezione da un contesto di licenza di pubblicazione.

Parametri:  
* **publishingLicenseContext**: modulo pre-elaborato della licenza di pubblicazione serializzata 


* **options**: opzioni di creazione 


* **observer**: classe che implementa l'interfaccia [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context**: contesto client che verrà nuovamente passato in maniera opaca all'oggetto [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)