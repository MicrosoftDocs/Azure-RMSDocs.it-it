---
title: 'Classe MIP:: AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2e96fb769a1b917715daa872736c6d2b81e2626e
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055422"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>Classe MIP:: AuthDelegate:: OAuth2Challenge 
classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std:: String & Authority, const std:: String & Resource, const std:: String & scope, const std:: String & Claims)  |  Costruisce un nuovo oggetto [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) .
public const std:: String & getauthority () const  |  Ottenere la stringa dell'autorità.
public const std:: String & GetResource () const  |  Ottenere la stringa di risorsa.
public const std:: String & GetScope () const  |  Ottenere la stringa dell'ambito.
public const std:: String & getclaims () const  |  Ottenere la stringa delle attestazioni.
  
## <a name="members"></a>Members
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge (funzione)
Costruisce un nuovo oggetto [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) .

Parametri:  
* **autorità**: l'autorità con cui deve essere generato il token. 


* **Resource**: la risorsa su cui è impostato il token. 


* **scope**: ambito su cui è impostato il token.


  
### <a name="getauthority-function"></a>Getauthority (funzione)
Ottenere la stringa dell'autorità.

  
**Restituisce**: Stringa dell'autorità.
  
### <a name="getresource-function"></a>Funzione GetResource
Ottenere la stringa di risorsa.

  
**Restituisce**: Stringa di risorsa.
  
### <a name="getscope-function"></a>Funzione GetScope
Ottenere la stringa dell'ambito.

  
**Restituisce**: Stringa dell'ambito.
  
### <a name="getclaims-function"></a>Getclaims (funzione)
Ottenere la stringa delle attestazioni.

  
**Restituisce**: Stringa delle attestazioni.