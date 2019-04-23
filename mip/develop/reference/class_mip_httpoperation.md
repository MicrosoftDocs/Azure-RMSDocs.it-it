---
title: classe mip::HttpOperation
description: Documenta la classe mip::httpoperation di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: e3eaedbf508f116b19521286b686bc955d108efe
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173559"
---
# <a name="class-miphttpoperation"></a>classe mip::HttpOperation 
Interfaccia che descrive una singola operazione HTTP implementata dall'app client quando si esegue l'override [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID dell'operazione.
Public std:: shared_ptr\<HttpResponse\> GetResponse)  |  Ottenere una risposta, se presente.
public bool IsCancelled()  |  Ottiene lo stato di annullamento dell'operazione.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID dell'operazione.

  
**Restituisce**: ID operazione corrispondente [HttpRequest](class_mip_httprequest.md) e [HttpResponse](class_mip_httpresponse.md) avrà lo stesso ID
  
### <a name="getresponse-function"></a>Metodo GetResponse (funzione)
Ottenere una risposta, se presente.

  
**Restituisce**: Risposta
  
### <a name="iscancelled-function"></a>IsCancelled (funzione)
Ottiene lo stato di annullamento dell'operazione.

  
**Restituisce**: Stato di annullamento