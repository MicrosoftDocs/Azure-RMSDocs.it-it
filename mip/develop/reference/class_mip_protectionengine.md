---
title: Classe mip::ProtectionEngine
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 88cb6565e8e392a83d01ded79186cf7dbb6fb43c
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883514"
---
# <a name="class-mipprotectionengine"></a>Classe mip::ProtectionEngine 
Gestisce azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public void GetTemplatesAsync (const std::\<shared_ptr ProtectionEngine::\>Observer & Observer, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public std:: Vector\<std:: String\> gettemplates (const std::\<shared_ptr\>void & context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public void GetRightsForLabelIdAsync (const std:: String & documentId, const std:: String & LabelId, const std:: String & owneremail, const std:: String & delegatedUserEmail, const std:: shared_ptr\<ProtectionEngine:: O bserver\>& Observer, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.
public std:: Vector\<std:: String\> GetRightsForLabelId (const std:: String & documentId, const std:: String & LabelId, const std:: String & owneremail, const std:: String & delegatedUserEmail, const std:: Shared PTR\<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un labelId.
public void CreateProtectionHandlerFromDescriptorAsync (const std::\<shared_ptr\>ProtectionDescriptor & descriptor, const ProtectionHandlerCreationOptions & Options, const std\< :: shared_ptr ProtectionHandler:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std::\<shared_ptr\>ProtectionDescriptor & descrittore, const ProtectionHandlerCreationOptions opzioni di &, const std:\<:\>shared_ptr void & context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public void CreateProtectionHandlerFromPublishingLicenseAsync (const std::\<vector\>uint8_t & serializedPublishingLicense, const ProtectionHandlerCreationOptions & Options, const std:: shared_ptr\<ProtectionHandler:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std::\<vector\>uint8_t & serializedPublishingLicense, const ProtectionHandlerCreationOptions & Options, const std::\<shared_ptr\>void & context)  |  Crea un gestore di protezione da una licenza di pubblicazione serializzata.
public void CreateProtectionHandlerForPublishingAsync (const ProtectionHandler::P ublishingsettings & Settings, const std:\<: shared_ptr ProtectionHandler::\>Observer & Observer, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler::P ublishingsettings & Settings, const std:\<:\>shared_ptr void & context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public void CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & Settings, const std:\<: shared_ptr ProtectionHandler::\>Observer & Observer, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler:: ConsumptionSettings & Settings, const std:\<:\>shared_ptr void & Context )  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni del motore.

  
**Restituisce**: Impostazioni motore
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync (funzione)
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **observer**: Classe che implementa l'interfaccia [ProtectionEngine:: Observer](class_mip_protectionengine_observer.md) 


* **context**: Contesto client che verrà passato in modo opaco agli osservatori e [HttpDelegate](class_mip_httpdelegate.md) facoltativi


  
### <a name="gettemplates-function"></a>Funzione gettemplates
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **context**: Contesto client che verrà passato in modo opaco a [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: Elenco di ID modello
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **labelId**: [Etichetta](class_mip_label.md) di ID associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **observer**: Classe che implementa l'interfaccia [ProtectionEngine:: Observer](class_mip_protectionengine_observer.md) 


* **context**: Lo stesso contesto verrà inviato a [ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un labelId.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **labelId**: [Etichetta](class_mip_label.md) di ID associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: Proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **context**: Lo stesso contesto verrà inviato a [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: Elenco dei diritti
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* descrittore: Un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **Opzioni**: Opzioni di creazione 


* **observer**: Classe che implementa l'interfaccia [ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md) 


* **context**: Contesto client che verrà passato in modo opaco agli osservatori e [HttpDelegate](class_mip_httpdelegate.md) facoltativi


> Deprecato Questo metodo sarà presto deprecato a favore di CreateProtectionHandlerForPublishingAsync
  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* descrittore: Un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la configurazione di protezione 


* **Opzioni**: Opzioni di creazione 


* **context**: Contesto client che verrà passato in modo opaco a [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
> Deprecato Questo metodo sarà presto deprecato a favore di CreateProtectionHandlerForPublishingAsync
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync (funzione)
Crea un gestore di protezione da una licenza di pubblicazione serializzata.

Parametri:  
* **serializedPublishingLicense**: Una licenza di pubblicazione serializzata 


* **Opzioni**: Opzioni di creazione 


* **observer**: Classe che implementa l'interfaccia [ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md) 


* **context**: Contesto client che verrà passato in modo opaco agli osservatori e [HttpDelegate](class_mip_httpdelegate.md) facoltativi


> Deprecato Questo metodo sarà presto deprecato a favore di CreateProtectionHandlerForConsumptionAsync
  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense (funzione)
Crea un gestore di protezione da una licenza di pubblicazione serializzata.

Parametri:  
* **serializedPublishingLicense**: Una licenza di pubblicazione serializzata 


* **Opzioni**: Opzioni di creazione 


* **observer**: Classe che implementa l'interfaccia [ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md) 


* **context**: Contesto client che verrà passato in modo opaco a [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
> Deprecato Questo metodo sarà presto deprecato a favore di CreateProtectionHandlerForConsumption
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: Impostazioni di protezione 


* **observer**: Classe che implementa l'interfaccia [ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md) 


* **context**: Contesto client che verrà inviato in modo opaco agli osservatori e [HttpDelegate](class_mip_httpdelegate.md) facoltativi


  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: Impostazioni di protezione 


* **context**: Contesto client che verrà trasmesso in modo opaco a [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: Impostazioni di protezione 


* **observer**: Classe che implementa l'interfaccia [ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md) 


* **context**: Contesto client che verrà inviato in modo opaco agli osservatori e [HttpDelegate](class_mip_httpdelegate.md) facoltativi


  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: Impostazioni di protezione 


* **context**: Contesto client che verrà trasmesso in modo opaco a [HttpDelegate](class_mip_httpdelegate.md) facoltativo



  
**Restituisce**: [ProtectionHandler](class_mip_protectionhandler.md)