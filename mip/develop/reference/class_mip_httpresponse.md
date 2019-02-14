---
title: Classe mip::HttpResponse
description: Documenta la classe mip::httpresponse di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 00a6d7dd3728edbf6fb1dbb4e59c537d7b6cf911
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252997"
---
# <a name="class-miphttpresponse"></a>Classe mip::HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
public const std::string& GetBody() const  |  Ottiene il corpo della richiesta.
Public std:: Map const\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders() const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Membri
  
### <a name="getstatuscode-function"></a>GetStatusCode (funzione)
Ottiene il codice di stato della risposta.

  
**Restituisce**: Codice di stato
  
### <a name="getbody-function"></a>GetBody (funzione)
Ottiene il corpo della richiesta.

  
**Restituisce**: Corpo della richiesta
  
### <a name="getheaders-function"></a>GetHeaders (funzione)
Ottiene le intestazioni della richiesta.

  
**Restituisce**: Intestazioni della richiesta
