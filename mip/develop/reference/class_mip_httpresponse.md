---
title: Classe mip::HttpResponse
description: Documenta la classe mip::httpresponse di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f7b16658135e802776cde37fdef19c82f7c198e6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329812"
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
