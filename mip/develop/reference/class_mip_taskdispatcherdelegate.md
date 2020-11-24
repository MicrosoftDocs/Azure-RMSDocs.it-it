---
title: Classe TaskDispatcherDelegate
description: 'Documenta la classe taskdispatcherdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 057ba0d4de58ab4dedf8d3e2f8b2a42b0e5f969a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567032"
---
# <a name="class-taskdispatcherdelegate"></a>Classe TaskDispatcherDelegate 
Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String& taskId, std:: Function \<void()\> Task)  |  Eseguire un'attività in un thread in background.
public void DispatchTask (const std:: String& taskId, std:: Function \<void()\> Task, Int64_t delaySeconds)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String& taskId, std:: Function \<void()\> Task)  |  Eseguire immediatamente un'attività su un thread indipendente.
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