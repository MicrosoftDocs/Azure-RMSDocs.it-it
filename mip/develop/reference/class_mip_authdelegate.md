---
title: 'Classe MIP:: AuthDelegate'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: b865a26b9cfd96cf4beafa2eb712917405f1dd5c
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884511"
---
# <a name="class-mipauthdelegate"></a>Classe MIP:: AuthDelegate 
Delegato per le operazioni correlate all'autenticazione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const MIP:: Identity & Identity, const OAuth2Challenge & Challenge, OAuth2Token & token)  |  Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.
public virtual bool AcquireOAuth2Token (const MIP:: Identity & Identity, const OAuth2Challenge & Challenge, const std\<:\>: shared_ptr void & context, OAuth2Token & token)  |  Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.
  
## <a name="members"></a>Members
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.

Parametri:  
* **identity**: 


* **richiesta di verifica**: 


* **token**: 


> Deprecato Questo metodo sarà presto deprecato a favore di quello che accetta un parametro di contesto. Se la nuova versione è stata implementata, non è necessario implementare questa versione.
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.

Parametri:  
* **identity**: Utente per il quale è richiesto un token 


* **richiesta di verifica**: OAuth2 Challenge 


* **context**: Contesto opaco passato all'API MIP dall'applicazione host 


* **token**: [output] token OAuth2 con codifica Base64

