---
title: classe HttpRequest
description: 'Documenta la classe HttpRequest:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: c613729664141eb96e2cd1844107fcc1d9a4fa18
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215222"
---
# <a name="class-httprequest"></a>classe HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID della richiesta.
public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
public const std:: Vector \<uint8_t\>& GetBody () const  |  Ottiene il corpo della richiesta.
public const std:: Map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID della richiesta.

  
**Returns**: ID della richiesta l'oggetto HttpResponse corrispondente avrà lo stesso ID
  
### <a name="getrequesttype-function"></a>GetRequestType (funzione)
Ottiene il tipo di richiesta.

  
**Restituisce**: tipo di richiesta
  
### <a name="geturl-function"></a>GetUrl (funzione)
Ottiene l'URL della richiesta.

  
**Restituisce**: URL della richiesta
  
### <a name="getbody-function"></a>Funzione GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: corpo della richiesta
  
### <a name="getheaders-function"></a>Funzione GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: intestazioni della richiesta