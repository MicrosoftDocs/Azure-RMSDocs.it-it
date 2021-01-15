---
title: Classe TaskDispatcherDelegate
description: 'Documenta la classe taskdispatcherdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: f8f84b51200ff630b6158f7b02ca88e2a3d21e25
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212876"
---
# <a name="class-taskdispatcherdelegate"></a>Classe TaskDispatcherDelegate 
Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String& taskId, std:: Function \<void()\> Task)  |  Eseguire un'attività in un thread in background.
public void DispatchTask (const std:: String& taskId, std:: Function \<void()\> Task, Int64_t delaySeconds)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String& taskId, std:: Function \<void()\> Task)  |  Eseguire immediatamente un'attività su un thread indipendente.
public bool CancelTask (const std:: String& taskId)  |  Annulla un'attività in background.
public void CancelAllTasks ()  |  Annulla tutte le attività in background.
  
## <a name="members"></a>Membri
  
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