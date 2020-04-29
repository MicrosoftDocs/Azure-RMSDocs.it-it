---
title: Classe PolicyProfile
description: 'Documenta la classe policyprofile:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 9f70b8bfa1eee6e994b67c668b5144d6cb74ecad
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760899"
---
# <a name="class-policyprofile"></a>Classe PolicyProfile 
PolicyProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo PolicyProfile, ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std::\<shared_ptr\> void& context)  |  Avvia l'operazione di elenco motori.
public std:: Vector\<std:: String\> ListEngines ()  |  Elenco dei motori.
public std:: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std:: String& ID, const std:\<:\> shared_ptr void& context)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void UnloadEngine (const std:: String& ID)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const PolicyEngine:: Settings& Settings, const std:\<:\> shared_ptr void& context)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public std:: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine:: Settings& Settings, const std:\<:\> shared_ptr void& context)  |  Aggiungere un nuovo motore di criteri al profilo.
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: String& ID, const std:\<:\> shared_ptr void& context)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Eliminare il motore dei criteri con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public void AcquireAuthToken (Cloud Cloud, const std::\<shared_ptr\> AuthDelegate& AuthDelegate) const  |  Attiva un callback di autenticazione.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni configurate nel profilo.

  
**Restituisce**: impostazioni configurate nel profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri  
* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato PolicyProfile::Observer.
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco dei motori.

  
**Restituisce**: ID dei motori memorizzati nella cache
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri  
* **ID**: ID univoco del motore. 


* **context**: parametro che verrà inoltrato in modo non trasparente alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato PolicyProfile::Observer.
  
### <a name="unloadengine-function"></a>UnloadEngine (funzione)
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri  
* **ID**: ID univoco del motore.


  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore dei criteri al profilo.

Parametri  
* **settings**: oggetto mip::PolicyEngine::Settings che specifica le impostazioni del motore. 


* **context**: parametro che verrà trasmesso in modo opaco alle funzioni Observer e HttpDelegate facoltative. 


In base all'esito positivo o negativo dell'operazione verrà chiamato PolicyProfile::Observer.
  
### <a name="addengine-function"></a>AddEngine (funzione)
Aggiungere un nuovo motore di criteri al profilo.

Parametri  
* **settings**: oggetto mip::PolicyEngine::Settings che specifica le impostazioni del motore. 


* **context**: parametro che verrà trasmesso in modo opaco al HttpDelegate facoltativo



  
**Restituisce**: PolicyEngine appena creato
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.

Parametri  
* **ID**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato PolicyProfile::Observer.
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Eliminare il motore dei criteri con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri  
* **ID**: ID univoco del motore.


  
### <a name="acquireauthtoken-function"></a>AcquireAuthToken (funzione)
Attiva un callback di autenticazione.

Parametri  
* **cloud**: cloud di Azure 


* **authDelegate**: callback di autenticazione che verrà richiamato


MIP non memorizza nella cache o non esegue altre operazioni con il valore restituito dal delegato di autenticazione. Questa funzione è consigliata per le applicazioni che non sono "connesse" fino a quando MIP richiede un token di autenticazione. Consente a un'applicazione di recuperare un token prima che MIP ne richieda effettivamente uno.