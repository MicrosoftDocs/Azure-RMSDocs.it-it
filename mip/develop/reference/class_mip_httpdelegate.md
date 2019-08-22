---
title: Classe mip::HttpDelegate
description: 'Documenta la classe MIP:: httpdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d2b01c53b44d6884f47cf48c431ee7359f64b9c4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885593"
---
# <a name="class-miphttpdelegate"></a>Classe mip::HttpDelegate 
Interfaccia per l'override della gestione HTTP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std::\<shared_ptr\>HttpRequest & Request, const std:\<:\>shared_ptr void & context)  |  Inviare una richiesta HTTP.
public std:: shared_ptr\<HttpOperation\> SendAsync (const std::\<shared_ptr\>HttpRequest & Request, const std:\<:\>shared_ptr void & context, const std:: funzione\<void (STD:: shared_ptr\<HttpOperation\>)\>& callbackFn)  |  Inviare una richiesta HTTP in modo asincrono.
public void CancelOperation (const std:: String & RequestId)  |  Annulla un'operazione HTTP specifica.
public void CancelAllOperations()  |  Annulla le richieste HTTP in corso.
  
## <a name="members"></a>Members
  
### <a name="send-function"></a>Funzione Send
Inviare una richiesta HTTP.

Parametri:  
* **richiesta**: Richiesta HTTP 


* **context**: Lo stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP



  
**Restituisce**: Contenitore operazione HTTP
  
### <a name="sendasync-function"></a>Funzione SendAsync
Inviare una richiesta HTTP in modo asincrono.

Parametri:  
* **richiesta**: Richiesta HTTP 


* **context**: Lo stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP 


* **callbackFn**: Funzione che verrà eseguita al completamento



  
**Restituisce**: Contenitore operazione HTTP
  
### <a name="canceloperation-function"></a>CancelOperation (funzione)
Annulla un'operazione HTTP specifica.

Parametri:  
* **requestId**: ID della richiesta da annullare


  
### <a name="cancelalloperations-function"></a>CancelAllOperations (funzione)
Annulla le richieste HTTP in corso.