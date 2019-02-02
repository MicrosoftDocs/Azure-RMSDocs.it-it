---
title: Classe mip::HttpDelegate
description: Documenta la classe mip::httpdelegate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 68d26b23c1e3ea2e29c22316f80e18937ab78d5c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651021"
---
# <a name="class-miphttpdelegate"></a>Classe mip::HttpDelegate 
Interfaccia per l'override della gestione HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<HttpResponse\> inviare (const std:: shared_ptr\<HttpRequest\>& richiesta, const std:: shared_ptr\<void\>& contesto)  |  Inviare una richiesta HTTP.
public void SendAsync (const std:: shared_ptr\<HttpRequest\>& richiesta, const std:: shared_ptr\<void\>& context, const std:: Function\<void(std::shared_ptr\<HttpResponse\>)\>& fnCallback)  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="send-function"></a>Funzione Send
Inviare una richiesta HTTP.

Parametri:  
* **request**: Richiesta HTTP 


* **context**: Lo stesso contesto di client opaco passato all'API che ha generato questa richiesta HTTP



  
**Restituisce**: Risposta HTTP
  
### <a name="sendasync-function"></a>SendAsync (funzione)
_Non ancora documentato._
