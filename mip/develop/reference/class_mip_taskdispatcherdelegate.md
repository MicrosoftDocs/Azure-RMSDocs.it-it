---
title: 'Classe MIP:: TaskDispatcherDelegate'
description: 'Documenta la classe MIP:: taskdispatcherdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e73a03b842b1216bcc4ef71941ca4bc0b0233945
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559948"
---
# <a name="class-miptaskdispatcherdelegate"></a>Classe MIP:: TaskDispatcherDelegate 
Classe che definisce l'interfaccia per il dispatcher di attività dell'SDK MIP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String & taskId, std:: Function\<void ()\> attività)  |  Eseguire un'attività in un thread in background.
public void DispatchTask (const std:: String & taskId, std:: Function\<void ()\> Task, int64_t delaySeconds)  |  Eseguire un'attività in un thread in background con il ritardo specificato.
public void ExecuteTaskOnIndependentThread (const std:: String & taskId, std:: Function\<void ()\> attività)  |  Eseguire immediatamente un'attività su un thread indipendente.
public bool CancelTask (const std:: String & taskId)  |  Annulla un'attività in background.
public void CancelAllTasks ()  |  Annulla tutte le attività in background.
  
## <a name="members"></a>Membri
  
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