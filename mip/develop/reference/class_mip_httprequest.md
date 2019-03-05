---
title: Classe mip::HttpRequest
description: Documenta la classe mip::httprequest di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6e663d4083d9daa2fc744289708f4c127ffb29c2
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330696"
---
# <a name="class-miphttprequest"></a>Classe mip::HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
public const std::string& GetBody() const  |  Ottiene il corpo della richiesta.
Public std:: Map const\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders() const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getrequesttype-function"></a>GetRequestType (funzione)
Ottiene il tipo di richiesta.

  
**Restituisce**: Tipo di richiesta
  
### <a name="geturl-function"></a>GetUrl (funzione)
Ottiene l'URL della richiesta.

  
**Restituisce**: Url della richiesta
  
### <a name="getbody-function"></a>GetBody (funzione)
Ottiene il corpo della richiesta.

  
**Restituisce**: Corpo della richiesta
  
### <a name="getheaders-function"></a>GetHeaders (funzione)
Ottiene le intestazioni della richiesta.

  
**Restituisce**: Intestazioni della richiesta
