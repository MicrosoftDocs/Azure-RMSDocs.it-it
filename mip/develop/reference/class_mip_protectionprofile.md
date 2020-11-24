---
title: Classe ProtectionProfile
description: 'Documenta la classe protectionprofile:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a783a90b64d5829632e2104ff2706fd86a0d9e68
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567107"
---
# <a name="class-protectionprofile"></a>Classe ProtectionProfile 
ProtectionProfile è la classe radice per l'esecuzione di operazioni di protezione.
Un'applicazione deve creare un oggetto ProtectionProfile prima di eseguire qualsiasi operazione di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.
public std:: shared_ptr \<AsyncControl\> ListEnginesAsync (const std:: shared_ptr \<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: Vector \<std::string\> ListEngines ()  |  Elenco motori.
public std:: shared_ptr \<AsyncControl\> AddEngineAsync (const ProtectionEngine:: settings& Settings, const std:: shared_ptr \<void\>& context)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
public std::shared_ptr\<ProtectionEngine\> AddEngine(const ProtectionEngine::Settings& settings)  |  Aggiunge un nuovo motore di protezione al profilo.
public std:: shared_ptr \<AsyncControl\> DeleteEngineAsync (const std:: string& engineId, const std:: shared_ptr \<void\>& context)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la durata
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri  
* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer



  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato ProtectionProfile::Observer.
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco motori.

  
**Restituisce**: ID dei motori memorizzati nella cache
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri  
* **settings**: oggetto mip::ProtectionEngine::Settings che specifica le impostazioni del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer



  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato ProtectionProfile::Observer.
  
### <a name="addengine-function"></a>AddEngine (funzione)
Aggiunge un nuovo motore di protezione al profilo.

Parametri  
* **settings**: oggetto mip::ProtectionEngine::Settings che specifica le impostazioni del motore.



  
**Restituisce**: ProtectionEngine appena creato
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri  
* **ID**: ID univoco del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer



  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato ProtectionProfile::Observer.
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri  
* **ID**: ID univoco del motore.

