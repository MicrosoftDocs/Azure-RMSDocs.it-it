---
title: Classe mip::HttpDelegate
description: Documenta la classe mip::httpdelegate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8dd81508766c65d6232c278d56f3720a98aaa9eb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256295"
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
