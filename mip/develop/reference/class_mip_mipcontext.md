---
title: 'Classe MIP:: MipContext'
description: 'Documenta la classe MIP:: mipcontext di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f6bc8d5a61ec259b85ae9e2479afeb9a2f00412f
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054571"
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