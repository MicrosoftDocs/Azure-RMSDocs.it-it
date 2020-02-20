---
title: 'Classe MIP:: HttpOperation'
description: 'Documenta la classe MIP:: httpoperation di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 4be7b54dd5df255c488043d84ebcfebbce7e6ac2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489997"
---
# <a name="class-miphttpoperation"></a>Classe MIP:: HttpOperation 
Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID operazione.
public std:: shared_ptr\<HttpResponse\> GetResponse ()  |  Ottenere la risposta, se disponibile.
public bool annullato ()  |  Ottenere lo stato di annullamento dell'operazione.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID operazione.

  
**Restituisce**: ID operazione i cui HttpRequest e HttpResponse corrispondenti avranno lo stesso ID
  
### <a name="getresponse-function"></a>GetResponse (funzione)
Ottenere la risposta, se disponibile.

  
**Restituisce**: risposta
  
### <a name="iscancelled-function"></a>Funzione annullata
Ottenere lo stato di annullamento dell'operazione.

  
**Restituisce**: stato di annullamento