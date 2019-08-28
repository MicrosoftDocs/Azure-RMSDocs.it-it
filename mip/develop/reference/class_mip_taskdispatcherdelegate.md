---
title: 'Classe MIP:: TaskDispatcherDelegate'
description: 'Documenta la classe MIP:: taskdispatcherdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d5237bf999f7ad704fd303783a9fbdc506b58ed2
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056765"
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