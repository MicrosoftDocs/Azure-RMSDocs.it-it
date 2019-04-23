---
title: class mip::TaskDispatcherDelegate
description: Documenta la classe mip::taskdispatcherdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 568a6df614370769556cd3634070e199beb4da5b
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184281"
---
# <a name="class-miptaskdispatcherdelegate"></a>class mip::TaskDispatcherDelegate 
Una classe che definisce l'interfaccia per il dispatcher attività MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask(const std::string& taskId, std::function\<void()\> task)  |  Eseguire un'attività in un thread in background.
public void DispatchTask(const std::string& taskId, std::function\<void()\> task, int64_t delay)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String & taskId, std:: Function\<void()\> attività)  |  Eseguire immediatamente un'attività su un thread indipendente.
public bool CancelTask (const std:: String & taskId)  |  Annullare un'attività in background.
public void CancelAllTasks()  |  Annullare tutte le attività in background.
  
## <a name="members"></a>Membri
  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background.

Parametri:  
* **taskId**: ID che identifica un'attività 


* **task**: Funzione da eseguire


  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background con il ritardo specificato.

Parametri:  
* **taskId**: ID che identifica un'attività 


* **task**: Funzione da eseguire 


* **ritardo**: Il ritardo (in secondi) prima dell'esecuzione attività


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread (funzione)
Eseguire immediatamente un'attività su un thread indipendente.

Parametri:  
* **taskId**: ID che identifica un'attività 


* **task**: Funzione da eseguire


  
### <a name="canceltask-function"></a>CancelTask (funzione)
Annullare un'attività in background.

Parametri:  
* **taskId**: ID dell'attività da annullare



  
**Restituisce**: True se l'attività è stata annullata correttamente, altrimenti false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks (funzione)
Annullare tutte le attività in background.