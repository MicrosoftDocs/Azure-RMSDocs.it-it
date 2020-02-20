---
title: Classe mip::ProtectionEngine
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 23f9f54a3f9701d0c9321b7ba643ed7dd3f47be1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486835"
---
# <a name="class-mipprotectionengine"></a>Classe mip::ProtectionEngine 
Gestisce azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public std:: shared_ptr\<AsyncControl\> GetTemplatesAsync (const std:: shared_ptr\<ProtectionEngine:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public std:: Vector\<std:: shared_ptr\<TemplateDescriptor\>\> gettemplates (const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public bool IsFeatureSupported (FeatureId featureId)  |  Verificare che la funzionalità sia supportata.
public std:: shared_ptr\<AsyncControl\> GetRightsForLabelIdAsync (const std:: String & documentId, const std:: String & labelId, const std:: String & ownerEmail, const std:: String & delegatedUserEmail, const std:: shared_ptr\<ProtectionEngine:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.
public std:: Vector\<std:: String\> GetRightsForLabelId (const std:: String & documentId, const std:: String & labelId, const std:: String & ownerEmail, const std:: String & delegatedUserEmail, const std:: shared_ptr\<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un labelId.
public std:: shared_ptr\<AsyncControl\> CreateProtectionHandlerForPublishingAsync (const ProtectionHandler::P ublishingSettings & Settings, const std:: shared_ptr\<ProtectionHandler:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler::P ublishingSettings & Settings, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<AsyncControl\> CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & Settings, const std:: shared_ptr\<ProtectionHandler:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler:: ConsumptionSettings & Settings, const std:: shared_ptr\<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public bool LoadUserCert (const std:: shared_ptr\<void\>& context)  |  pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.
public std:: shared_ptr\<AsyncControl\> LoadUserCertAsync (const std:: shared_ptr\<ProtectionEngine:: Observer\>& Observer, const std:: shared_ptr\<void\>& context)  |  pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni del motore.

  
**Restituisce**: impostazioni del motore
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync (funzione)
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **Observer**: una classe che implementa l'interfaccia ProtectionEngine:: Observer 


* **contesto**: contesto client che verrà passato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="gettemplates-function"></a>Funzione gettemplates
Ottiene la raccolta di modelli disponibili per un utente.

Parametri:  
* **contesto**: contesto client che verrà passato in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: elenco di ID modello
  
### <a name="isfeaturesupported-function"></a>IsFeatureSupported (funzione)
Verificare che la funzionalità sia supportata.

Parametri:  
* **FeatureId**: ID della funzionalità da controllare



  
**Restituisce**: risultato booleano
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.

Parametri:  
* **documentId**: ID documento associato ai metadati del documento 


* **LabelId**: ID etichetta associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **Observer**: una classe che implementa l'interfaccia ProtectionEngine:: Observer 


* **contesto**: lo stesso contesto verrà inviato a ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess o ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure



  
**Restituisce**: oggetto controllo asincrono.
  
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



  
**Restituisce**: oggetto controllo asincrono.
  
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



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri:  
* **Impostazioni**: impostazioni di protezione 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: ProtectionHandler
  
### <a name="loadusercert-function"></a>LoadUserCert (funzione)
pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.

Parametri:  
* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: true se il caricamento è riuscito altrimenti false.
  
### <a name="loadusercertasync-function"></a>LoadUserCertAsync (funzione)
pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.

Parametri:  
* **Observer**: una classe che implementa l'interfaccia ProtectionHandler:: Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.