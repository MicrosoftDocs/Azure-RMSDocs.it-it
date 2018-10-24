---
title: Classe mip ProtectionProfile
description: Riferimento per la classe mip ProtectionProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7dffb4a6b1490ef185eb9a5062f394f4509f00a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446686"
---
# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
Un'applicazione deve creare un oggetto [ProtectionProfile](class_mip_protectionprofile.md) prima di eseguire qualsiasi operazione di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Avvia l'operazione di elenco motori.
public std::vector<std::string> ListEngines()  |  Elenco motori.
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
public std::shared_ptr<ProtectionEngine> AddEngine(const ProtectionEngine::Settings& settings)  |  Aggiunge un nuovo motore di protezione al profilo.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
 public void DeleteEngine(const std::string& engineId)  |  Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: [impostazioni](class_mip_protectionprofile_settings.md) usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="listengines"></a>ListEngines
Elenco motori.

  
**Restituisce**: ID dei motori memorizzati nella cache
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica le impostazioni del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="protectionengine"></a>ProtectionEngine
Aggiunge un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica le impostazioni del motore.



  
**Restituisce**: [ProtectionEngine](class_mip_protectionengine.md) appena creato
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="deleteengine"></a>DeleteEngine
Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore.

