---
title: Classe mip::PolicyProfile
description: Documenta la classe MIP::p olicyprofile dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 515f780c269025175e99caed72e8da381ef88104
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489776"
---
# <a name="class-mippolicyprofile"></a>Classe mip::PolicyProfile 
La classe PolicyProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica richiederà solo un PolicyProfile, ma può creare più profili, se necessario.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: Vector\<std:: String\> ListEngines ()  |  Elenco dei motori.
public std:: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void UnloadEngine (const std:: String & ID)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const PolicyEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public std:: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Aggiungere un nuovo motore di criteri al profilo.
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Eliminare il motore dei criteri con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni configurate nel profilo.

  
**Restituisce**: impostazioni configurate nel profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: parametro che verrà passato alle funzioni observer. 


PolicyProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco dei motori.

  
**Restituisce**: ID dei motori memorizzati nella cache
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà inoltrato in modo non trasparente alle funzioni observer. 


PolicyProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="unloadengine-function"></a>UnloadEngine (funzione)
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri:  
* **id**: ID univoco del motore.


  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore dei criteri al profilo.

Parametri:  
* **Settings**: oggetto mip::P olicyengine:: Settings che specifica le impostazioni del motore. 


* **context**: parametro che verrà trasmesso in modo opaco alle funzioni Observer e HttpDelegate facoltative. 


PolicyProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="addengine-function"></a>AddEngine (funzione)
Aggiungere un nuovo motore di criteri al profilo.

Parametri:  
* **Settings**: oggetto mip::P olicyengine:: Settings che specifica le impostazioni del motore. 


* **context**: parametro che verrà trasmesso in modo opaco al HttpDelegate facoltativo



  
**Restituisce**: PolicyEngine appena creato
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


PolicyProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Eliminare il motore dei criteri con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore.

