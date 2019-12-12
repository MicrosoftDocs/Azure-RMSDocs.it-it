---
title: 'Classe MIP:: MipContext'
description: 'Documenta la classe MIP:: mipcontext di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9efbe9330014458a26f62e4dfac9ea24ad5d4475
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73561025"
---
# <a name="class-mipmipcontext"></a>Classe MIP:: MipContext 
MipContext rappresenta lo stato condiviso tra tutti i profili, i motori e i gestori.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
blocco public void ShutDown ()  |  Terminare MIP.
public bool IsFeatureEnabled (funzionalità FlightingFeature) const  |  Ottiene un valore che indica se una funzionalità è abilitata o meno.
public const ApplicationInfo& GetApplicationInfo() const  |  Ottenere la descrizione dell'applicazione.
public const std:: String & GetMipPath () const  |  Ottenere il percorso del file per log, cache e così via.
public bool IsOfflineOnly ()  |  Ottiene l'impostazione solo offline.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Ottiene l'implementazione del logger.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Ottiene l'implementazione del logger.
public static MIP_API std:: shared_ptr&lt;MipContext&gt; __CDECL MIP:: MipContext:: create | Creare una nuova istanza di MipContext da utilizzare durante l'inizializzazione dei profili.
public static MIP_API std:: shared_ptr&lt;MipContext&gt; __CDECL MIP:: MipContext:: CreateWithCustomFeatureSettings | Creare una nuova istanza di MipContext con le impostazioni delle funzionalità personalizzate.

## <a name="members"></a>Membri
  
### <a name="shutdown-function"></a>Funzione ShutDown
Terminare MIP.
Questo metodo deve essere chiamato prima dell'arresto del processo/DLL
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled (funzione)
Ottiene un valore che indica se una funzionalità è abilitata o meno.

Parametri:  
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
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (funzione)
Ottiene l'implementazione del logger.

  
**Restituisce**: logger
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate (funzione)
Ottiene l'implementazione del logger.

  
**Restituisce**: logger

### <a name="create-function"></a>Funzione Create
Creare una nuova istanza di MipContext da utilizzare durante l'inizializzazione dei profili.

**Restituisce**: istanza di MipContext.

### <a name="createwithcustomfeaturesettings-function"></a>CreateWithCustomFeatureSettings (funzione)
Creare una nuova istanza di MipContext con le impostazioni delle funzionalità personalizzate.

**Restituisce**: istanza di MipContext.