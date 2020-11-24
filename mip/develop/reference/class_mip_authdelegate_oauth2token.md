---
title: 'Classe AuthDelegate:: OAuth2Token'
description: 'Documenta la classe authdelegate:: oauth2token di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a8532e1950977e421fa25b426fa4e4061e610d8d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567261"
---
# <a name="class-authdelegateoauth2token"></a>Classe AuthDelegate:: OAuth2Token 
Classe che contiene le informazioni sul token di accesso fornite da un'applicazione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Costruisce un nuovo oggetto OAuth2Token.
public OAuth2Token (const std:: String& accessToken)  |  Costruire un nuovo oggetto OAuth2Token dal token di accesso JWT.
public const std:: String& GetAccessToken () const  |  Ottenere la stringa del token di accesso.
public void SetAccessToken (const std:: String& accessToken)  |  Impostare la stringa del token di accesso.
public const std:: String& GetErrorMessage () const  |  Ottenere il messaggio di errore, se presente.
public void SetErrorMessage (const std:: String& errorMessage)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Members
  
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

