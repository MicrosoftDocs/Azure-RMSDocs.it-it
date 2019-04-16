---
title: Classe mip::HttpResponse
description: Documenta la classe mip::httpresponse di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 06bc3f52bdecd85412dc0c35df46c7847167aa1b
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573756"
---
# <a name="class-miphttpresponse"></a>Classe mip::HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID di risposta.
public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
Public std:: Vector const\<uint8_t\>& GetBody() const  |  Ottiene il corpo della richiesta.
Public std:: Map const\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders() const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID di risposta.

  
**Restituisce**: ID risposta corrispondente [HttpRequest](class_mip_httprequest.md) verrà hanno avuto lo stesso ID
  
### <a name="getstatuscode-function"></a>GetStatusCode (funzione)
Ottiene il codice di stato della risposta.

  
**Restituisce**: Codice di stato
  
### <a name="getbody-function"></a>GetBody (funzione)
Ottiene il corpo della richiesta.

  
**Restituisce**: Testo della richiesta
  
### <a name="getheaders-function"></a>GetHeaders (funzione)
Ottiene le intestazioni della richiesta.

  
**Restituisce**: Intestazioni della richiesta