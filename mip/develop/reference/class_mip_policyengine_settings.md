---
title: Classe mip::PolicyEngine::Settings
description: Documenta la classe MIP::p olicyengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 620775649ee0fa593f141b1a4f983ad8b52caafe
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487617"
---
# <a name="class-mippolicyenginesettings"></a>Classe mip::PolicyEngine::Settings 
Definisce le impostazioni associate a un PolicyEngine.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String & engineId, const std:: String & clientData, const std:: String & locale, bool loadSensitivityTypes)  |  Costruttore PolicyEngine:: Settings per il caricamento di un motore esistente.
Impostazioni pubbliche (const Identity & Identity, const std:: String & clientData, const std:: String & locale, bool loadSensitivityTypes)  |  Costruttore PolicyEngine:: Settings per la creazione di un nuovo motore.
public const std::string& GetEngineId() const  |  Ottiene l'ID del motore.
public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
public const Identity& GetIdentity() const  |  Ottiene l'oggetto Identity.
public void SetIdentity(const Identity& identity)  |  Imposta l'oggetto Identity.
public const std::string& GetClientData() const  |  Ottiene il set di dati client configurato nelle impostazioni.
public void SetClientData(const std::string& clientData)  |  Imposta la stringa di dati client.
public const std::string& GetLocale() const  |  Ottiene le impostazioni locali configurate nelle impostazioni.
public void SetCustomSettings (const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione, usato per la telemetria definita dal client.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione, un identificatore univoco.
public bool IsLoadSensitivityTypesEnabled () const  |  Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Facoltativamente, imposta l'URL di base dell'endpoint cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
public void SetLabelFilter (const std:: Vector\<LabelFilterType\>& labelFilter)  |  Imposta il filtro delle etichette.
public const std:: Vector\<LabelFilterType\>& GetLabelFilter () const  |  Ottiene il filtro dell'etichetta.
public void SetVariableTextMarkingType (VariableTextMarkingType variableTextMarkingType)  |  Imposta il tipo di contrassegno del testo della variabile.
public VariableTextMarkingType GetVariableTextMarkingType () const  |  Ottiene il tipo di contrassegno del testo della variabile.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore PolicyEngine:: Settings per il caricamento di un motore esistente.

Parametri:  
* **engineId**: impostare sull'ID motore univoco generato da AddEngineAsync o su un valore generato automaticamente. Quando si carica un motore esistente, usare nuovamente l'ID. In caso contrario verrà creato un nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **Facoltativo**: il flag che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se il true OnPolicyChange Observer nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="settings-function"></a>Funzione Settings
Costruttore PolicyEngine:: Settings per la creazione di un nuovo motore.

Parametri:  
* **identity**: informazioni di identità relative all'utente associato al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **Facoltativo**: il flag che indica quando il motore è caricato deve caricare anche tipi di riservatezza personalizzati, se il true OnPolicyChange Observer nel profilo verrà richiamato sugli aggiornamenti ai tipi di riservatezza personalizzati e sulle modifiche dei criteri. Se la chiamata a false ListSensitivityTypes restituirà sempre un elenco vuoto.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Ottiene l'ID del motore.

  
**Restituisce**: stringa univoca che identifica il motore.
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID del motore.

Parametri:  
* **id**: ID motore.


  
### <a name="getidentity-function"></a>GetIdentity (funzione)
Ottiene l'oggetto Identity.

  
**Restituisce**: riferimento all'identità nell'oggetto Settings. 
  
**Vedere anche**: mip::Identity
  
### <a name="setidentity-function"></a>Funzione seidentity
Imposta l'oggetto Identity.

Parametri:  
* **identity**: identificatore univoco di un utente. 


  
**Vedere anche**: mip::Identity
  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Ottiene il set di dati client configurato nelle impostazioni.

  
**Restituisce**: stringa di dati specificata dal client.
  
### <a name="setclientdata-function"></a>SetClientData (funzione)
Imposta la stringa di dati client.

Parametri:  
* **clientData**: dati specificati dall'utente.


  
### <a name="getlocale-function"></a>GetLocale (funzione)
Ottiene le impostazioni locali configurate nelle impostazioni.

  
**Restituisce**: impostazioni locali.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri:  
* **customSettings**: elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce:** : elenco di coppie nome/valore.
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione, usato per la telemetria definita dal client.

Parametri:  
* **sessionId**: stringa univoca che connette gli eventi di telemetria.


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione, un identificatore univoco.

  
**Restituisce**: ID sessione.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (funzione)
Ottiene il flag che indica se sono abilitate le etichette di riservatezza di carico.

  
**Restituisce**: true se Enabled else false.
  
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

  
**Returns**: utente delegato specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="setlabelfilter-function"></a>SetLabelFilter (funzione)
Imposta il filtro delle etichette.

Parametri:  
* **labelFilter**: filtro etichette.


Per impostazione predefinita, le etichette sono filtro per ambito. questa API consente di filtrare in base alle possibili azioni.
  
### <a name="getlabelfilter-function"></a>GetLabelFilter (funzione)
Ottiene il filtro dell'etichetta.

  
**Restituisce**: filtro etichette.
Per impostazione predefinita, le etichette sono filtro per ambito. questa API consente di filtrare in base alle possibili azioni.
  
### <a name="setvariabletextmarkingtype-function"></a>SetVariableTextMarkingType (funzione)
Imposta il tipo di contrassegno del testo della variabile.

Parametri:  
* **variableTextMarkingType**: tipo di contrassegno del testo della variabile.


  
### <a name="getvariabletextmarkingtype-function"></a>GetVariableTextMarkingType (funzione)
Ottiene il tipo di contrassegno del testo della variabile.

  
**Returns**: tipo di contrassegno del testo della variabile.