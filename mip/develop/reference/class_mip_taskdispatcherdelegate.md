---
title: Classe TaskDispatcherDelegate
description: 'Documenta la classe taskdispatcherdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b7cd2267b795540a8bb4035a695f5b34f0580b87
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764290"
---
# <a name="class-taskdispatcherdelegate"></a>Classe TaskDispatcherDelegate 
Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String& taskId, std::\<Function void (\> ) Task)  |  Eseguire un'attività in un thread in background.
public void DispatchTask (const std:: String& taskId, std::\<Function void (\> ) Task, int64_t delaySeconds)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String& taskId, std::\<Function void (\> ) Task)  |  Eseguire immediatamente un'attività su un thread indipendente.
public bool CancelTask (const std:: String& taskId)  |  Annulla un'attività in background.
public void CancelAllTasks ()  |  Annulla tutte le attività in background.
  
## <a name="members"></a>Members
  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background.

Parametri  
* **taskId**: ID per identificare in modo univoco un'attività 


* **Task**: funzione da eseguire


  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background con il ritardo specificato.

Parametri  
* **taskId**: ID per identificare in modo univoco un'attività 


* **Task**: funzione da eseguire 


* **delaySeconds**: ritardo (in secondi) prima dell'esecuzione dell'attività


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread (funzione)
Eseguire immediatamente un'attività su un thread indipendente.

Parametri  
* **taskId**: ID per identificare in modo univoco un'attività 


* **Task**: funzione da eseguire


  
### <a name="canceltask-function"></a>CancelTask (funzione)
Annulla un'attività in background.

Parametri  
* **taskId**: ID dell'attività da annullare



  
**Restituisce**: true se l'attività è stata annullata correttamente; in caso contrario, false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks (funzione)
Annulla tutte le attività in background.