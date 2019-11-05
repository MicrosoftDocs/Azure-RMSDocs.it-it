---
title: 'Classe MIP:: HttpOperation'
description: 'Documenta la classe MIP:: httpoperation di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6f0c3cc726d72d89a8682907ebc350270db5daee
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558781"
---
# <a name="class-miphttpoperation"></a>Classe MIP:: HttpOperation 
Interfaccia che descrive una singola operazione HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID operazione.
public std:: shared_ptr\<HttpResponse\> GetResponse ()  |  Ottenere la risposta, se disponibile.
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