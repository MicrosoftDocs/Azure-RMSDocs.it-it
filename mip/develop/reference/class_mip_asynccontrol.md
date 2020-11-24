---
title: Classe AsyncControl
description: 'Documenta la classe AsyncControl:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7058ccdcac0133bc708a81d5e7342f61c48994f9
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567273"
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