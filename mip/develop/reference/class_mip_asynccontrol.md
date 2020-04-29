---
title: Classe AsyncControl
description: 'Documenta la classe AsyncControl:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d032abf9fe7192cfe6ccfd5890d6585aaa2ba645
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763665"
---
# <a name="class-asynccontrol"></a>Classe AsyncControl 
Classe utilizzata per annullare l'operazione asincrona.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public bool Cancel ()  |  Se si chiama Annulla si tenterà di annullare l'attività, in caso di esito positivo verrà chiamato il callback OnFailure appropriato con MIP:: OperationCancelledError. Questa funzionalità dipende dal delegato del dispatcher di attività (.
  
## <a name="members"></a>Members
  
### <a name="cancel-function"></a>Annulla funzione
Se si chiama Annulla si tenterà di annullare l'attività, in caso di esito positivo verrà chiamato il callback OnFailure appropriato con MIP:: OperationCancelledError. Questa funzionalità dipende dal delegato del dispatcher di attività (.
  
**Vedere anche**: MIP:: TaskDispatcherDelegate),

  
**Restituisce**: false se non è possibile inviare il segnale di annullamento, true in caso contrario.
Non contengono un riferimento sicuro a un oggetto AsyncControl in un blocco di completamento dell'attività.