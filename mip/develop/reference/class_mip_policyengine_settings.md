---
title: Classe mip PolicyEngine Settings
description: Riferimento per la classe mip PolicyEngine Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6ac94d1e34615a0248dac85f28c55154b127574f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446346"
---
# <a name="class-mippolicyenginesettings"></a>Classe mip::PolicyEngine::Settings 
Definisce le impostazioni associate a un oggetto [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per il caricamento di un motore esistente.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per la creazione di un nuovo motore.
 public const std::string& GetEngineId() const  |  Ottiene l'ID del motore.
 public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
 public const Identity& GetIdentity() const  |  Ottiene l'oggetto Identity.
 public void SetIdentity(const Identity& identity)  |  Imposta l'oggetto Identity.
 public const std::string& GetClientData() const  |  Ottiene il set di dati client configurato nelle impostazioni.
 public void SetClientData(const std::string& clientData)  |  Imposta la stringa di dati client.
 public const std::string& GetLocale() const  |  Ottiene le impostazioni locali configurate nelle impostazioni.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione, usato per la telemetria definita dal client.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione, un identificatore univoco.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: impostare sull'ID motore univoco generato da AddEngineAsync o su un valore generato automaticamente. Quando si carica un motore esistente, usare nuovamente l'ID. In caso contrario verrà creato un nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali.


  
### <a name="settings"></a>Impostazioni
Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: informazioni di identità relative all'utente associato al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali.


  
### <a name="getengineid"></a>GetEngineId
Ottiene l'ID del motore.

  
**Restituisce**: stringa univoca che identifica il motore.
  
### <a name="setengineid"></a>SetEngineId
Imposta l'ID del motore.

Parametri:  
* **id**: ID motore.


  
### <a name="getidentity"></a>GetIdentity
Ottiene l'oggetto Identity.

  
**Restituisce**: riferimento all'identità nell'oggetto Settings. 
  
**Vedere anche**: mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Imposta l'oggetto Identity.

Parametri:  
* **identity**: identificatore univoco di un utente. 


  
**Vedere anche**: mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Ottiene il set di dati client configurato nelle impostazioni.

  
**Restituisce**: stringa di dati specificata dal client.
  
### <a name="setclientdata"></a>SetClientData
Imposta la stringa di dati client.

Parametri:  
* **clientData**: dati specificati dall'utente.


  
### <a name="getlocale"></a>GetLocale
Ottiene le impostazioni locali configurate nelle impostazioni.

  
**Restituisce**: impostazioni locali.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri:  
* **customSettings**: elenco di coppie nome/valore.


  
### <a name="getcustomsettings"></a>GetCustomSettings
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce:**: elenco di coppie nome/valore.
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione, usato per la telemetria definita dal client.

Parametri:  
* **sessionId**: stringa univoca che connette gli eventi di telemetria.


  
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione, un identificatore univoco.

  
**Restituisce**: ID sessione.