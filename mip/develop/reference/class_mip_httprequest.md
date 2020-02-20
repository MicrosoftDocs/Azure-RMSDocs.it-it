---
title: Classe mip::HttpRequest
description: 'Documenta la classe MIP:: HttpRequest di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f3b26ad07b8b3bfc556646cfd96a71aa9188bbb0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488093"
---
# <a name="class-miphttprequest"></a>Classe mip::HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID della richiesta.
public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
public const std:: Vector\<uint8_t\>& GetBody () const  |  Ottiene il corpo della richiesta.
public const std:: Map\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Members
  
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