---
title: 'Classe MIP:: AsyncControl'
description: 'Documenta la classe MIP:: AsyncControl di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: afef25cef1363d5275581a774279c97d61239f4b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77492767"
---
# <a name="class-mipasynccontrol"></a>Classe MIP:: AsyncControl 
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