---
title: 'Classe MIP:: HttpOperation'
description: 'Documenta la classe MIP:: httpoperation di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 8503a5466fe180fc6831e85e1b53954ba99f55c7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884118"
---
# <a name="class-miphttpoperation"></a>Classe MIP:: HttpOperation 
Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID operazione.
public std:: shared_ptr\<HttpResponse\> GetResponse ()  |  Ottenere la risposta, se disponibile.
public bool annullato ()  |  Ottenere lo stato di annullamento dell'operazione.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID operazione.

  
**Restituisce**: ID operazione i corrispondenti HttpRequest e HttpResponse avranno lo stesso ID
  
### <a name="getresponse-function"></a>GetResponse (funzione)
Ottenere la risposta, se disponibile.

  
**Restituisce**: Risposta
  
### <a name="iscancelled-function"></a>Funzione annullata
Ottenere lo stato di annullamento dell'operazione.

  
**Restituisce**: Stato di annullamento