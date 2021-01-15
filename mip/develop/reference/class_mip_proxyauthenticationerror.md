---
title: Classe ProxyAuthenticationError
description: 'Documenta la classe proxyauthenticationerror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 04915e74cc09f271a2ca3bb256b906bc442bb3fd
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214304"
---
# <a name="class-proxyauthenticationerror"></a>Classe ProxyAuthenticationError 
Errore di autenticazione del proxy.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Category GetCategory () const  |  Ottiene la categoria di errore di rete.
public int32_t GetResponseStatusCode () const  |  Ottiene il codice di stato della risposta HTTP.
Categoria enum  |  Categoria di errore di rete.
  
## <a name="members"></a>Membri
  
### <a name="getcategory-function"></a>GetCategory (funzione)
Ottiene la categoria di errore di rete.

  
**Restituisce**: categoria di errore di rete
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode (funzione)
Ottiene il codice di stato della risposta HTTP.

  
**Restituisce**: codice di stato della risposta http, 0 se None
  
### <a name="category-enum"></a>Enum categoria

Categoria di errore di rete.

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
