---
title: Classe mip::HttpDelegate
description: Documenta la classe mip::httpdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 18425a807fcddc1bc1db19a35534036a6552255c
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329846"
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
