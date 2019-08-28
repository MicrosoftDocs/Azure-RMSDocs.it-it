---
title: 'Classe MIP:: AuthDelegate:: OAuth2Token'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 93c73f632410bf6b1c6898746d1fcbd2c4f67e72
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056259"
---
# <a name="class-mipauthdelegateoauth2token"></a>Classe MIP:: AuthDelegate:: OAuth2Token 
Classe che definisce il modo in cui l'SDK MIP prevede che il token OAuth2 venga passato nuovamente all'SDK.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Costruisce un nuovo oggetto [OAuth2Token](class_mip_authdelegate_oauth2token.md) .
public OAuth2Token (const std:: String & accessToken)  |  Costruisce un nuovo oggetto [OAuth2Token](class_mip_authdelegate_oauth2token.md) da un AccessToken.
public const std:: String & GetAccessToken () const  |  Ottenere la stringa del token di accesso.
public void SetAccessToken (const std:: String & accessToken)  |  Impostare la stringa del token di accesso.
  
## <a name="members"></a>Members
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Costruisce un nuovo oggetto [OAuth2Token](class_mip_authdelegate_oauth2token.md) .
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Costruisce un nuovo oggetto [OAuth2Token](class_mip_authdelegate_oauth2token.md) da un AccessToken.

Parametri:  
* **accessToken**: Il token di accesso effettivo passato nell'SDK.


  
### <a name="getaccesstoken-function"></a>GetAccessToken (funzione)
Ottenere la stringa del token di accesso.

  
**Restituisce**: Stringa del token di accesso.
  
### <a name="setaccesstoken-function"></a>SetAccessToken (funzione)
Impostare la stringa del token di accesso.

Parametri:  
* **AccessToken**: stringa del token di accesso.

