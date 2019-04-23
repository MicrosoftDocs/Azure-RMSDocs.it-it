---
title: Classe mip::HttpDelegate
description: Documenta la classe mip::httpdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6dedd5e52b0599a58acabd85f7bd076169b3758e
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60174052"
---
# <a name="class-miphttpdelegate"></a>Classe mip::HttpDelegate 
Interfaccia per l'override della gestione HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<HttpOperation\> inviare (const std:: shared_ptr\<HttpRequest\>& richiesta, const std:: shared_ptr\<void\>& contesto)  |  Inviare una richiesta HTTP.
Public std:: shared_ptr\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>& richiesta, const std:: shared_ptr\<void\>& context, const std:: funzione\<void (std:: shared_ptr\<HttpOperation\>)\>& callbackFn)  |  Inviare la richiesta HTTP in modo asincrono.
public void CancelOperation (const std:: String & requestId)  |  Annullare un'operazione HTTP specifica.
public void CancelAllOperations()  |  Annullare le richieste HTTP in corso.
  
## <a name="members"></a>Membri
  
### <a name="send-function"></a>Funzione Send
Inviare una richiesta HTTP.

Parametri:  
* **request**: Richiesta HTTP 


* **context**: Lo stesso contesto di client opaco passato all'API che ha generato questa richiesta HTTP



  
**Restituisce**: Contenitore di operazione HTTP
  
### <a name="sendasync-function"></a>SendAsync (funzione)
Inviare la richiesta HTTP in modo asincrono.

Parametri:  
* **request**: Richiesta HTTP 


* **context**: Lo stesso contesto di client opaco passato all'API che ha generato questa richiesta HTTP 


* **callbackFn**: Funzione che verrà eseguito dopo il completamento



  
**Restituisce**: Contenitore di operazione HTTP
  
### <a name="canceloperation-function"></a>CancelOperation (funzione)
Annullare un'operazione HTTP specifica.

Parametri:  
* **requestId**: ID della richiesta di annullamento


  
### <a name="cancelalloperations-function"></a>CancelAllOperations (funzione)
Annullare le richieste HTTP in corso.