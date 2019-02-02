---
title: classe mip::AuthDelegate::OAuth2Token
description: Documenta la classe mip::authdelegate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 7ce9e336edfeeee07725b30c4d76c3b3c2073bc6
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652048"
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

