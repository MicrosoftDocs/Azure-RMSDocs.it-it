---
title: Classe HttpOperation
description: 'Documenta la classe httpoperation:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 7ceb76ff61ce13fd47b764fa336ffcf5e167608e
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211516"
---
# <a name="class-httpoperation"></a>Classe HttpOperation 
Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID operazione.
public std:: shared_ptr \<HttpResponse\> GetResponse ()  |  Ottenere la risposta, se disponibile.
public bool annullato ()  |  Ottenere lo stato di annullamento dell'operazione.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID operazione.

  
**Restituisce**: ID operazione i cui HttpRequest e HttpResponse corrispondenti avranno lo stesso ID
  
### <a name="getresponse-function"></a>GetResponse (funzione)
Ottenere la risposta, se disponibile.

  
**Restituisce**: risposta
  
### <a name="iscancelled-function"></a>Funzione annullata
Ottenere lo stato di annullamento dell'operazione.

  
**Restituisce**: stato di annullamento