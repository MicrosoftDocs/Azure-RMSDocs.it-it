---
title: Classe mip::ProtectionProfile
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: aa660990885356f887bb310e7049d166e3bdc190
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057494"
---
# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
Un'applicazione deve creare un oggetto [ProtectionProfile](class_mip_protectionprofile.md) prima di eseguire qualsiasi operazione di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.
public void ListEnginesAsync (const std::\<shared_ptr\>void & context)  |  Avvia l'operazione di elenco motori.
public std:: Vector\<std:: String\> ListEngines ()  |  Elenco motori.
public void AddEngineAsync (const ProtectionEngine:: Settings & Settings, const std:\<:\>shared_ptr void & context)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: Settings & Settings)  |  Aggiunge un nuovo motore di protezione al profilo.
public void DeleteEngineAsync (const std:: String & engineId, const std:\<:\>shared_ptr void & context)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: Contesto client che verrà passato in modo opaco agli osservatori


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco motori.

  
**Restituisce**: ID motore memorizzati nella cache
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica le impostazioni del motore. 


* **context**: Contesto client che verrà passato in modo opaco agli osservatori


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="addengine-function"></a>AddEngine (funzione)
Aggiunge un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica le impostazioni del motore.



  
**Restituisce**: [ProtectionEngine](class_mip_protectionengine.md) appena creato
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: Contesto client che verrà passato in modo opaco agli osservatori


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore.

