---
title: Classe mip::PolicyProfile
description: Documenta la classe MIP::p olicyprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8feb0b93982a00c4843ea914f969ef27cf8e5ca2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560905"
---
# <a name="class-mippolicyprofile"></a>Classe mip::PolicyProfile 
La classe PolicyProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica richiederà solo un PolicyProfile, ma può creare più profili, se necessario.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: Vector\<std:: String\> ListEngines ()  |  Elenco dei motori.
public void UnloadEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void UnloadEngine (const std:: String & ID)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void AddEngineAsync (const PolicyEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public std:: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Aggiungere un nuovo motore di criteri al profilo.
public void DeleteEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Eliminare il motore dei criteri con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public static MIP_API void __CDECL MIP::P olicyProfile:: LoadAsync | Avvia il caricamento di un profilo in base alle impostazioni fornite.
public static const MIP_API char * __CDECL MIP::P olicyProfile:: GetVersion | Ottenere la versione della libreria

## <a name="members"></a>Membri
  
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


* **context**: parametro che verrà fowarded in modo opaco alle funzioni Observer e HttpDelegate facoltative. 


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

### <a name="loadasync-function"></a>LoadAsync (funzione)
Avvia il caricamento di un profilo in base alle impostazioni fornite.

Parametri:  
* **Settings (impostazioni**): impostazioni del profilo utilizzate per caricare l'oggetto profilo. </para>
* **context**: parametro di contesto che verrà passato nelle funzioni Observer.

### <a name="getversion-function"></a>GetVersion (funzione)
Ottenere la versione della libreria

**Restituisce**: stringa di versione.