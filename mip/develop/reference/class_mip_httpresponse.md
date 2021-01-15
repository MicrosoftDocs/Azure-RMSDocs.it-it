---
title: classe HttpResponse
description: 'Documenta la classe HttpResponse:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8e4a8c392c6e18197e3b9b376482f3145d1ecd3f
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211397"
---
# <a name="class-httpresponse"></a>classe HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID risposta.
public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
public const std:: Vector \<uint8_t\>& GetBody () const  |  Ottiene il corpo della richiesta.
public const std:: Map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID risposta.

  
**Returns**: ID risposta il cui HttpRequest corrispondente avrà lo stesso ID
  
### <a name="getstatuscode-function"></a>GetStatusCode (funzione)
Ottiene il codice di stato della risposta.

  
**Restituisce**: codice di stato
  
### <a name="getbody-function"></a>Funzione GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: corpo della richiesta
  
### <a name="getheaders-function"></a>Funzione GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: intestazioni della richiesta