---
title: 'Classe MIP:: MipContext'
description: 'Documenta la classe MIP:: mipcontext di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 20ce55ec371582ee16c70f311e0fc38ffc79d2fc
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070625"
---
# <a name="class-mipmipcontext"></a>Classe MIP:: MipContext 
MipContext rappresenta lo stato condiviso tra tutti i profili, i motori e i gestori.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
blocco public void ShutDown ()  |  Terminare MIP.
public bool IsFeatureEnabled (funzionalità FlightingFeature) const  |  Ottiene un valore che indica se una funzionalità è abilitata o meno.
public const ApplicationInfo& GetApplicationInfo() const  |  Ottenere la descrizione dell'applicazione.
public const std:: String & GetMipPath () const  |  Ottenere il percorso del file per log, cache e così via.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Ottiene l'implementazione del logger.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Ottiene l'implementazione del logger.
public static MIP_API std:: shared_ptr&lt;MipContext&gt; __CDECL MIP:: MipContext:: create | Creare una nuova istanza di MipContext da utilizzare durante l'inizializzazione dei profili.
public static MIP_API std:: shared_ptr&lt;MipContext&gt; __CDECL MIP:: MipContext:: CreateWithCustomFeatureSettings | Creare una nuova istanza di MipContext con le impostazioni delle funzionalità personalizzate.

## <a name="members"></a>Members
  
### <a name="shutdown-function"></a>Funzione ShutDown
Terminare MIP.
Questo metodo deve essere chiamato prima dell'arresto del processo/DLL
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled (funzione)
Ottiene un valore che indica se una funzionalità è abilitata o meno.

Parametri:  
* **funzionalità**: Funzionalità da abilitare/disabilitare



  
**Restituisce**: Se una funzionalità è abilitata o meno se un FeatureFlightingDelegate non è stato fornito da un'applicazione, verrà restituito sempre true.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo (funzione)
Ottenere la descrizione dell'applicazione.

  
**Restituisce**: Descrizione dell'applicazione
  
### <a name="getmippath-function"></a>GetMipPath (funzione)
Ottenere il percorso del file per log, cache e così via.

  
**Restituisce**: Percorso del file (con la directory foglia "MIP")
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (funzione)
Ottiene l'implementazione del logger.

  
**Restituisce**: Logger
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate (funzione)
Ottiene l'implementazione del logger.

**Restituisce**: Logger

### <a name="create-function"></a>Create (funzione)
Creare una nuova istanza di MipContext da utilizzare durante l'inizializzazione dei profili.

**Restituisce**: Istanza di MipContext.

### <a name="createwithcustomfeaturesettings-function"></a>CreateWithCustomFeatureSettings (funzione)
Creare una nuova istanza di MipContext con le impostazioni delle funzionalità personalizzate.

**Restituisce**: Istanza di MipContext.

