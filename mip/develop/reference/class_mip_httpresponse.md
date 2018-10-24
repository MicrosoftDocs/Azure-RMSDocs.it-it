---
title: Classe mip HttpResponse
description: Riferimento per la classe mip HttpResponse
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a19ea78b048cafe94501d452bb9c7409237f6ffd
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445356"
---
# <a name="class-miphttpresponse"></a>Classe mip::HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
 public const std::string& GetBody() const  |  Ottiene il corpo della richiesta.
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getstatuscode"></a>GetStatusCode
Ottiene il codice di stato della risposta.

  
**Restituisce**: codice di stato
  
### <a name="getbody"></a>GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: corpo della richiesta
  
### <a name="getheaders"></a>GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: intestazioni della richiesta