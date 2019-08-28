---
title: Classe mip::HttpRequest
description: 'Documenta la classe MIP:: HttpRequest di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 92cf2bc3840e3cb38210c42c1e1b2d43db1e8bd4
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054833"
---
# <a name="class-miphttprequest"></a>Classe mip::HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID della richiesta.
public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
public const std::\<vector\>uint8_t & GetBody () const  |  Ottiene il corpo della richiesta.
public const std::\<map std:: String, std:: String,\>CaseInsensitiveComparator & GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID della richiesta.

  
**Restituisce**: ID richiesta il HttpResponse corrispondente avrà lo stesso ID
  
### <a name="getrequesttype-function"></a>GetRequestType (funzione)
Ottiene il tipo di richiesta.

  
**Restituisce**: Tipo di richiesta
  
### <a name="geturl-function"></a>GetUrl (funzione)
Ottiene l'URL della richiesta.

  
**Restituisce**: URL della richiesta
  
### <a name="getbody-function"></a>Funzione GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: Corpo della richiesta
  
### <a name="getheaders-function"></a>Funzione GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: Intestazioni della richiesta