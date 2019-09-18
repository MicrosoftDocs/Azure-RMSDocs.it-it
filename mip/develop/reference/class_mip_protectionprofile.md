---
title: Classe mip::ProtectionProfile
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: dcd50c403f20486e479fc00016ed6c0ef8885efa
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070507"
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
public static MIP_API void __CDECL MIP::P rotectionProfile:: LoadAsync | Impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata
public static MIP_API std:: shared_ptr&lt;ProtectionProfile&gt; __CDECL MIP::P rotectionprofile:: Load | Caricamento di un profilo in base alle impostazioni fornite.
public static const MIP_API char * __CDECL MIP::P rotectionProfile:: GetVersion | Ottiene la versione della libreria.
public static MIP_API std:: shared_ptr&lt;PublishingLicenseInfo&gt; __CDECL MIP::P rotectionprofile:: GetPublishingLicenseInfo | Crea un contenitore per i dettagli di una licenza di pubblicazione e può essere utilizzato per creare un gestore di protezione. 


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

### <a name="loadasync-function"></a>LoadAsync (funzione)
Impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata 

In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).

Parametri:
* **Impostazioni**: Impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.
* **context**: Lo stesso contesto verrà inviato a ProtectionProfile:: Observer:: OnLoadSuccess o ProtectionProfile:: Observer:: OnLoadFailure così com'è.

### <a name="load-function"></a>Load (funzione)
Caricamento di un profilo in base alle impostazioni fornite.

In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).

Parametri:
* **Impostazioni**: Impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.

**Restituisce**: Profilo appena creato.

### <a name="getversion-function"></a>GetVersion (funzione)
Ottiene la versione della libreria. 

**Restituisce**: Versione della libreria.

### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo (funzione)
Crea un contenitore per i dettagli di una licenza di pubblicazione e può essere utilizzato per creare un gestore di protezione. 

Parametri:
* **serializedPublishingLicense**: Licenza di pubblicazione serializzata..

**Restituisce**: Un titolare per i dettagli di una licenza di pubblicazione 
