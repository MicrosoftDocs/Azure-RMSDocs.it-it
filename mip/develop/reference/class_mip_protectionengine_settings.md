---
title: Classe mip ProtectionEngine Settings
description: Riferimento per la classe mip ProtectionEngine Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f61e86a87ecfea21bc9d02f4e55f3fbe663e9b80
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446703"
---
# <a name="class-mipprotectionenginesettings"></a>Classe mip::ProtectionEngine::Settings 
Oggetto [Settings](class_mip_protectionengine_settings.md) usato da [ProtectionEngine](class_mip_protectionengine.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Costruttore [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) per la creazione di un nuovo motore.
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Costruttore [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) per il caricamento di un motore esistente.
 public const std::string& GetEngineId() const  |  Ottiene l'ID motore.
 public void SetEngineId(const std::string& engineId)  |  Imposta l'ID motore.
 public const Identity& GetIdentity() const  |  Ottiene l'identità utente associata al motore.
 public void SetIdentity(const Identity& identity)  |  Imposta l'identità utente associata al motore.
 public const std::string& GetClientData() const  |  Ottiene i dati personalizzati specificati dal client.
 public void SetClientData(const std::string& clientData)  |  Imposta i dati personalizzati specificati dal client.
 public const std::string& GetLocale() const  |  Ottiene le impostazioni locali in cui verranno scritti i dati del motore.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Imposta coppie nome-valore usate a scopi di test e sperimentazione.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Ottiene coppie nome-valore usate a scopi di test e sperimentazione.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione del motore.
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Facoltativamente, imposta l'URL di base dell'endpoint cloud.
 public const std::string& GetCloudEndpointBaseUrl() const  |  Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: identità che verrà associata a [ProtectionEngine](class_mip_protectionengine.md)


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output del motore verrà fornito con queste impostazioni locali.


  
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: identificatore univoco del motore che verrà caricato 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output del motore verrà fornito con queste impostazioni locali.


  
### <a name="getengineid"></a>GetEngineId
Ottiene l'ID motore.

  
**Restituisce**: ID motore
  
### <a name="setengineid"></a>SetEngineId
Imposta l'ID motore.

Parametri:  
* **engineId**: ID motore.


  
### <a name="getidentity"></a>GetIdentity
Ottiene l'identità utente associata al motore.

  
**Restituisce**: identità utente associata al motore
  
### <a name="setidentity"></a>SetIdentity
Imposta l'identità utente associata al motore.

Parametri:  
* **identity**: identità utente associata al motore


  
### <a name="getclientdata"></a>GetClientData
Ottiene i dati personalizzati specificati dal client.

  
**Restituisce**: dati personalizzati specificati dal client
  
### <a name="setclientdata"></a>SetClientData
Imposta i dati personalizzati specificati dal client.

Parametri:  
* **Custom**: dati specificati dal client


  
### <a name="getlocale"></a>GetLocale
Ottiene le impostazioni locali in cui verranno scritti i dati del motore.

  
**Restituisce**: impostazioni locali in cui verranno scritti i dati del motore
  
### <a name="setcustomsettings"></a>SetCustomSettings
Imposta coppie nome-valore usate a scopi di test e sperimentazione.

Parametri:  
* **customSettings**: coppie nome-valore usate a scopi di test e sperimentazione


  
### <a name="getcustomsettings"></a>GetCustomSettings
Ottiene coppie nome-valore usate a scopi di test e sperimentazione.

  
**Restituisce**: coppie nome-valore usate a scopi di test e sperimentazione
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.

Parametri:  
* **sessionId**: ID sessione del motore, usato per la correlazione di registrazione/telemetria


  
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione del motore.

  
**Restituisce**: ID sessione del motore
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
Facoltativamente, imposta l'URL di base dell'endpoint cloud.

Parametri:  
* **cloudEndpointBaseUrl**: URL di base usato da tutte le richieste di servizio (ad esempio, "https://api.aadrm.com")


Se l'URL di base non viene specificato, sarà determinato tramite una ricerca DNS del dominio dell'identità del motore.
  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.

  
**Restituisce**: URL di base