---
title: 'Classe MIP:: AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 836704d51d1afa55bc296681c863ee10a072ea79
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885907"
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