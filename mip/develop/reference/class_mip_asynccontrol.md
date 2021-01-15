---
title: Classe AsyncControl
description: 'Documenta la classe AsyncControl:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 7d21002c9bf90014a57eeb9b666f706e2b41f68d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212213"
---
# <a name="class-asynccontrol"></a>Classe AsyncControl 
Classe utilizzata per annullare l'operazione asincrona.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public bool Cancel ()  |  Se si chiama Annulla si tenterà di annullare l'attività, in caso di esito positivo verrà chiamato il callback OnFailure appropriato con MIP:: OperationCancelledError. Questa funzionalità dipende dal delegato del dispatcher di attività (.
  
## <a name="members"></a>Membri
  
### <a name="cancel-function"></a>Annulla funzione
Se si chiama Annulla si tenterà di annullare l'attività, in caso di esito positivo verrà chiamato il callback OnFailure appropriato con MIP:: OperationCancelledError. Questa funzionalità dipende dal delegato del dispatcher di attività (.
  
**Vedere anche**: MIP:: TaskDispatcherDelegate),

  
**Restituisce**: false se non è possibile inviare il segnale di annullamento, true in caso contrario.
Non contengono un riferimento sicuro a un oggetto AsyncControl in un blocco di completamento dell'attività.