---
title: Classe mip HttpRequest
description: Riferimento per la classe mip HttpRequest
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e838eb247bc00d43da72db1de03304e89a1b1da5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445241"
---
# <a name="class-miphttprequest"></a>Classe mip::HttpRequest 
Interfaccia che descrive una singola richiesta HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public HttpRequestType GetRequestType() const  |  Ottiene il tipo di richiesta.
 public const std::string& GetUrl() const  |  Ottiene l'URL della richiesta.
 public const std::string& GetBody() const  |  Ottiene il corpo della richiesta.
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="httprequesttype"></a>HttpRequestType
Ottiene il tipo di richiesta.

  
**Restituisce**: tipo di richiesta
  
### <a name="geturl"></a>GetUrl
Ottiene l'URL della richiesta.

  
**Restituisce**: URL della richiesta
  
### <a name="getbody"></a>GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: corpo della richiesta
  
### <a name="getheaders"></a>GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: intestazioni della richiesta