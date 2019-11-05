---
title: 'Classe MIP:: AuthDelegate:: OAuth2Token'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d8bce56e02778d48e6e3c0cfdb02f1c3f1f4054a
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560339"
---
# <a name="class-mipauthdelegateoauth2token"></a>Classe MIP:: AuthDelegate:: OAuth2Token 
Classe che definisce il modo in cui l'SDK MIP prevede che il token OAuth2 venga passato nuovamente all'SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Costruisce un nuovo oggetto OAuth2Token.
public OAuth2Token (const std:: String & accessToken)  |  Costruisce un nuovo oggetto OAuth2Token da un accessToken.
public const std:: String & GetAccessToken () const  |  Ottenere la stringa del token di accesso.
public void SetAccessToken (const std:: String & accessToken)  |  Impostare la stringa del token di accesso.
  
## <a name="members"></a>Membri
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Costruisce un nuovo oggetto OAuth2Token.
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Costruisce un nuovo oggetto OAuth2Token da un accessToken.

Parametri:  
* **AccessToken**: il token di accesso effettivo passato nell'SDK.


  
### <a name="getaccesstoken-function"></a>GetAccessToken (funzione)
Ottenere la stringa del token di accesso.

  
**Returns**: stringa del token di accesso.
  
### <a name="setaccesstoken-function"></a>SetAccessToken (funzione)
Impostare la stringa del token di accesso.

Parametri:  
* **AccessToken**: stringa del token di accesso.

