---
title: 'Classe ProtectionEngine:: Settings'
description: "Documenta la classe protectionengine:: Settings dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 015c806c8830fd932354a1cc6afa33e15b9c1256
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225029"
---
# <a name="class-protectionenginesettings"></a>Classe ProtectionEngine:: Settings 
Oggetto Settings usato da ProtectionEngine durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const Identity& Identity, const std:: shared_ptr \<AuthDelegate\>& authDelegate, const std:: string& clientData, const std:: string& locale)  |  Costruttore ProtectionEngine::Settings per la creazione di un nuovo motore.
Impostazioni pubbliche (const std:: String& engineId, const std:: shared_ptr \<AuthDelegate\>& authDelegate, const std:: string& clientData, const std:: string& locale)  |  Costruttore ProtectionEngine::Settings per il caricamento di un motore esistente.
public const std::string& GetEngineId() const  |  Ottiene l'ID motore.
public void SetEngineId(const std::string& engineId)  |  Imposta l'ID motore.
public const Identity& GetIdentity() const  |  Ottiene l'identità utente associata al motore.
public void SetIdentity(const Identity& identity)  |  Imposta l'identità utente associata al motore.
public const std::string& GetClientData() const  |  Ottiene i dati personalizzati specificati dal client.
public void SetClientData(const std::string& clientData)  |  Imposta i dati personalizzati specificati dal client.
public const std::string& GetLocale() const  |  Ottiene le impostazioni locali in cui verranno scritti i dati del motore.
public void SetCustomSettings (const std:: Vector \<std::pair\<std::string, std::string\> \>& valore)  |  Imposta coppie nome-valore usate a scopi di test e sperimentazione.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Ottiene coppie nome-valore usate a scopi di test e sperimentazione.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione del motore.
void public void (Cloud Cloud)  |  Imposta facoltativamente il cloud di destinazione.
Cloud pubblico getcloud () const  |  Ottiene il cloud di destinazione utilizzato da tutte le richieste di servizio.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud per il cloud personalizzato.
public const std::string& GetCloudEndpointBaseUrl() const  |  Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.
public void SetAuthDelegate (const std:: shared_ptr \<AuthDelegate\>& authDelegate)  |  Impostare il delegato di autenticazione del motore.
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  Ottiene il delegato di autenticazione del motore.
public const std:: String& GetUnderlyingApplicationId () const  |  Ottiene l'ID applicazione sottostante.
public void SetUnderlyingApplicationId (const std:: String& underlyingApplicationId)  |  Imposta l'ID applicazione sottostante.
public bool GetAllowCloudServiceOnly () const  |  Ottiene un valore che indica se il servizio cloud è consentito o meno.
public void SetAllowCloudServiceOnly (bool allowCloudServiceOnly)  |  Imposta un valore che indica se il servizio cloud è consentito o meno.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionEngine::Settings per la creazione di un nuovo motore.

Parametri  
* **identity**: identità che verrà associata a ProtectionEngine


* **authDelegate**: il delegato di autenticazione usato dall'SDK per acquisire i token di autenticazione, eseguirà l'override di PolicyProfile:: Settings:: authDelegate se entrambi specificati 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output del motore verrà fornito con queste impostazioni locali.


  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionEngine::Settings per il caricamento di un motore esistente.

Parametri  
* **engineId**: identificatore univoco del motore che verrà caricato 


* **authDelegate**: il delegato di autenticazione usato dall'SDK per acquisire i token di autenticazione, eseguirà l'override di PolicyProfile:: Settings:: authDelegate se entrambi specificati 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output del motore verrà fornito con queste impostazioni locali.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Ottiene l'ID motore.

  
**Restituisce**: ID motore
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID motore.

Parametri  
* **engineId**: ID del motore.


  
### <a name="getidentity-function"></a>GetIdentity (funzione)
Ottiene l'identità utente associata al motore.

  
**Restituisce**: identità utente associata al motore
  
### <a name="setidentity-function"></a>Funzione seidentity
Imposta l'identità utente associata al motore.

Parametri  
* **identity**: identità utente associata al motore


  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Ottiene i dati personalizzati specificati dal client.

  
**Restituisce**: dati personalizzati specificati dal client
  
### <a name="setclientdata-function"></a>SetClientData (funzione)
Imposta i dati personalizzati specificati dal client.

Parametri  
* **Custom**: dati specificati dal client


  
### <a name="getlocale-function"></a>GetLocale (funzione)
Ottiene le impostazioni locali in cui verranno scritti i dati del motore.

  
**Restituisce**: impostazioni locali in cui verranno scritti i dati del motore
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta coppie nome-valore usate a scopi di test e sperimentazione.

Parametri  
* **customSettings**: coppie nome-valore usate a scopi di test e sperimentazione


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene coppie nome-valore usate a scopi di test e sperimentazione.

  
**Restituisce**: coppie nome-valore usate a scopi di test e sperimentazione
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione del motore, usato per la correlazione di registrazione/telemetria.

Parametri  
* **SessionID**: ID sessione del motore, usato per la correlazione di registrazione/telemetria


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione del motore.

  
**Restituisce**: ID sessione motore
  
### <a name="setcloud-function"></a>Funzione secloud
Imposta facoltativamente il cloud di destinazione.

Parametri  
* **Cloud**: cloud


Se il cloud non è specificato, sarà determinato dalla ricerca DNS del dominio di identità del motore, se possibile, in caso contrario, il fallback al cloud globale.
  
### <a name="getcloud-function"></a>Funzione getcloud
Ottiene il cloud di destinazione utilizzato da tutte le richieste di servizio.

  
**Restituisce**: cloud
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl (funzione)
Imposta l'URL di base dell'endpoint cloud per il cloud personalizzato.

Parametri  
* **cloudEndpointBaseUrl**: URL di base usato da tutte le richieste di servizio (ad esempio, "https://api.aadrm.com")


Questo valore verrà letto e deve essere impostato solo per cloud = Custom
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl (funzione)
Ottiene l'URL di base del cloud usato da tutte le richieste di servizio, se specificato.

  
**Restituisce**: URL di base
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate (funzione)
Impostare il delegato di autenticazione del motore.

Parametri  
* **authDelegate**: delegato di autenticazione


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato di autenticazione del motore.

  
**Restituisce**: delegato di autenticazione del motore.
  
### <a name="getunderlyingapplicationid-function"></a>GetUnderlyingApplicationId (funzione)
Ottiene l'ID applicazione sottostante.

  
**Restituisce**: ID applicazione sottostante
  
### <a name="setunderlyingapplicationid-function"></a>SetUnderlyingApplicationId (funzione)
Imposta l'ID applicazione sottostante.

Parametri  
* **UnderlyingApplicationId**: ID applicazione sottostante.


  
### <a name="getallowcloudserviceonly-function"></a>GetAllowCloudServiceOnly (funzione)
Ottiene un valore che indica se il servizio cloud è consentito o meno.

  
**Restituisce** un valore booleano che indica se è consentito o meno il servizio cloud.
  
### <a name="setallowcloudserviceonly-function"></a>SetAllowCloudServiceOnly (funzione)
Imposta un valore che indica se il servizio cloud è consentito o meno.

Parametri  
* **allowCloudServiceOnly**: valore booleano che indica se è consentito o meno il servizio cloud

