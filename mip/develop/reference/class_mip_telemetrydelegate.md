---
title: Classe TelemetryDelegate
description: 'Documenta la classe telemetrydelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 40e9c3a695f70af8051ef2a6e89ad232a7c09f54
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225052"
---
# <a name="class-telemetrydelegate"></a>Classe TelemetryDelegate 
Classe che definisce l'interfaccia per le notifiche di controllo/telemetria del MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void WriteEvent (const std:: shared_ptr \<TelemetryEvent\>& Event)  |  Registrare un evento di diagnostica.
public void Flush()  |  Scarica tutti gli eventi in coda (ad esempio, a causa dell'arresto)
  
## <a name="members"></a>Membri
  
### <a name="writeevent-function"></a>WriteEvent (funzione)
Registrare un evento di diagnostica.

Parametri  
* **evento**: evento da registrare


  
### <a name="flush-function"></a>Flush (funzione)
Scarica tutti gli eventi in coda (ad esempio, a causa dell'arresto)