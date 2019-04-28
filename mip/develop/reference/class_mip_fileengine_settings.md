---
title: Classe mip::FileEngine::Settings
description: 'Classe MIP:: fileengine di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2481ee7d42f00ce5b33529b15e17b22ba6556b0e
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184706"
---
# <a name="class-mipfileenginesettings"></a>Classe mip::FileEngine::Settings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String & engineId, const std:: String & clientData, const std:: String & delle impostazioni locali, loadSensitivityTypes bool)  |  Costruttore [FileEngine::Settings](class_mip_fileengine_settings.md) per il caricamento di un motore esistente.
Impostazioni pubbliche (const Identity & identity, const std:: String & clientData, const std:: String & delle impostazioni locali, loadSensitivityTypes bool)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md) per la creazione di un nuovo motore.
public const std::string& GetEngineId() const  |  Restituisce l'ID motore.
public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
public const Identity& GetIdentity() const  |  Restituisce il motore [identità](class_mip_identity.md).
public void SetIdentity(const Identity& identity)  |  Imposta l'identità del motore.
public const std::string& GetClientData() const  |  Restituisce i dati client del motore.
public const std::string& GetLocale() const  |  Restituisce le impostazioni locali del motore.
public void SetCustomSettings (const std:: Vector\<std:: Pair\<std:: String, std:: String\>\>& valore)  |  Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione del motore.
public const std::string& GetSessionId() const  |  Restituisce l'ID sessione del motore.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Imposta l'URL di base dell'endpoint cloud di protezione, usato per specificare il limite del cloud.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Ottiene l'url di base di protezione cloud endpoint.
public void SetPolicyCloudEndpointBaseUrl (const std:: String & policyCloudEndpointBaseUrl)  |  Imposta i criteri cloud endpoint url di base, consente di specificare limiti di cloud.
public const std::string& GetPolicyCloudEndpointBaseUrl() const  |  Ottiene l'url dell'endpoint cloud criteri base.
public void SetProtectionOnlyEngine(const bool protectionOnly)  |  Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
public const bool IsProtectionOnlyEngine() const  |  Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.
public bool IsLoadSensitivityTypesEnabled() const  |  Ottenere il flag che indica se le etichette di riservatezza di carico è abilitata.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [FileEngine::Settings](class_mip_fileengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: Impostare l'ID motore univoco generato da AddEngineAsync. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **loadSensitivityTypes**: Flag facoltativo che indica quando viene caricato il motore deve caricare anche tipi sensibilità personalizzata, se osservatore OnPolicyChange true nel profilo verranno richiamati per gli aggiornamenti per i tipi di sensibilità personalizzata, nonché le modifiche dei criteri. Se false ListSensitivityTypes chiama il metodo restituirà sempre un elenco vuoto.


  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: [Identità](class_mip_identity.md) informazioni dell'utente associata al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **loadSensitivityTypes**: Flag facoltativo che indica quando viene caricato il motore deve caricare anche tipi sensibilità personalizzata, se osservatore OnPolicyChange true nel profilo verranno richiamati per gli aggiornamenti per i tipi di sensibilità personalizzata, nonché le modifiche dei criteri. Se false ListSensitivityTypes chiama il metodo restituirà sempre un elenco vuoto.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Restituisce l'ID motore.
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID del motore.

Parametri:  
* **id**: ID motore.


  
### <a name="getidentity-function"></a>Operazione GetIdentity (funzione)
Restituisce il motore [identità](class_mip_identity.md).
  
### <a name="setidentity-function"></a>SetIdentity (funzione)
Imposta l'identità del motore.
  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Restituisce i dati client del motore.
  
### <a name="getlocale-function"></a>GetLocale (funzione)
Restituisce le impostazioni locali del motore.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di coppie nome-valore usate a scopi di test e sperimentazione.
  
### <a name="setsessionid-function"></a>SetSessionId (funzione)
Imposta l'ID sessione del motore.
  
### <a name="getsessionid-function"></a>GetSessionId (funzione)
Restituisce l'ID sessione del motore.
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl function
Imposta l'URL di base dell'endpoint cloud di protezione, usato per specificare il limite del cloud.

Parametri:  
* **protectionCloudEndpointBaseUrl**: Url di base associato con endpoint protection


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl function
Ottiene l'url di base di protezione cloud endpoint.

  
**Restituisce**: Url di base associato con endpoint protection
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl (funzione)
Imposta i criteri cloud endpoint url di base, consente di specificare limiti di cloud.

Parametri:  
* **policyCloudEndpointBaseUrl**: Url di base associato con endpoint dei criteri


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl (funzione)
Ottiene l'url dell'endpoint cloud criteri base.

  
**Restituisce**: Url di base associato con endpoint dei criteri
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine (funzione)
Imposta l'indicatore del motore di sola protezione, senza criteri/etichette.
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine (funzione)
Restituisce l'indicatore del motore di sola protezione, senza criteri/etichette.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (funzione)
Ottenere il flag che indica se le etichette di riservatezza di carico è abilitata.

  
**Restituisce**: True se abilitato in caso contrario false.