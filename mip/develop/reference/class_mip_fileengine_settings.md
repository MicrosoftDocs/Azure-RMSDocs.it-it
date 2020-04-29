---
title: 'Classe fileengine:: Settings'
description: "Documenta la classe fileengine:: Settings dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 5a992c81b4d32a876f5f047a98b229aace7cb075
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763258"
---
# <a name="class-fileenginesettings"></a>Classe fileengine:: Settings 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String& engineId, const std:\<:\> shared_ptr AuthDelegate& AuthDelegate, const std:: String& clientData, const std:: String& locale, bool loadSensitivityTypes)  |  Costruttore FileEngine::Settings per il caricamento di un motore esistente.
Impostazioni pubbliche (const Identity& Identity, const std:\<:\> shared_ptr AuthDelegate& AuthDelegate, const std:: String& clientData, const std:: String& locale, bool loadSensitivityTypes)  |  Costruttore FileProfile::Settings per la creazione di un nuovo motore.
public const std::string& GetEngineId() const  |  Restituisce l'ID motore.
public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
public const Identity& GetIdentity() const  |  Restituisce l'identità del motore.
public void SetIdentity(const Identity& identity)  |  Imposta l'identità del motore.
public const std::string& GetClientData() const  |  Restituisce i dati client del motore.
public const std::string& GetLocale() const  |  Restituisce le impostazioni locali del motore.
public void SetCustomSettings (const std::\<vector std::p\<Air std:: String, std::\> \> String& value)  |  Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public const std::\<vector std::p\<Air std:: String, std::\> \> String& GetCustomSettings () const  |  Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore.
public const std::string& GetSessionId() const  |  Restituisce l'ID sessione del motore.
void public void (Cloud Cloud)  |  Imposta facoltativamente il cloud di destinazione.
Cloud pubblico getcloud () const  |  Ottiene il cloud di destinazione utilizzato da tutte le richieste di servizio.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud di protezione per il cloud personalizzato.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Ottiene l'URL di base dell'endpoint cloud di protezione.
public void SetPolicyCloudEndpointBaseUrl (const std:: String& policyCloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud dei criteri per il cloud personalizzato.
public const std:: String& GetPolicyCloudEndpointBaseUrl () const  |  Ottiene l'URL di base dell'endpoint cloud dei criteri.
public void SetProtectionOnlyEngine (bool protectionOnly)  |  Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
public const bool IsProtectionOnlyEngine() const  |  Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.
public bool IsLoadSensitivityTypesEnabled () const  |  Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.
public void EnablePFile (valore bool)  |  Imposta il flag che indica se produrre Pfile.
Public Const bool IsPFileEnabled ()  |  Ottiene il flag che indica se produce Pfile.
public void SetDelegatedUserEmail (const std:: String& delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String& GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
public void SetLabelFilter (const std::\<vector\> LabelFilterType& labelFilter)  |  Imposta il filtro delle etichette.
public const std::\<vector\> LabelFilterType& GetLabelFilter () const  |  Ottiene il filtro dell'etichetta.
public void SetAuthDelegate (const std::\<shared_ptr\> AuthDelegate& AuthDelegate)  |  Impostare il delegato di autenticazione del motore.
public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  Ottiene il delegato di autenticazione del motore.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore FileEngine::Settings per il caricamento di un motore esistente.

Parametri  
* **engineId**: imposta l'ID del motore univoco generato da AddEngineAsync. 


* **authDelegate**: il delegato di autenticazione usato dall'SDK per acquisire i token di autenticazione, eseguirà l'override di PolicyProfile:: Settings:: authDelegate se entrambi specificati 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **loadSensitivityTypes**: il flag facoltativo che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se il valore true OnPolicyChange Observer nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="settings-function"></a>Funzione Settings
Costruttore FileProfile::Settings per la creazione di un nuovo motore.

Parametri  
* **identity**: informazioni di identità relative all'utente associato al nuovo motore. 


* **authDelegate**: il delegato di autenticazione usato dall'SDK per acquisire i token di autenticazione, eseguirà l'override di PolicyProfile:: Settings:: authDelegate se entrambi specificati 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **loadSensitivityTypes**: il flag facoltativo che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se il valore true OnPolicyChange Observer nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Restituisce l'ID motore.
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID del motore.

Parametri  
* **ID**: ID del motore.


  
### <a name="getidentity-function"></a>GetIdentity (funzione)
Restituisce l'identità del motore.
  
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
  
### <a name="setcloud-function"></a>Funzione secloud
Imposta facoltativamente il cloud di destinazione.

Parametri  
* **cloud**: cloud


Se il cloud non è specificato, l'impostazione predefinita sarà cloud globale.
  
### <a name="getcloud-function"></a>Funzione getcloud
Ottiene il cloud di destinazione utilizzato da tutte le richieste di servizio.

  
**Restituisce**: cloud
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl (funzione)
Imposta l'URL di base dell'endpoint cloud di protezione per il cloud personalizzato.

Parametri  
* **protectionCloudEndpointBaseUrl**: URL di base associato agli endpoint di protezione


Questo valore verrà letto e deve essere impostato solo per cloud = Custom
  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl (funzione)
Ottiene l'URL di base dell'endpoint cloud di protezione.

  
**Restituisce**: URL di base associato agli endpoint di protezione questo valore verrà letto e deve essere impostato per cloud = Custom
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl (funzione)
Imposta l'URL di base dell'endpoint cloud dei criteri per il cloud personalizzato.

Parametri  
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

  
**Restituisce**: true se Enabled else false.
  
### <a name="enablepfile-function"></a>EnablePFile (funzione)
Imposta il flag che indica se produrre Pfile.
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled (funzione)
Ottiene il flag che indica se produce Pfile.

  
**Restituisce**: true se Enabled else false.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail (funzione)
Imposta l'utente delegato.

Parametri  
* **delegatedUserEmail**: il messaggio di posta elettronica di delega.


Un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail (funzione)
Ottiene l'utente delegato.

  
**Returns**: utente delegato specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="setlabelfilter-function"></a>SetLabelFilter (funzione)
Imposta il filtro delle etichette.

Parametri  
* **labelFilter**: filtro etichette.


Per impostazione predefinita, le etichette sono filtro per ambito. questa API consente di filtrare in base alle possibili azioni. Se non è impostato, HyokProtection e DoubleKeyProtection vengono filtrati.
  
### <a name="getlabelfilter-function"></a>GetLabelFilter (funzione)
Ottiene il filtro dell'etichetta.

  
**Restituisce**: filtro etichette.
Per impostazione predefinita, le etichette sono filtro per ambito. questa API consente di filtrare in base alle possibili azioni.
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate (funzione)
Impostare il delegato di autenticazione del motore.

Parametri  
* **authDelegate**: delegato di autenticazione


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato di autenticazione del motore.

  
**Restituisce**: delegato di autenticazione del motore.