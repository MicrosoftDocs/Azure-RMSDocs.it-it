---
title: Classe MIP::P roxyAuthenticationError
description: Documenta la classe MIP::p roxyauthenticationerror dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c0289f9b2f2a8a1163e62e6c6a96e3023f297194
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489623"
---
# <a name="class-mipproxyauthenticationerror"></a>Classe MIP::P roxyAuthenticationError 
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
NoConnection            | Non è stato possibile stabilire una connessione
Proxy            | Errore del proxy
SSL            | Errore SSL
Timeout            | Timeout della connessione
Offline            | Per l'operazione è necessaria la connettività di rete
Throttled            | Operazione HTTP non riuscita a causa della limitazione del traffico del server
Annullato            | L'operazione HTTP è stata annullata dall'applicazione
Categoria di errore di rete.