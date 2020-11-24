---
title: Classe ProxyAuthenticationError
description: 'Documenta la classe proxyauthenticationerror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d4468fe243f7120630d0a34d453ff4e9a5bf6527
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567080"
---
# <a name="class-proxyauthenticationerror"></a>Classe ProxyAuthenticationError 
Errore di autenticazione del proxy.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Category GetCategory () const  |  Ottiene la categoria di errore di rete.
public int32_t GetResponseStatusCode () const  |  Ottiene il codice di stato della risposta HTTP.
Categoria enum  |  Categoria di errore di rete.
  
## <a name="members"></a>Members
  
### <a name="getcategory-function"></a>GetCategory (funzione)
Ottiene la categoria di errore di rete.

  
**Restituisce**: categoria di errore di rete
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode (funzione)
Ottiene il codice di stato della risposta HTTP.

  
**Restituisce**: codice di stato della risposta http, 0 se None
  
### <a name="category-enum"></a>Enum categoria

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Sconosciuto            | Errore di rete sconosciuto
FailureResponseCode            | Il codice di risposta HTTP indica un errore
BadResponse            | Impossibile leggere la risposta HTTP
UnexpectedResponse            | Risposta HTTP completata ma contenente dati imprevisti
NoConnection            | Impossibile stabilire una connessione
Proxy            | Errore del proxy
SSL            | Errore SSL
Timeout            | Timeout della connessione
Offline            | Per l'operazione è necessaria la connettività di rete
Sospensione causata dal servizio Microsoft FullText            | Operazione HTTP non riuscita a causa della limitazione del traffico del server
Operazione annullata            | L'operazione HTTP è stata annullata dall'applicazione

Categoria di errore di rete.