---
title: Classe mip::HttpResponse
description: 'Documenta la classe MIP:: HttpResponse di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e24eef471b11daffadb84235edbc93ff14696c25
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488059"
---
# <a name="class-miphttpresponse"></a>Classe mip::HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client quando si esegue l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID risposta.
public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
public const std:: Vector\<uint8_t\>& GetBody () const  |  Ottiene il corpo della richiesta.
public const std:: Map\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID risposta.

  
**Returns**: ID risposta il cui HttpRequest corrispondente avrà lo stesso ID
  
### <a name="getstatuscode-function"></a>GetStatusCode (funzione)
Ottiene il codice di stato della risposta.

  
**Restituisce**: codice di stato
  
### <a name="getbody-function"></a>Funzione GetBody
Ottiene il corpo della richiesta.

  
**Restituisce**: corpo della richiesta
  
### <a name="getheaders-function"></a>Funzione GetHeaders
Ottiene le intestazioni della richiesta.

  
**Restituisce**: intestazioni della richiesta