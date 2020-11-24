---
title: Classe AuthDelegate
description: 'Documenta la classe authdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 9a971a7d0e8cf78baa5231225da620c9e1c8fa47
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567267"
---
# <a name="class-authdelegate"></a>Classe AuthDelegate 
Delegato per le operazioni correlate all'autenticazione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& Challenge, OAuth2Token& token)  |  Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.
public virtual bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& Challenge, const std:: shared_ptr \<void\>& context, OAuth2Token& token)  |  Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.
  
## <a name="members"></a>Members
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.

Parametri  
* **Identity**: utente per cui è richiesto un token 


* **richiesta**: OAuth2 Challenge 


* **token**: [output] token OAuth2 con codifica Base64



  
**Restituisce**: true se il token è stato acquisito correttamente; in caso contrario, false in caso di errore, se il parametro di output del token contiene un messaggio di errore, verrà incluso nell'eccezione NoAuthTokenError che verrà successivamente generata all'applicazione.
> Deprecato: questo metodo sarà presto deprecato a favore di quello che accetta un parametro di contesto. Se la nuova versione è stata implementata, non è necessario implementare questa versione.
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando è necessario un token di autenticazione per il motore dei criteri con l'identità specificata e la richiesta specificata. Il client deve restituire se l'acquisizione del token è stata completata correttamente. In caso di esito positivo, deve inizializzare l'oggetto token specificato.

Parametri  
* **Identity**: utente per cui è richiesto un token 


* **richiesta**: OAuth2 Challenge 


* **contesto**: contesto opaco passato all'API MIP dall'applicazione host 


* **token**: [output] token OAuth2 con codifica Base64



  
**Restituisce**: true se il token è stato acquisito correttamente; in caso contrario, false in caso di errore, se il parametro di output del token contiene un messaggio di errore, verrà incluso nell'eccezione NoAuthTokenError che verrà successivamente generata all'applicazione.