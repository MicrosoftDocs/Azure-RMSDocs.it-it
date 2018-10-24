---
title: Classe mip HttpDelegate
description: Riferimento per la classe mip HttpDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3e55f9aff5a9ebd97731ec21e408a33f22905648
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445371"
---
# <a name="class-miphttpdelegate"></a>Classe mip::HttpDelegate 
Interfaccia per l'override della gestione HTTP.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::shared_ptr<HttpResponse> Send(const std::shared_ptr<HttpRequest>& request, const std::shared_ptr<void>& context)  |  Inviare una richiesta HTTP.
  
## <a name="members"></a>Membri
  
### <a name="httpresponse"></a>HttpResponse
Inviare una richiesta HTTP.

Parametri:  
* **request**: richiesta HTTP 


* **context**: stesso contesto client opaco passato all'API che ha generato questa richiesta HTTP



  
**Restituisce**: risposta HTTP