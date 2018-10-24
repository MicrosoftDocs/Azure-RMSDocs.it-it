---
title: Classe mip FileEngine Settings
description: Riferimento per la classe mip FileEngine Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 656ad1cf21a2d761dfb4c857b278b7421ee2b790
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446482"
---
# <a name="class-mipfileenginesettings"></a>Classe mip::FileEngine::Settings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Costruttore [FileEngine::Settings](class_mip_fileengine_settings.md) per il caricamento di un motore esistente.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md) per la creazione di un nuovo motore.
 public const std::string& GetEngineId() const  |  Restituisce l'ID motore.
 public const Identity& GetIdentity() const  |  Restituisce l'identità del motore.
 public void SetIdentity(const Identity& identity)  |  Imposta l'identità del motore.
 public const std::string& GetClientData() const  |  Restituisce i dati client del motore.
 public const std::string& GetLocale() const  |  Restituisce le impostazioni locali del motore.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore.
 public const std::string& GetSessionId() const  |  Restituisce l'ID sessione del motore.
 public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud di protezione, usato per specificare il limite del cloud.
 public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Ottiene cloudEndpointBaseUrl.
 public void SetProtectionOnlyEngine(const bool protectionOnly)  |  Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
 public const bool IsProtectionOnlyEngine() const  |  Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [FileEngine::Settings](class_mip_fileengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: impostare sull'ID motore univoco generato da AddEngineAsync. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali.


  
### <a name="settings"></a>Impostazioni
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: informazioni di identità relative all'utente associato al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali.


  
### <a name="getengineid"></a>GetEngineId
Restituisce l'ID motore.
  
### <a name="getidentity"></a>GetIdentity
Restituisce l'identità del motore.
  
### <a name="setidentity"></a>SetIdentity
Imposta l'identità del motore.
  
### <a name="getclientdata"></a>GetClientData
Restituisce i dati client del motore.
  
### <a name="getlocale"></a>GetLocale
Restituisce le impostazioni locali del motore.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
  
### <a name="getcustomsettings"></a>GetCustomSettings
Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione del motore.
  
### <a name="getsessionid"></a>GetSessionId
Restituisce l'ID sessione del motore.
  
### <a name="setprotectioncloudendpointbaseurl"></a>SetProtectionCloudEndpointBaseUrl
Imposta l'URL di base dell'endpoint cloud di protezione, usato per specificare il limite del cloud.

Parametri:  
* **protectionCloudEndpointBaseUrl**: URL di base associato agli endpoint di protezione


  
### <a name="getprotectioncloudendpointbaseurl"></a>GetProtectionCloudEndpointBaseUrl
Ottiene cloudEndpointBaseUrl.

  
**Restituisce**: URL di base associato agli endpoint di protezione
  
### <a name="setprotectiononlyengine"></a>SetProtectionOnlyEngine
Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
  
### <a name="isprotectiononlyengine"></a>IsProtectionOnlyEngine
Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.