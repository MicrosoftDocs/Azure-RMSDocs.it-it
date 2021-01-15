---
title: Classe ProtectionEngine
description: 'Documenta la classe protectionengine:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 6df50823102c7cf897dceb2d6d576384431ccfc6
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214678"
---
# <a name="class-protectionengine"></a>Classe ProtectionEngine 
Gestisce azioni correlate alla protezione relative a un'identità specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni del motore.
public std:: shared_ptr \<AsyncControl\> GetTemplatesAsync (const std:: shared_ptr \<ProtectionEngine::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public std:: Vector \<std::shared_ptr\<TemplateDescriptor\> \> gettemplates (const std:: shared_ptr \<void\>& context)  |  Ottiene la raccolta di modelli disponibili per un utente.
public bool IsFeatureSupported (FeatureId featureId)  |  Verificare che la funzionalità sia supportata.
public std:: shared_ptr \<AsyncControl\> GetRightsForLabelIdAsync (const std:: string& documentId, const std:: string& LabelId, const std:: string& owneremail, const std:: string& delegatedUserEmail, const std:: shared_ptr \<ProtectionEngine::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.
public std:: Vector \<std::string\> GetRightsForLabelId (const std:: string& documentId, const std:: string& LabelId, const std:: string& owneremail, const std:: string& delegatedUserEmail, const std:: shared_ptr \<void\>& context)  |  Ottiene la raccolta di diritti disponibili per un utente per un labelId.
public std:: shared_ptr \<AsyncControl\> CreateProtectionHandlerForPublishingAsync (const ProtectionHandler::P ublishingsettings& Settings, const std:: shared_ptr \<ProtectionHandler::Observer\>& Observer, const std:: shared_ptr& \<void\> context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr \<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler::P ublishingsettings& Settings, const std:: shared_ptr \<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr \<AsyncControl\> CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings& Settings, const std:: shared_ptr \<ProtectionHandler::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public std:: shared_ptr \<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler:: ConsumptionSettings& Settings, const std:: shared_ptr \<void\>& context)  |  Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.
public bool LoadUserCert (const std:: shared_ptr \<void\>& context)  |  pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.
public std:: shared_ptr \<AsyncControl\> LoadUserCertAsync (const std:: shared_ptr \<ProtectionEngine::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.
public void RegisterContentForTrackingAndRevocation (const std:: Vector \<uint8_t\>& serializedPublishingLicense, const std:: string& ContentName, bool isOwnerNotificationEnabled, const std:: shared_ptr \<void\>& context)  |  Registrare la licenza di pubblicazione (PL) per il rilevamento dei documenti & revoca.
public std:: shared_ptr \<AsyncControl\> RegisterContentForTrackingAndRevocationAsync (const std:: vector \<uint8_t\>& serializedPublishingLicense, const std:: String& ContentName, bool isOwnerNotificationEnabled, const std:: shared_ptr \<ProtectionEngine::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  Registrare la licenza di pubblicazione (PL) per il rilevamento dei documenti & revoca.
public void RevokeContent (const std:: Vector \<uint8_t\>& serializedPublishingLicense, const std:: shared_ptr \<void\>& context)  |  Eseguire la revoca per il contenuto.
public std:: shared_ptr \<AsyncControl\> RevokeContentAsync (const std:: vector \<uint8_t\>& serializedPublishingLicense, const std:: shared_ptr \<ProtectionEngine::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  Eseguire la revoca per il contenuto.
public std:: Vector \<std::shared_ptr\<DelegationLicense\> \> CreateDelegationLicenses (const DelegationLicenseSettings& Settings, const std:: shared_ptr \<void\>& context)  |  Crea una licenza delegata.
public std:: shared_ptr \<AsyncControl\> CreateDelegationLicensesAsync (const DelegationLicenseSettings& Settings, const std:: shared_ptr \<ProtectionEngine::Observer\>& Observer, const std:: shared_ptr \<void\>& context)  |  Crea una licenza delegata.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni del motore.

  
**Restituisce**: impostazioni del motore
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync (funzione)
Ottiene la raccolta di modelli disponibili per un utente.

Parametri  
* **observer**: classe che implementa l'interfaccia ProtectionEngine::Observer 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer e all'oggetto HttpDelegate facoltativo



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="gettemplates-function"></a>Funzione gettemplates
Ottiene la raccolta di modelli disponibili per un utente.

Parametri  
* **context**: contesto client che verrà passato in maniera opaca all'oggetto HttpDelegate facoltativo



  
**Restituisce**: elenco di ID modello
  
### <a name="isfeaturesupported-function"></a>IsFeatureSupported (funzione)
Verificare che la funzionalità sia supportata.

Parametri  
* **FeatureId**: ID della funzionalità da controllare



  
**Restituisce**: risultato booleano
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un ID etichetta.

Parametri  
* **documentId**: ID documento associato ai metadati del documento 


* **LabelId**: ID etichetta associato ai metadati del documento con cui è stato creato il documento 


* **owneremail**: proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **observer**: classe che implementa l'interfaccia ProtectionEngine::Observer 


* **context**: questo stesso contesto verrà inoltrato a ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess o ProtectionEngine::Observer::OnGetRightsForLabelIdFailure



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId (funzione)
Ottiene la raccolta di diritti disponibili per un utente per un labelId.

Parametri  
* **documentId**: ID documento associato ai metadati del documento 


* **LabelId**: ID etichetta associato ai metadati del documento con cui è stato creato il documento 


* **ownerEmail**: proprietario del documento 


* **R**: l'utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore 


* **context**: questo stesso contesto verrà inoltrato all'oggetto HttpDelegate facoltativo



  
**Restituisce**: elenco di diritti
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri  
* **Impostazioni**: impostazioni di protezione 


* **observer**: classe che implementa l'interfaccia ProtectionHandler::Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri  
* **Impostazioni**: impostazioni di protezione 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: ProtectionHandler
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri  
* **Impostazioni**: impostazioni di protezione 


* **observer**: classe che implementa l'interfaccia ProtectionHandler::Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption (funzione)
Crea un gestore di protezione in cui diritti/ruoli vengono assegnati a utenti specifici.

Parametri  
* **Impostazioni**: impostazioni di protezione 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: ProtectionHandler
  
### <a name="loadusercert-function"></a>LoadUserCert (funzione)
pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.

Parametri  
* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo



  
**Restituisce**: true se il caricamento è riuscito altrimenti false.
  
### <a name="loadusercertasync-function"></a>LoadUserCertAsync (funzione)
pre-preventivamente: caricare il certificato concessore di licenze utente, utile quando il caricamento in background tramite prelicense potrebbe incorrere in una chiamata di rete aggiuntiva.

Parametri  
* **observer**: classe che implementa l'interfaccia ProtectionHandler::Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="registercontentfortrackingandrevocation-function"></a>RegisterContentForTrackingAndRevocation (funzione)
Registrare la licenza di pubblicazione (PL) per il rilevamento dei documenti & revoca.

Parametri  
* **ContentName**: nome associato al contenuto specificato da serializedPublishingLicense. Se serializedPublishingLicense specifica un nome di contenuto, tale valore avrà la precedenza. 


* **isOwnerNotificationEnabled**: impostare su true per notificare al proprietario via posta elettronica ogni volta che il documento viene decrittografato oppure false per non inviare la notifica. 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo


  
### <a name="registercontentfortrackingandrevocationasync-function"></a>RegisterContentForTrackingAndRevocationAsync (funzione)
Registrare la licenza di pubblicazione (PL) per il rilevamento dei documenti & revoca.

Parametri  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata dal contenuto protetto 


* **ContentName**: nome associato al contenuto specificato da serializedPublishingLicense. Se serializedPublishingLicense specifica un nome di contenuto, tale valore avrà la precedenza 


* **isOwnerNotificationEnabled**: impostare su true per notificare al proprietario via posta elettronica ogni volta che il documento viene decrittografato oppure false per non inviare la notifica. 


* **observer**: classe che implementa l'interfaccia ProtectionHandler::Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="revokecontent-function"></a>RevokeContent (funzione)
Eseguire la revoca per il contenuto.

Parametri  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata dal contenuto protetto 


* **contesto**: contesto client che verrà trasmesso in modo opaco a HttpDelegate facoltativo


  
### <a name="revokecontentasync-function"></a>RevokeContentAsync (funzione)
Eseguire la revoca per il contenuto.

Parametri  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata dal contenuto protetto 


* **observer**: classe che implementa l'interfaccia ProtectionHandler::Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="createdelegationlicenses-function"></a>CreateDelegationLicenses (funzione)
Crea una licenza delegata.

Parametri  
* **Impostazioni**: impostazioni di delega 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: un vettore delle licenze di delega usa questo metodo per creare licenze per un elenco di utenti
  
### <a name="createdelegationlicensesasync-function"></a>CreateDelegationLicensesAsync (funzione)
Crea una licenza delegata.

Parametri  
* **Impostazioni**: impostazioni di delega 


* **observer**: classe che implementa l'interfaccia ProtectionHandler::Observer 


* **contesto**: contesto client che verrà inviato in modo opaco agli osservatori e HttpDelegate facoltativi



  
**Restituisce**: oggetto controllo asincrono.
Utilizzare questo metodo per creare licenze per un elenco di utenti. Ricevere il vettore DelegationLicense negli errori di callback OnCreateDelegatedLicensesSuccess vengono inviati in OnCreateDelegatedLicensesFailure