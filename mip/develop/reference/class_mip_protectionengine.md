---
title: Classe mip::ProtectionEngine
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9eb44a39f32c2997729e6d77ddace96c580328cd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73557753"
---
# <a name="class-mipprotectionengine"></a>Classe mip::ProtectionEngine 
Gestisce azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public void GetTemplatesAsync (const std:: shared_ptr\<ProtectionEngine:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public std:: Vector\<std:: String\> gettemplates (const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public void GetRightsForLabelIdAsync (const std:: String & documentId, const std:: String & labelId, const std:: String & ownerEmail, const std:: String & delegatedUserEmail, const std:: shared_ptr\<ProtectionEngine:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.
public std:: Vector\<std:: String\> GetRightsForLabelId (const std:: String & documentId, const std:: String & labelId, const std:: String & ownerEmail, const std:: String & delegatedUserEmail, const std:: shared_ptr @no__t _2_ void\>& contesto)  |  Ottiene la raccolta di diritti disponibili per un utente per un labelId.
public void CreateProtectionHandlerForPublishingAsync (const ProtectionHandler::P ublishingSettings & Settings, const std:: shared_ptr\<ProtectionHandler:: Observer\>& Observer, const std:: shared_ptr\<void @no__ contesto & t_3_)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler::P ublishingSettings & Settings, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public void CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & Settings, const std:: shared_ptr\<ProtectionHandler:: Observer\>& Observer, const std:: shared_ptr\<void @no contesto & __t_3_)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler:: ConsumptionSettings & Settings, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni del motore.

  
**Restituisce**: impostazioni del motore
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync (funzione)
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **Observer**: una classe che implementa l'interfaccia ProtectionEngine:: Observer 


* **contesto**: contesto client che verrà passato in modo opaco agli osservatori e HttpDelegate facoltativi


  
### <a name="gettemplates-function"></a>Funzione gettemplates
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **contesto**: contesto client che verrà passato in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: elenco di ID modello
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **LabelId**: ID etichetta associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **Observer**: una classe che implementa l'interfaccia ProtectionEngine:: Observer 


* **contesto**: lo stesso contesto verrà inviato a ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess o ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un labelId.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **LabelId**: ID etichetta associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **contesto**: lo stesso contesto verrà inviato a HttpDelegate facoltativo



  
**Restituisce**: elenco di diritti
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: impostazioni di protezione 


* **Observer**: una classe che implementa l'interfaccia ProtectionHandler:: Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi


  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: impostazioni di protezione 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: ProtectionHandler
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: impostazioni di protezione 


* **Observer**: una classe che implementa l'interfaccia ProtectionHandler:: Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi


  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: impostazioni di protezione 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: ProtectionHandler