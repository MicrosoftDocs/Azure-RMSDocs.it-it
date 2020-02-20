---
title: 'Classe MIP:: TaskDispatcherDelegate'
description: 'Documenta la classe MIP:: taskdispatcherdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: dca6a5fa04b62abf23f0116f63fd4a91c6081da0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489334"
---
# <a name="class-miptaskdispatcherdelegate"></a>Classe MIP:: TaskDispatcherDelegate 
Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String & taskId, std:: Function\<void ()\> attività)  |  Eseguire un'attività in un thread in background.
public void DispatchTask (const std:: String & taskId, std:: Function\<void ()\> Task, int64_t delaySeconds)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String & taskId, std:: Function\<void ()\> attività)  |  Eseguire immediatamente un'attività su un thread indipendente.
public bool CancelTask (const std:: String & taskId)  |  Annulla un'attività in background.
public void CancelAllTasks()  |  Annulla tutte le attività in background.
  
## <a name="members"></a>Members
  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background.

Parametri:  
* **taskId**: ID per identificare in modo univoco un'attività 


* **Task**: funzione da eseguire


  
### <a name="dispatchtask-function"></a>DispatchTask (funzione)
Eseguire un'attività in un thread in background con il ritardo specificato.

Parametri:  
* **taskId**: ID per identificare in modo univoco un'attività 


* **Task**: funzione da eseguire 


* **delaySeconds**: ritardo (in secondi) prima dell'esecuzione dell'attività


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread (funzione)
Eseguire immediatamente un'attività su un thread indipendente.

Parametri:  
* **taskId**: ID per identificare in modo univoco un'attività 


* **Task**: funzione da eseguire


  
### <a name="canceltask-function"></a>CancelTask (funzione)
Annulla un'attività in background.

Parametri:  
* **taskId**: ID dell'attività da annullare



  
**Restituisce**: true se l'attività è stata annullata correttamente; in caso contrario, false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks (funzione)
Annulla tutte le attività in background.