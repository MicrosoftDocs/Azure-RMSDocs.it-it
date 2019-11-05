---
title: Classe mip::HttpRequest
description: 'Documenta la classe MIP:: HttpRequest di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: bfe55f09caaa20687750b055e10828f8cc6df2bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560184"
---
# <a name="class-miphttprequest"></a>Classe mip::HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID della richiesta.
public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
public const std:: Vector\<uint8_t\>& GetBody () const  |  Ottiene il corpo della richiesta.
public const std:: Map\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
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