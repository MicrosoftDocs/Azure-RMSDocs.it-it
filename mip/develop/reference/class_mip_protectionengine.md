---
title: Classe mip::ProtectionEngine
description: Documenta la classe mip::protectionengine di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 60a61f5e06b5e76cbf0c557e7d489a8d618a8261
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574152"
---
# <a name="class-mipprotectionengine"></a>Classe mip::ProtectionEngine 
Gestisce azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public void GetTemplatesAsync (const std:: shared_ptr\<ProtectionEngine::Observer\>& observer, const std:: shared_ptr\<void\>& contesto)  |  Ottiene la raccolta di modelli disponibili per un utente.
public std::vector\<std::string\> GetTemplates(const std::shared_ptr\<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public void GetRightsForLabelIdAsync (const std:: String & documentId, const std:: String & ID etichetta, const std:: String & ownerEmail, const std:: shared_ptr\<ProtectionEngine::Observer\>& observer, const std: : shared_ptr\<void\>& contesto)  |  Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.
Public std:: Vector\<std:: String\> GetRightsForLabelId (const std:: String & documentId, const std:: String & ID etichetta, const std:: String & ownerEmail, const std:: shared_ptr\<void\> & contesto)  |  Ottiene la raccolta di diritti disponibili per un utente per un labelId.
public void CreateProtectionHandlerFromDescriptorAsync (const std:: shared_ptr\<ProtectionDescriptor\>& descrittore, ProtectionHandlerCreationOptions const & opzioni, const std:: shared_ptr\< ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std:: shared_ptr\<ProtectionDescriptor\>& descrittore, ProtectionHandlerCreationOptions const & opzioni, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public void CreateProtectionHandlerFromPublishingLicenseAsync (const std:: Vector\<uint8_t\>& serializedPublishingLicense, ProtectionHandlerCreationOptions const & opzioni, const std:: shared_ptr\<ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std:: Vector\<uint8_t\>& serializedPublishingLicense, const ProtectionHandlerCreationOptions & opzioni, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata.
public void CreateProtectionHandlerFromProtectionInfoAsync (const std:: Vector\<uint8_t\>& serializedPublishingLicense, const std:: Vector\<uint8_t\>& serializedProtectionInfo, const std:: shared_ptr\<ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata e informazioni di protezione serializzato.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromProtectionInfo (const std:: Vector\<uint8_t\>& serializedPublishingLicense, const std:: Vector\< uint8_t\>& serializedProtectionInfo, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata e informazioni di protezione serializzato.
public void CreateProtectionHandlerFromPublishingLicenseContextAsync (const PublishingLicenseContext & publishingLicenseContext, ProtectionHandlerCreationOptions const & opzioni, const std:: shared_ptr\< ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione da un contesto di licenza di pubblicazione.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicenseContext (PublishingLicenseContext const & publishingLicenseContext, ProtectionHandlerCreationOptions const & opzioni, const std:: shared_ptr\<void\>& contesto)  |  Crea un gestore di protezione da un contesto di licenza di pubblicazione.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni del motore.

  
**Restituisce**: Impostazioni del motore
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync (funzione)
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **observer**: Una classe che implementa il [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato all'Observer in modo non trasparente e facoltativi [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="gettemplates-function"></a>Funzione GetTemplates
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **context**: Contesto di client che verrà in maniera opaca passato come facoltativa [HttpDelegate](class_mip_httpdelegate.md)



  
**Restituisce**: Elenco di ID di modello
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.

Parametri:  
* **documentId**: ID del documento associati i metadati del documento 


* **labelId**: [Etichetta](class_mip_label.md) ID associato con i metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **observer**: Una classe che implementa il [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) interfaccia 


* **context**: Questo stesso contesto verrà inoltrato al [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un labelId.

Parametri:  
* **documentId**: ID del documento associati i metadati del documento 


* **labelId**: [Etichetta](class_mip_label.md) ID associato con i metadati del documento con cui è stato creato il documento 


* **ownerEmail**: Proprietario del documento 


* **context**: Questo stesso contesto verrà inoltrato come facoltativa [HttpDelegate](class_mip_httpdelegate.md)



  
**Restituisce**: Elenco di diritti
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **descrittore**: Oggetto [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **opzioni**: Opzioni di creazione 


* **observer**: Una classe che implementa il [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato all'Observer in modo non trasparente e facoltativi [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **descrittore**: Oggetto [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **opzioni**: Opzioni di creazione 


* **context**: Contesto di client che verrà passato in modo non trasparente a facoltativo [HttpDelegate](class_mip_httpdelegate.md)



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync (funzione)
Crea un gestore di protezione da una licenza di pubblicazione serializzata.

Parametri:  
* **serializedPublishingLicense**: Una licenza di pubblicazione serializzata 


* **opzioni**: Opzioni di creazione 


* **observer**: Una classe che implementa il [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato all'Observer in modo non trasparente e facoltativi [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense (funzione)
Crea un gestore di protezione da una licenza di pubblicazione serializzata.

Parametri:  
* **serializedPublishingLicense**: Una licenza di pubblicazione serializzata 


* **opzioni**: Opzioni di creazione 


* **observer**: Una classe che implementa il [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato in modo non trasparente a facoltativo [HttpDelegate](class_mip_httpdelegate.md)



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfromprotectioninfoasync-function"></a>CreateProtectionHandlerFromProtectionInfoAsync (funzione)
Crea un gestore di protezione da una licenza di pubblicazione serializzata e informazioni di protezione serializzato.

Parametri:  
* **serializedPublishingLicense**: Una licenza di pubblicazione serializzata 


* **serializedProtectionInfo**: Informazioni di protezione serializzato 


* **observer**: Una classe che implementa il [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato in maniera opaca all'Observer


  
### <a name="createprotectionhandlerfromprotectioninfo-function"></a>CreateProtectionHandlerFromProtectionInfo (funzione)
Crea un gestore di protezione da una licenza di pubblicazione serializzata e informazioni di protezione serializzato.

Parametri:  
* **serializedPublishingLicense**: Una licenza di pubblicazione serializzata 


* **serializedProtectionInfo**: Informazioni di protezione serializzato 


* **context**: Contesto di client che verrà passato in maniera opaca all'Observer



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync-function"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync (funzione)
Crea un gestore di protezione da un contesto di licenza di pubblicazione.

Parametri:  
* **publishingLicenseContext**: Un modulo di pre-elaborato della licenza di pubblicazione serializzato 


* **opzioni**: Opzioni di creazione 


* **observer**: Una classe che implementa il [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato all'Observer in modo non trasparente e facoltativi [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicensecontext-function"></a>CreateProtectionHandlerFromPublishingLicenseContext (funzione)
Crea un gestore di protezione da un contesto di licenza di pubblicazione.

Parametri:  
* **publishingLicenseContext**: Un modulo di pre-elaborato della licenza di pubblicazione serializzato 


* **opzioni**: Opzioni di creazione 


* **observer**: Una classe che implementa il [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaccia 


* **context**: Contesto di client che verrà passato in modo non trasparente a facoltativo [HttpDelegate](class_mip_httpdelegate.md)



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)