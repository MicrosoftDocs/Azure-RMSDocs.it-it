---
title: Classe ProxyAuthenticationError
description: 'Documenta la classe proxyauthenticationerror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 0da14f6a13632c0bf45ac3a409b0033a9ee1c603
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564417"
---
# <a name="class-proxyauthenticationerror"></a>Classe ProxyAuthenticationError 
Errore di autenticazione del proxy.
  
## <a name="summary"></a>Riepilogo

| Membri                                       | Descrizioni
|-----------------------------------------------|---------------------------------------------
| public Category GetCategory () const           |  Ottiene la categoria di errore di rete.
| public int32_t GetResponseStatusCode () const  |  Ottiene il codice di stato della risposta HTTP.
| Categoria enum                                 |  Categoria di errore di rete.
  
## <a name="members"></a>Membri
  
### <a name="getcategory-function"></a>GetCategory (funzione)

Ottiene la categoria di errore di rete.

**Restituisce**: categoria di errore di rete
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode (funzione)

Ottiene il codice di stato della risposta HTTP.

**Restituisce**: codice di stato della risposta http, 0 se None
  
### <a name="category-enum"></a>Enum categoria

Categoria di errore di rete.

| Valori                   | Descrizioni
|--------------------------|---------------------------------------------
| Unknown                  | Errore di rete sconosciuto
| FailureResponseCode      | Il codice di risposta HTTP indica un errore
| BadResponse              | Impossibile leggere la risposta HTTP
| UnexpectedResponse       | Risposta HTTP completata ma contenente dati imprevisti
| NoConnection             | Impossibile stabilire una connessione
| Proxy                    | Errore del proxy
| SSL                      | Errore SSL
| Timeout                  | Timeout della connessione
| Offline                  | Per l'operazione è necessaria la connettività di rete
| Sospensione causata dal servizio Microsoft FullText                | Operazione HTTP non riuscita a causa della limitazione del traffico del server
| Operazione annullata                | L'operazione HTTP è stata annullata dall'applicazione
