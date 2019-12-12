---
title: Classe mip::ProtectionProfile
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a6c78e7311f3af3920df19d7a3a6ca92bb09e819
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560065"
---
# <a name="class-mipprotectionprofile"></a>Classe mip::ProtectionProfile 
ProtectionProfile è la classe radice per l'esecuzione di operazioni di protezione.
Prima di eseguire qualsiasi operazione di protezione, un'applicazione deve creare un ProtectionProfile
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: Vector\<std:: String\> ListEngines ()  |  Elenco motori.
public void AddEngineAsync (const ProtectionEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Avvia l'aggiunta di un nuovo motore di protezione al profilo.
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: Settings & Settings)  |  Aggiunge un nuovo motore di protezione al profilo.
public void DeleteEngineAsync (const std:: String & engineId, const std:: shared_ptr\<void\>& context)  |  Avvia l'eliminazione del motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public void DeleteEngine(const std::string& engineId)  |  Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.
public static MIP_API void __CDECL MIP::P rotectionProfile:: LoadAsync | Impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata
public static MIP_API std:: shared_ptr&lt;ProtectionProfile&gt; __CDECL MIP::P rotectionProfile:: Load | Caricamento di un profilo in base alle impostazioni fornite.
public static const MIP_API char * __CDECL MIP::P rotectionProfile:: GetVersion | Ottiene la versione della libreria.
public static MIP_API std:: shared_ptr&lt;PublishingLicenseInfo&gt; __CDECL MIP::P rotectionProfile:: GetPublishingLicenseInfo | Crea un contenitore per i dettagli di una licenza di pubblicazione e può essere utilizzato per creare un gestore di protezione. 

## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.

  
**Restituisce**: impostazioni utilizzate da ProtectionProfile durante l'inizializzazione e per tutta la durata
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer


ProtectionProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="listengines-function"></a>ListEngines (funzione)
Elenco motori.

  
**Restituisce**: ID dei motori memorizzati nella cache
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di protezione al profilo.

Parametri:  
* **Settings**: oggetto mip::P rotectionengine:: Settings che specifica le impostazioni del motore. 


* **context**: contesto client che verrà nuovamente passato in maniera opaca agli observer


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


ProtectionProfile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="deleteengine-function"></a>DeleteEngine (funzione)
Elimina il motore di protezione con l'ID specificato. Tutti i dati per il motore specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore.

### <a name="loadasync-function"></a>LoadAsync (funzione)
Impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata 

In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).

Parametri:
* **Impostazioni**: impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.
* **contesto**: lo stesso contesto verrà inviato a ProtectionProfile:: Observer:: OnLoadSuccess o ProtectionProfile:: Observer:: OnLoadFailure così com'è.

### <a name="load-function"></a>Load (funzione)
Caricamento di un profilo in base alle impostazioni fornite.

In base all'esito positivo o negativo dell'operazione verrà chiamato [ProtectionProfile::Observer](class_mip_protectionprofile_observer.md).

Parametri:
* **Impostazioni**: impostazioni usate da ProtectionProfile durante l'inizializzazione e per tutta la sua durata.

**Restituisce**: profilo appena creato.

### <a name="getversion-function"></a>GetVersion (funzione)
Ottiene la versione della libreria. 

**Restituisce**: versione della libreria.

### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo (funzione)
Crea un contenitore per i dettagli di una licenza di pubblicazione e può essere utilizzato per creare un gestore di protezione. 

Parametri:
* **serializedPublishingLicense**: licenza di pubblicazione serializzata..

**Restituisce**: un proprietario per i dettagli di una licenza di pubblicazione 