---
title: Classe mip::ProtectionProfile
description: 'Classe MIP:: protectionprofile di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d789250d2ab91ca6e65181e216f260db8d44d496
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184366"
---
# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) è la classe radice per l'esecuzione di operazioni di protezione.
Un'applicazione deve creare un oggetto [ProtectionProfile](class_mip_protectionprofile.md) prima di eseguire qualsiasi operazione di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& contesto)  |  Avvia l'operazione di elenco motori.
Public std:: Vector\<std:: String\> ListEngines()  |  Elenco motori.
pubblica AddEngineAsync void (ProtectionEngine::Settings const & impostazioni, const std:: shared_ptr\<void\>& contesto)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
Public std:: shared_ptr\<ProtectionEngine\> AddEngine (ProtectionEngine::Settings const & impostazioni)  |  Aggiunge un nuovo motore di protezione al profilo.
public void DeleteEngineAsync (const std:: String & engineId, const std:: shared_ptr\<void\>& contesto)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni usate da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante l'inizializzazione e per tutta la sua durata
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: Contesto di client che verrà passato in maniera opaca all'Observer


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco motori.

  
**Restituisce**: Gli ID di motore memorizzato nella cache
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica le impostazioni del motore. 


* **context**: Contesto di client che verrà passato in maniera opaca all'Observer


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="addengine-function"></a>AddEngine (funzione)
Aggiunge un nuovo motore di protezione al profilo.

Parametri:  
* **settings**: oggetto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) che specifica le impostazioni del motore.



  
**Restituisce**: Appena creati [ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: Contesto di client che verrà passato in maniera opaca all'Observer


In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore.

