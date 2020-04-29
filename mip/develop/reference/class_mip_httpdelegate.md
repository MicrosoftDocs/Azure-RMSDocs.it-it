---
title: Classe HttpDelegate
description: 'Documenta la classe httpdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e1ddc8595e3cba2172228532a84ca68883cc0afd
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762817"
---
# <a name="class-httpdelegate"></a>Classe HttpDelegate 
Interfaccia per l'override della gestione HTTP.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std::\<shared_ptr\> HttpRequest& request, const std:\<:\> shared_ptr void& context)  |  Inviare una richiesta HTTP.
public std:: shared_ptr\<HttpOperation\> SendAsync (const std::\<shared_ptr\> HttpRequest& request, const std:\<:\> shared_ptr void& context, const std\<:: Function void (STD\<:\> : shared_ptr HttpOperation)  |  Inviare una richiesta HTTP in modo asincrono.
public void CancelOperation (const std:: String& RequestId)  |  Annulla un'operazione HTTP specifica.
public void CancelAllOperations ()  |  Annulla le richieste HTTP in corso.
  
## <a name="members"></a>Members
  
### <a name="send-function"></a>Funzione Send
Inviare una richiesta HTTP.

Parametri  
* **request**: richiesta HTTP 


* **context**: stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP



  
**Restituisce**: contenitore operazione http
  
### <a name="sendasync-function"></a>Funzione SendAsync
Inviare una richiesta HTTP in modo asincrono.

Parametri  
* **request**: richiesta HTTP 


* **context**: stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP 


* **callbackFn**: funzione che verrà eseguita al completamento



  
**Restituisce**: contenitore operazione http
  
### <a name="canceloperation-function"></a>CancelOperation (funzione)
Annulla un'operazione HTTP specifica.

Parametri  
* **RequestId**: ID della richiesta da annullare


  
### <a name="cancelalloperations-function"></a>CancelAllOperations (funzione)
Annulla le richieste HTTP in corso.