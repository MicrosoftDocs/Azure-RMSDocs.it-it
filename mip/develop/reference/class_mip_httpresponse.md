---
title: classe HttpResponse
description: 'Documenta la classe HttpResponse:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 0a08b2bea4834375a01897b3d657772112463b89
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566875"
---
# <a name="class-httpresponse"></a>classe HttpResponse 
Interfaccia che descrive una singola risposta HTTP, implementata dall'app client durante l'override di HttpDelegate.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Ottiene l'ID risposta.
public int32_t GetStatusCode() const  |  Ottiene il codice di stato della risposta.
public const std:: Vector \<uint8_t\>& GetBody () const  |  Ottiene il corpo della richiesta.
public const std:: Map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders () const  |  Ottiene le intestazioni della richiesta.
  
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