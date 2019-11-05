---
title: Classe mip::HttpDelegate
description: 'Documenta la classe MIP:: httpdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a29673c71aaa0357ebb52bc4cab3b3fef74a21d1
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560190"
---
# <a name="class-miphttpdelegate"></a>Classe mip::HttpDelegate 
Interfaccia per l'override della gestione HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& Request, const std:: shared_ptr\<void\>& context)  |  Inviare una richiesta HTTP.
public std:: shared_ptr\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>& Request, const std:: shared_ptr\<void\>& context, const std:: Function\<void (STD :: shared_ptr\<HttpOperation\>)  |  Inviare una richiesta HTTP in modo asincrono.
public void CancelOperation (const std:: String & RequestId)  |  Annulla un'operazione HTTP specifica.
public void CancelAllOperations ()  |  Annulla le richieste HTTP in corso.
  
## <a name="members"></a>Membri
  
### <a name="send-function"></a>Funzione Send
Inviare una richiesta HTTP.

Parametri:  
* **request**: richiesta HTTP 


* **context**: stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP



  
**Restituisce**: contenitore operazione http
  
### <a name="sendasync-function"></a>Funzione SendAsync
Inviare una richiesta HTTP in modo asincrono.

Parametri:  
* **request**: richiesta HTTP 


* **context**: stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP 


* **callbackFn**: funzione che verrà eseguita al completamento



  
**Restituisce**: contenitore operazione http
  
### <a name="canceloperation-function"></a>CancelOperation (funzione)
Annulla un'operazione HTTP specifica.

Parametri:  
* **RequestId**: ID della richiesta da annullare


  
### <a name="cancelalloperations-function"></a>CancelAllOperations (funzione)
Annulla le richieste HTTP in corso.