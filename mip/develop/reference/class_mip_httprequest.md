---
title: Classe mip::HttpRequest
description: Documenta la classe mip::httprequest di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 8b0349db2e985d6fb015e1a2698187089483fbe3
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173512"
---
# <a name="class-miphttprequest"></a>Classe mip::HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene ID richiesta
public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
Public std:: Vector const\<uint8_t\>& GetBody() const  |  Ottiene il corpo della richiesta.
Public std:: Map const\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders() const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene ID richiesta

  
**Restituisce**: Request ID corrispondente [HttpResponse](class_mip_httpresponse.md) avrà lo stesso ID
  
### <a name="getrequesttype-function"></a>GetRequestType (funzione)
Ottiene il tipo di richiesta.

  
**Restituisce**: Tipo di richiesta
  
### <a name="geturl-function"></a>GetUrl (funzione)
Ottiene l'URL della richiesta.

  
**Restituisce**: Url della richiesta
  
### <a name="getbody-function"></a>GetBody (funzione)
Ottiene il corpo della richiesta.

  
**Restituisce**: Testo della richiesta
  
### <a name="getheaders-function"></a>GetHeaders (funzione)
Ottiene le intestazioni della richiesta.

  
**Restituisce**: Intestazioni della richiesta