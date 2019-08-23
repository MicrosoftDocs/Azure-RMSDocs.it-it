---
title: Classe mip::HttpResponse
description: 'Documenta la classe MIP:: HttpResponse di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 4d7711f755f4ffde923eb7d913abdb5bd2a905db
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884137"
---
# <a name="class-miphttpresponse"></a>Classe mip::HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID risposta.
public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
public const std::\<vector\>uint8_t & GetBody () const  |  Ottiene il corpo della richiesta.
public const std::\<map std:: String, std:: String,\>CaseInsensitiveComparator & GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID risposta.

  
**Restituisce**: ID risposta il cui HttpRequest corrispondente avrà lo stesso ID
  
### <a name="getstatuscode-function"></a>GetStatusCode (funzione)
Ottiene il codice di stato della risposta.

  
**Restituisce**: status code
  
### <a name="getbody-function"></a>Funzione GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: Corpo della richiesta
  
### <a name="getheaders-function"></a>Funzione GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: Intestazioni della richiesta