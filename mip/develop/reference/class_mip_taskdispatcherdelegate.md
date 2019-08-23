---
title: 'Classe MIP:: TaskDispatcherDelegate'
description: 'Documenta la classe MIP:: taskdispatcherdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 0455f446cddd7db1c05f0f7e7b76b33496810cf1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883015"
---
# <a name="class-miptaskdispatcherdelegate"></a>Classe MIP:: TaskDispatcherDelegate 
Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String & taskId, std::\<Function void (\> ) Task)  |  Eseguire un'attività in un thread in background.
public void DispatchTask (const std:: String & taskId, std::\<Function void (\> ) Task, int64_t delay)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String & taskId, std::\<Function void (\> ) Task)  |  Eseguire immediatamente un'attività su un thread indipendente.
public bool CancelTask (const std:: String & taskId)  |  Annulla un'attività in background.
public void CancelAllTasks()  |  Annulla tutte le attività in background.
  
## <a name="members"></a>Members
  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background.

Parametri:  
* **taskId**: ID per identificare in modo univoco un'attività 


* **attività**: Funzione da eseguire


  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background con il ritardo specificato.

Parametri:  
* **taskId**: ID per identificare in modo univoco un'attività 


* **attività**: Funzione da eseguire 


* **ritardo**: Ritardo (in secondi) prima dell'esecuzione dell'attività


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread (funzione)
Eseguire immediatamente un'attività su un thread indipendente.

Parametri:  
* **taskId**: ID per identificare in modo univoco un'attività 


* **attività**: Funzione da eseguire


  
### <a name="canceltask-function"></a>CancelTask (funzione)
Annulla un'attività in background.

Parametri:  
* **taskId**: ID dell'attività da annullare



  
**Restituisce**: True se l'attività è stata annullata correttamente; in caso contrario, false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks (funzione)
Annulla tutte le attività in background.