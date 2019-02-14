---
title: classe mip::AuthDelegate::OAuth2Token
description: Documenta la classe mip::authdelegate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: bef28489d16b040ff910103d9e0bf5a4719c66ff
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255972"
---
# <a name="class-mipauthdelegateoauth2token"></a>classe mip::AuthDelegate::OAuth2Token 
Una classe che definisce come Microsoft Information Protection SDK prevede che il token oauth2 da passare nuovamente nel SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Token()  |  Creare una nuova [OAuth2Token](class_mip_authdelegate_oauth2token.md) oggetto.
pubblica OAuth2Token (const std:: String & accessToken)  |  Creare una nuova [OAuth2Token](class_mip_authdelegate_oauth2token.md) oggetto da un accessToken.
public const std::string& GetAccessToken() const  |  Ottenere la stringa di token di accesso.
public void SetAccessToken (const std:: String & accessToken)  |  Impostare la stringa di Token di accesso.
  
## <a name="members"></a>Membri
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Creare una nuova [OAuth2Token](class_mip_authdelegate_oauth2token.md) oggetto.
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Creare una nuova [OAuth2Token](class_mip_authdelegate_oauth2token.md) oggetto da un accessToken.

Parametri:  
* **accessToken**: Il token di accesso effettivo passato il SDK.


  
### <a name="getaccesstoken-function"></a>Il parametro GetAccessToken (funzione)
Ottenere la stringa di token di accesso.

  
**Restituisce**: La stringa di token di accesso.
  
### <a name="setaccesstoken-function"></a>SetAccessToken (funzione)
Impostare la stringa di Token di accesso.

Parametri:  
* **accessToken**: la stringa di token di accesso.

