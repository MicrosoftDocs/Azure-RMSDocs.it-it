---
title: 'Classe MIP:: AuthDelegate'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 30907f3bf4a08f72305a59290c8cbd891def44c9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490609"
---
# <a name="class-mipauthdelegate"></a>Classe MIP:: AuthDelegate 
Delegato per le operazioni correlate all'autenticazione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const MIP:: Identity & Identity, const OAuth2Challenge & Challenge, OAuth2Token & token)  |  Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.
public virtual bool AcquireOAuth2Token (const MIP:: Identity & Identity, const OAuth2Challenge & Challenge, const std:: shared_ptr\<void\>& context, OAuth2Token & token)  |  Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.
  
## <a name="members"></a>Members
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.

Parametri:  
* **Identity**: utente per cui è richiesto un token 


* **richiesta**: OAuth2 Challenge 


* **token**: [output] token OAuth2 con codifica Base64



  
**Restituisce**: true se il token è stato acquisito correttamente; in caso contrario, false in caso di errore, se il parametro di output del token contiene un messaggio di errore, verrà incluso nell'eccezione NoAuthTokenError che verrà successivamente generata all'applicazione.
> Deprecato: questo metodo sarà presto deprecato a favore di quello che accetta un parametro di contesto. Se la nuova versione è stata implementata, non è necessario implementare questa versione.
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.

Parametri:  
* **Identity**: utente per cui è richiesto un token 


* **richiesta**: OAuth2 Challenge 


* **contesto**: contesto opaco passato all'API MIP dall'applicazione host 


* **token**: [output] token OAuth2 con codifica Base64



  
**Restituisce**: true se il token è stato acquisito correttamente; in caso contrario, false in caso di errore, se il parametro di output del token contiene un messaggio di errore, verrà incluso nell'eccezione NoAuthTokenError che verrà successivamente generata all'applicazione.