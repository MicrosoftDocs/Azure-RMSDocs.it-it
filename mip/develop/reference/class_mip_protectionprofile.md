---
title: Classe mip::ProtectionProfile
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 14d52de8ff87a75aaf2c777eb55c427bbde72a12
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486733"
---
# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
ProtectionProfile è la classe radice per l'esecuzione di operazioni di protezione.
Prima di eseguire qualsiasi operazione di protezione, un'applicazione deve creare un ProtectionProfile
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: Vector\<std:: String\> ListEngines ()  |  Elenco motori.
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const ProtectionEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: Settings & Settings)  |  Aggiunge un nuovo motore di protezione al profilo.
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: String & engineId, const std:: shared_ptr\<void\>& context)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la durata
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer



  
**Restituisce**: oggetto controllo asincrono.
ProtectionProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco motori.

  
**Restituisce**: ID dei motori memorizzati nella cache
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri:  
* **Settings**: oggetto mip::P rotectionengine:: Settings che specifica le impostazioni del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer



  
**Restituisce**: oggetto controllo asincrono.
ProtectionProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="addengine-function"></a>AddEngine (funzione)
Aggiunge un nuovo motore di protezione al profilo.

Parametri:  
* **Settings**: oggetto mip::P rotectionengine:: Settings che specifica le impostazioni del motore.



  
**Restituisce**: ProtectionEngine appena creato
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer



  
**Restituisce**: oggetto controllo asincrono.
ProtectionProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore.

