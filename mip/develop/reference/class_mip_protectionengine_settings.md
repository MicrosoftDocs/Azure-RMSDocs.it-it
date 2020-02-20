---
title: Classe mip::ProtectionEngine::Settings
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 71f428667bf485d0abd4f953aa2d94181b1bd8f1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486886"
---
# <a name="class-mipprotectionenginesettings"></a>Classe mip::ProtectionEngine::Settings 
Impostazioni utilizzate da ProtectionEngine durante la sua creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Costruttore ProtectionEngine:: Settings per la creazione di un nuovo motore.
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Costruttore ProtectionEngine:: Settings per il caricamento di un motore esistente.
public const std::string& GetEngineId() const  |  Ottiene l'ID motore.
public void SetEngineId(const std::string& engineId)  |  Imposta l'ID motore.
public const Identity& GetIdentity() const  |  Ottiene l'identità utente associata al motore.
public void SetIdentity(const Identity& identity)  |  Imposta l'identità utente associata al motore.
public const std::string& GetClientData() const  |  Ottiene i dati personalizzati specificati dal client.
public void SetClientData(const std::string& clientData)  |  Imposta i dati personalizzati specificati dal client.
public const std::string& GetLocale() const  |  Ottiene le impostazioni locali in cui verranno scritti i dati del motore.
public void SetCustomSettings (const std:: Vector\<std::p Air\<std:: String, std:: String\>\>valore &)  |  Imposta coppie nome-valore usate a scopi di test e sperimentazione.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetCustomSettings () const  |  Ottiene coppie nome-valore usate a scopi di test e sperimentazione.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione del motore.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Facoltativamente, imposta l'URL di base dell'endpoint cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionEngine:: Settings per la creazione di un nuovo motore.

Parametri:  
* **Identity**: identità che verrà associata a ProtectionEngine


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output del motore verrà fornito con queste impostazioni locali.


  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionEngine:: Settings per il caricamento di un motore esistente.

Parametri:  
* **engineId**: identificatore univoco del motore che verrà caricato 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output del motore verrà fornito con queste impostazioni locali.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Ottiene l'ID motore.

  
**Restituisce**: ID motore
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID motore.

Parametri:  
* **engineId**: ID motore.


  
### <a name="getidentity-function"></a>GetIdentity (funzione)
Ottiene l'identità utente associata al motore.

  
**Restituisce**: identità utente associata al motore
  
### <a name="setidentity-function"></a>Funzione seidentity
Imposta l'identità utente associata al motore.

Parametri:  
* **identity**: identità utente associata al motore


  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Ottiene i dati personalizzati specificati dal client.

  
**Restituisce**: dati personalizzati specificati dal client
  
### <a name="setclientdata-function"></a>SetClientData (funzione)
Imposta i dati personalizzati specificati dal client.

Parametri:  
* **Custom**: dati specificati dal client


  
### <a name="getlocale-function"></a>GetLocale (funzione)
Ottiene le impostazioni locali in cui verranno scritti i dati del motore.

  
**Restituisce**: impostazioni locali in cui verranno scritti i dati del motore
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta coppie nome-valore usate a scopi di test e sperimentazione.

Parametri:  
* **customSettings**: coppie nome-valore usate a scopi di test e sperimentazione


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene coppie nome-valore usate a scopi di test e sperimentazione.

  
**Restituisce**: coppie nome-valore usate a scopi di test e sperimentazione
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.

Parametri:  
* **sessionId**: ID sessione del motore, usato per la correlazione di registrazione/telemetria


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione del motore.

  
**Restituisce**: ID sessione del motore
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl (funzione)
Facoltativamente, imposta l'URL di base dell'endpoint cloud.

Parametri:  
* **cloudEndpointBaseUrl**: URL di base usato da tutte le richieste di servizio (ad esempio, "https://api.aadrm.com")


Se l'URL di base non viene specificato, sarà determinato tramite una ricerca DNS del dominio dell'identità del motore.
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl (funzione)
Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.

  
**Restituisce**: URL di base