---
title: Classe mip::FileEngine::Settings
description: "Documenta la classe MIP:: fileengine dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 00ad6058b146f428a65a0697b722e6d3adb5c07d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884308"
---
# <a name="class-mipfileenginesettings"></a>Classe mip::FileEngine::Settings 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String & engineId, const std:: String & clientData, const std:: String & locale, bool loadSensitivityTypes)  |  Costruttore [FileEngine::Settings](class_mip_fileengine_settings.md) per il caricamento di un motore esistente.
Impostazioni pubbliche (const Identity & Identity, const std:: String & clientData, const std:: String & locale, bool loadSensitivityTypes)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md) per la creazione di un nuovo motore.
public const std::string& GetEngineId() const  |  Restituisce l'ID motore.
public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
public const Identity& GetIdentity() const  |  Restituisce l' [identità](class_mip_identity.md)del motore.
public void SetIdentity(const Identity& identity)  |  Imposta l'identità del motore.
public const std::string& GetClientData() const  |  Restituisce i dati client del motore.
public const std::string& GetLocale() const  |  Restituisce le impostazioni locali del motore.
public void SetCustomSettings (const std::\<vector std::p\<Air std:: String, std::\>String\>& value)  |  Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public const std::\<vector std::p\<Air std:: String, std::\>String\>& GetCustomSettings () const  |  Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore.
public const std::string& GetSessionId() const  |  Restituisce l'ID sessione del motore.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud di protezione, usato per specificare il limite del cloud.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Ottiene l'URL di base dell'endpoint cloud di protezione.
public void SetPolicyCloudEndpointBaseUrl (const std:: String & policyCloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud dei criteri, usato per specificare il limite del cloud.
public const std:: String & GetPolicyCloudEndpointBaseUrl () const  |  Ottiene l'URL di base dell'endpoint cloud dei criteri.
public void SetProtectionOnlyEngine (bool protectionOnly)  |  Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
public const bool IsProtectionOnlyEngine() const  |  Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.
public bool IsLoadSensitivityTypesEnabled () const  |  Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.
public void EnablePFile (valore bool)  |  Imposta il flag che indica se produrre Pfile.
Public Const bool IsPFileEnabled ()  |  Ottiene il flag che indica se produce Pfile.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore [FileEngine::Settings](class_mip_fileengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: Impostarlo sull'ID motore univoco generato da AddEngineAsync. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **loadSensitivityTypes**: Flag facoltativo che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se l'osservatore true OnPolicyChange nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="settings-function"></a>Funzione Settings
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: Informazioni di [identità](class_mip_identity.md) dell'utente associato al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **loadSensitivityTypes**: Flag facoltativo che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se l'osservatore true OnPolicyChange nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Restituisce l'ID motore.
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID del motore.

Parametri:  
* **id**: ID motore.


  
### <a name="getidentity-function"></a>GetIdentity (funzione)
Restituisce l' [identità](class_mip_identity.md)del motore.
  
### <a name="setidentity-function"></a>Funzione seidentity
Imposta l'identità del motore.
  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Restituisce i dati client del motore.
  
### <a name="getlocale-function"></a>GetLocale (funzione)
Restituisce le impostazioni locali del motore.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione del motore.
  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Restituisce l'ID sessione del motore.
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl (funzione)
Imposta l'URL di base dell'endpoint cloud di protezione, usato per specificare il limite del cloud.

Parametri:  
* **protectionCloudEndpointBaseUrl**: URL di base associato agli endpoint di protezione


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl (funzione)
Ottiene l'URL di base dell'endpoint cloud di protezione.

  
**Restituisce**: URL di base associato agli endpoint di protezione
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl (funzione)
Imposta l'URL di base dell'endpoint cloud dei criteri, usato per specificare il limite del cloud.

Parametri:  
* **policyCloudEndpointBaseUrl**: URL di base associato agli endpoint dei criteri


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl (funzione)
Ottiene l'URL di base dell'endpoint cloud dei criteri.

  
**Restituisce**: URL di base associato agli endpoint dei criteri
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine (funzione)
Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine (funzione)
Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (funzione)
Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.

  
**Restituisce**: True se Enabled else false.
  
### <a name="enablepfile-function"></a>EnablePFile (funzione)
Imposta il flag che indica se produrre Pfile.
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled (funzione)
Ottiene il flag che indica se produce Pfile.

  
**Restituisce**: True se Enabled else false.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail (funzione)
Imposta l'utente delegato.

Parametri:  
* **delegatedUserEmail**: il messaggio di posta elettronica di delega.


Un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail (funzione)
Ottiene l'utente delegato.

  
**Restituisce**: Utente delegato viene specificato un utente delegato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente