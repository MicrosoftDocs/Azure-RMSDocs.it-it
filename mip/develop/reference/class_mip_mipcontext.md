---
title: Classe MipContext
description: 'Documenta la classe mipcontext:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: cf191a1e770d13d84603fe593d63dedb98bbb14b
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761460"
---
# <a name="class-mipcontext"></a>Classe MipContext 
MipContext rappresenta lo stato condiviso tra tutti i profili, i motori e i gestori.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
blocco public void ShutDown ()  |  Terminare MIP.
public bool IsFeatureEnabled (funzionalità FlightingFeature) const  |  Ottiene un valore che indica se una funzionalità è abilitata o meno.
public const ApplicationInfo& GetApplicationInfo() const  |  Ottenere la descrizione dell'applicazione.
public const std:: String& GetMipPath () const  |  Ottenere il percorso del file per log, cache e così via.
public bool IsOfflineOnly ()  |  Ottiene l'impostazione solo offline.
public LogLevel GetThresholdLogLevel () const  |  Ottenere il livello di registrazione della soglia.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Ottiene l'implementazione del logger.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Ottiene l'implementazione del logger.
public const std::\<map FlightingFeature,\> bool& GetFlightingFeatures () const  |  Ottiene il set di funzionalità di Flight.
  
## <a name="members"></a>Members
  
### <a name="shutdown-function"></a>Funzione ShutDown
Terminare MIP.
Questo metodo deve essere chiamato prima dell'arresto del processo/DLL
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled (funzione)
Ottiene un valore che indica se una funzionalità è abilitata o meno.

Parametri  
* **funzionalità**: funzionalità da abilitare/disabilitare



  
**Restituisce**un valore che indica se una funzionalità è abilitata se un FeatureFlightingDelegate non è stato fornito da un'applicazione. verrà restituito sempre true.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo (funzione)
Ottenere la descrizione dell'applicazione.

  
**Restituisce**: Descrizione dell'applicazione
  
### <a name="getmippath-function"></a>GetMipPath (funzione)
Ottenere il percorso del file per log, cache e così via.

  
**Restituisce**: percorso file (con la directory foglia "MIP")
  
### <a name="isofflineonly-function"></a>IsOfflineOnly (funzione)
Ottiene l'impostazione solo offline.

  
**Restituisce**: indipendentemente dal fatto che l'applicazione sia in esecuzione in modalità solo offline
  
### <a name="getthresholdloglevel-function"></a>GetThresholdLogLevel (funzione)
Ottenere il livello di registrazione della soglia.

  
**Restituisce**: livello di log soglia
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (funzione)
Ottiene l'implementazione del logger.

  
**Restituisce**: logger
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate (funzione)
Ottiene l'implementazione del logger.

  
**Restituisce**: logger
  
### <a name="getflightingfeatures-function"></a>GetFlightingFeatures (funzione)
Ottiene il set di funzionalità di Flight.

  
**Returns**: mappa delle funzionalità di volo