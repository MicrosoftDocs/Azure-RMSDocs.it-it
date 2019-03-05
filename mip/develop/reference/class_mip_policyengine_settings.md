---
title: Classe mip::PolicyEngine::Settings
description: 'Classe MIP:: policyengine di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bc130d2c6056d971635bcf204243f29b13789466
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330834"
---
# <a name="class-mippolicyenginesettings"></a>Classe mip::PolicyEngine::Settings 
Definisce le impostazioni associate a un oggetto [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String & engineId, const std:: String & clientData, const std:: String & delle impostazioni locali, loadSensitivityTypes bool)  |  Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per il caricamento di un motore esistente.
Impostazioni pubbliche (const Identity & identity, const std:: String & clientData, const std:: String & delle impostazioni locali, loadSensitivityTypes bool)  |  Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per la creazione di un nuovo motore.
public const std::string& GetEngineId() const  |  Ottiene l'ID del motore.
public void SetEngineId(const std::string& id)  |  Imposta l'ID del motore.
public const Identity& GetIdentity() const  |  Ottenere il [identità](class_mip_identity.md) oggetto.
public void SetIdentity(const Identity& identity)  |  Impostare il [identità](class_mip_identity.md) oggetto.
public const std::string& GetClientData() const  |  Ottiene il set di dati client configurato nelle impostazioni.
public void SetClientData(const std::string& clientData)  |  Imposta la stringa di dati client.
public const std::string& GetLocale() const  |  Ottiene le impostazioni locali configurate nelle impostazioni.
public void SetCustomSettings (const std:: Vector\<std:: Pair\<std:: String, std:: String\>\>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione, usato per la telemetria definita dal client.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione, un identificatore univoco.
public bool IsLoadSensitivityTypesEnabled() const  |  Ottenere il flag che indica se le etichette di riservatezza di carico è abilitata.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per il caricamento di un motore esistente.

Parametri:  
* **engineId**: Impostare l'ID motore univoco generato da AddEngineAsync o su uno generato automaticamente. Quando si carica un motore esistente, usare nuovamente l'ID. In caso contrario verrà creato un nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **Facoltativo**: flag che indica quando viene caricato il motore deve caricare anche tipi sensibilità personalizzata, se verrà richiamato osservatore OnPolicyChange true nel profilo gli aggiornamenti per i tipi di sensibilità personalizzata, nonché le modifiche dei criteri. Se false ListSensitivityTypes chiama il metodo restituirà sempre un elenco vuoto.


  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [PolicyEngine::Settings](class_mip_policyengine_settings.md) per la creazione di un nuovo motore.

Parametri:  
* **identity**: [Identità](class_mip_identity.md) informazioni dell'utente associata al nuovo motore. 


* **clientData**: dati client personalizzabili che è possibile archiviare con il motore quando lo si scarica e recuperare da un motore caricato. 


* **locale**: l'output localizzabile del motore verrà fornito con queste impostazioni locali. 


* **Facoltativo**: flag che indica quando viene caricato il motore deve caricare anche tipi sensibilità personalizzata, se verrà richiamato osservatore OnPolicyChange true nel profilo gli aggiornamenti per i tipi di sensibilità personalizzata, nonché le modifiche dei criteri. Se false ListSensitivityTypes chiama il metodo restituirà sempre un elenco vuoto.


  
### <a name="getengineid-function"></a>GetEngineId (funzione)
Ottiene l'ID del motore.

  
**Restituisce**: Una stringa univoca che identifica il motore.
  
### <a name="setengineid-function"></a>SetEngineId (funzione)
Imposta l'ID del motore.

Parametri:  
* **id**: ID motore.


  
### <a name="getidentity-function"></a>Operazione GetIdentity (funzione)
Ottenere il [identità](class_mip_identity.md) oggetto.

  
**Restituisce**: Un riferimento all'identità nell'oggetto settings. 
  
**Vedere anche**: [MIP](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity (funzione)
Impostare il [identità](class_mip_identity.md) oggetto.

Parametri:  
* **identity**: identificatore univoco di un utente. 


  
**Vedere anche**: [MIP](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData (funzione)
Ottiene il set di dati client configurato nelle impostazioni.

  
**Restituisce**: Una stringa di dati specificati dal client.
  
### <a name="setclientdata-function"></a>SetClientData (funzione)
Imposta la stringa di dati client.

Parametri:  
* **clientData**: dati specificati dall'utente.


  
### <a name="getlocale-function"></a>GetLocale (funzione)
Ottiene le impostazioni locali configurate nelle impostazioni.

  
**Restituisce**: Le impostazioni locali.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri:  
* **customSettings**: Elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce**: Elenco di coppie nome/valore.
  
### <a name="setsessionid-function"></a>SetSessionId (funzione)
Imposta l'ID sessione, usato per la telemetria definita dal client.

Parametri:  
* **sessionId**: stringa univoca che connette gli eventi di telemetria.


  
### <a name="getsessionid-function"></a>GetSessionId (funzione)
Ottiene l'ID sessione, un identificatore univoco.

  
**Restituisce**: L'ID sessione.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (funzione)
Ottenere il flag che indica se le etichette di riservatezza di carico è abilitata.

  
**Restituisce**: True se abilitato in caso contrario false.
