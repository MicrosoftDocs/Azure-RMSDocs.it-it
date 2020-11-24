---
title: Classe HttpOperation
description: 'Documenta la classe httpoperation:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ece0d76577747170e4328bc1d9bdabb0678e65a5
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566880"
---
# <a name="class-httpoperation"></a>Classe HttpOperation 
Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID operazione.
public std:: shared_ptr \<HttpResponse\> GetResponse ()  |  Ottenere la risposta, se disponibile.
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