---
title: Classe mip::PolicyEngine::Settings
description: Documenta la classe MIP::p olicyengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d4eef1af6e738e7fbd2c33e961dcbffca8781924
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885277"
---
# <a name="class-mippolicyenginesettings"></a>Classe mip::PolicyEngine::Settings 
Definisce le impostazioni associate a un oggetto [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String & engineId, const std:: String & clientData, const std:: String & locale, bool loadSensitivityTypes)  |  Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per il caricamento di un motore esistente.
Impostazioni pubbliche (const Identity & Identity, const std:: String & clientData, const std:: String & locale, bool loadSensitivityTypes)  |  Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per la creazione di un nuovo motore.
public const std::string& GetEngineId() const  |  Ottiene l'ID del motore.
public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
public const Identity& GetIdentity() const  |  Ottiene l'oggetto [Identity](class_mip_identity.md) .
public void SetIdentity(const Identity& identity)  |  Impostare l'oggetto [Identity](class_mip_identity.md) .
public const std::string& GetClientData() const  |  Ottiene il set di dati client configurato nelle impostazioni.
public void SetClientData(const std::string& clientData)  |  Imposta la stringa di dati client.
public const std::string& GetLocale() const  |  Ottiene le impostazioni locali configurate nelle impostazioni.
public void SetCustomSettings (const std::\<vector std::p\<Air std:: String, std::\>String\>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std::\<vector std::p\<Air std:: String, std::\>String\>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione, usato per la telemetria definita dal client.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione, un identificatore univoco.
public bool IsLoadSensitivityTypesEnabled () const  |  Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Facoltativamente, imposta l'URL di base dell'endpoint cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: Impostarlo sull'ID del motore univoco generato da AddEngineAsync o da un oggetto generato automaticamente. Quando si carica un motore esistente, usare nuovamente l'ID. In caso contrario verrà creato un nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **Facoltativo**: il flag che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se il true OnPolicyChange Observer nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="settings-function"></a>Funzione Settings
Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: Informazioni di [identità](class_mip_identity.md) dell'utente associato al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **Facoltativo**: il flag che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se il true OnPolicyChange Observer nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Ottiene l'ID del motore.

  
**Restituisce**: Stringa univoca che identifica il motore.
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID del motore.

Parametri:  
* **id**: ID motore.


  
### <a name="getidentity-function"></a>GetIdentity (funzione)
Ottiene l'oggetto [Identity](class_mip_identity.md) .

  
**Restituisce**: Riferimento all'identità nell'oggetto Settings. 
  
**Vedere anche**: [MIP:: Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>Funzione seidentity
Impostare l'oggetto [Identity](class_mip_identity.md) .

Parametri:  
* **identity**: identificatore univoco di un utente. 


  
**Vedere anche**: [MIP:: Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Ottiene il set di dati client configurato nelle impostazioni.

  
**Restituisce**: Stringa di dati specificata dal client.
  
### <a name="setclientdata-function"></a>SetClientData (funzione)
Imposta la stringa di dati client.

Parametri:  
* **clientData**: dati specificati dall'utente.


  
### <a name="getlocale-function"></a>GetLocale (funzione)
Ottiene le impostazioni locali configurate nelle impostazioni.

  
**Restituisce**: Impostazioni locali.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri:  
* **customSettings**: Elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce**: Elenco di coppie nome/valore.
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione, usato per la telemetria definita dal client.

Parametri:  
* **sessionId**: stringa univoca che connette gli eventi di telemetria.


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione, un identificatore univoco.

  
**Restituisce**: ID della sessione.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (funzione)
Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.

  
**Restituisce**: True se Enabled else false.
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl (funzione)
Facoltativamente, imposta l'URL di base dell'endpoint cloud.

Parametri:  
* **cloudEndpointBaseUrl**: URL di base usato da tutte le richieste di servizio (ad esempio, "https://dataservice.protection.outlook.com")


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl (funzione)
Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.

  
**Restituisce**: URL di base
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail (funzione)
Imposta l'utente delegato.

Parametri:  
* **delegatedUserEmail**: il messaggio di posta elettronica di delega.


Un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail (funzione)
Ottiene l'utente delegato.

  
**Restituisce**: Utente delegato viene specificato un utente delegato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente