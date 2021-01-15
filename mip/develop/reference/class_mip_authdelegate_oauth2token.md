---
title: 'Classe AuthDelegate:: OAuth2Token'
description: 'Documenta la classe authdelegate:: oauth2token di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 4db3d2fbb2299b30b85516047ec237d2f23d7cd9
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212043"
---
# <a name="class-authdelegateoauth2token"></a>Classe AuthDelegate:: OAuth2Token 
Classe che contiene le informazioni sul token di accesso fornite da un'applicazione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Costruisce un nuovo oggetto OAuth2Token.
public OAuth2Token (const std:: String& accessToken)  |  Costruire un nuovo oggetto OAuth2Token dal token di accesso JWT.
public const std:: String& GetAccessToken () const  |  Ottenere la stringa del token di accesso.
public void SetAccessToken (const std:: String& accessToken)  |  Impostare la stringa del token di accesso.
public const std:: String& GetErrorMessage () const  |  Ottenere il messaggio di errore, se presente.
public void SetErrorMessage (const std:: String& errorMessage)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Costruisce un nuovo oggetto OAuth2Token.
  
### <a name="oauth2token-function"></a>OAuth2Token (funzione)
Costruire un nuovo oggetto OAuth2Token dal token di accesso JWT.

Parametri  
* **AccessToken**: JWT token di accesso.


  
### <a name="getaccesstoken-function"></a>GetAccessToken (funzione)
Ottenere la stringa del token di accesso.

  
**Restituisce**: stringa del token di accesso.
  
### <a name="setaccesstoken-function"></a>SetAccessToken (funzione)
Impostare la stringa del token di accesso.

Parametri  
* **AccessToken**: stringa del token di accesso.


  
### <a name="geterrormessage-function"></a>GetErrorMessage (funzione)
Ottenere il messaggio di errore, se presente.

  
**Restituisce**: messaggio di errore.
  
### <a name="seterrormessage-function"></a>SetErrorMessage (funzione)
Imposta il messaggio di errore.

Parametri  
* **ErrorMessage**: messaggio di errore.

