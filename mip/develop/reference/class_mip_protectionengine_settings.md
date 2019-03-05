---
title: Classe mip::ProtectionEngine::Settings
description: Documenta la classe mip::protectionengine di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d874e57806ecf2ee98fa41eb3b655e9525ed8362
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333756"
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
public const Identity& GetIdentity() const  |  Ottiene l'utente [identità](class_mip_identity.md) associate al motore.
public void SetIdentity(const Identity& identity)  |  Imposta l'utente [identità](class_mip_identity.md) associate al motore.
public const std::string& GetClientData() const  |  Ottiene i dati personalizzati specificati dal client.
public void SetClientData(const std::string& clientData)  |  Imposta i dati personalizzati specificati dal client.
public const std::string& GetLocale() const  |  Ottiene le impostazioni locali in cui verranno scritti i dati del motore.
public void SetCustomSettings (const std:: Vector\<std:: Pair\<std:: String, std:: String\>\>& valore)  |  Imposta coppie nome-valore usate a scopi di test e sperimentazione.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene coppie nome-valore usate a scopi di test e sperimentazione.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione del motore.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Facoltativamente, imposta l'URL di base dell'endpoint cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: [Identity](class_mip_identity.md) che verrà associato [ProtectionEngine](class_mip_protectionengine.md)


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: Output del motore verrà fornito con queste impostazioni locali.


  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: Identificatore univoco del motore che verrà caricato 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: Output del motore verrà fornito con queste impostazioni locali.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Ottiene l'ID motore.

  
**Restituisce**: ID del motore
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID motore.

Parametri:  
* **engineId**: ID motore.


  
### <a name="getidentity-function"></a>Operazione GetIdentity (funzione)
Ottiene l'utente [identità](class_mip_identity.md) associate al motore.

  
**Restituisce**: Utente [identità](class_mip_identity.md) associate al motore
  
### <a name="setidentity-function"></a>SetIdentity (funzione)
Imposta l'utente [identità](class_mip_identity.md) associate al motore.

Parametri:  
* **identity**: Utente [identità](class_mip_identity.md) associate al motore


  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Ottiene i dati personalizzati specificati dal client.

  
**Restituisce**: Dati personalizzati specificati dal client
  
### <a name="setclientdata-function"></a>SetClientData (funzione)
Imposta i dati personalizzati specificati dal client.

Parametri:  
* **Custom**: dati specificati dal client


  
### <a name="getlocale-function"></a>GetLocale (funzione)
Ottiene le impostazioni locali in cui verranno scritti i dati del motore.

  
**Restituisce**: Impostazioni locali del motore verranno scritti i dati
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta coppie nome-valore usate a scopi di test e sperimentazione.

Parametri:  
* **customSettings**: Utilizzato per il test e sperimentazione coppie nome/valore


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene coppie nome-valore usate a scopi di test e sperimentazione.

  
**Restituisce**: Utilizzato per il test e sperimentazione coppie nome/valore
  
### <a name="setsessionid-function"></a>SetSessionId (funzione)
Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.

Parametri:  
* **sessionId**: ID sessione del motore, utilizzato per la correlazione di registrazione e telemetria


  
### <a name="getsessionid-function"></a>GetSessionId (funzione)
Ottiene l'ID sessione del motore.

  
**Restituisce**: ID sessione del motore
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl (funzione)
Facoltativamente, imposta l'URL di base dell'endpoint cloud.

Parametri:  
* **cloudEndpointBaseUrl**: URL di base usato da tutte le richieste di servizio (ad esempio, "https://api.aadrm.com")


Se l'URL di base non viene specificato, sarà determinato tramite una ricerca DNS del dominio dell'identità del motore.
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.

  
**Restituisce**: URL di base
