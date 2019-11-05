---
title: 'Classe MIP:: AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8205d207a48d90832b5961b14d37c7a7226293a2
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559027"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>Classe MIP:: AuthDelegate:: OAuth2Challenge 
classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std:: String & Authority, const std:: String & Resource, const std:: String & scope, const std:: String & Claims)  |  Costruisce un nuovo oggetto OAuth2Challenge.
public const std:: String & getauthority () const  |  Ottenere la stringa dell'autorità.
public const std:: String & GetResource () const  |  Ottenere la stringa di risorsa.
public const std:: String & GetScope () const  |  Ottenere la stringa dell'ambito.
public const std:: String & getclaims () const  |  Ottenere la stringa delle attestazioni.
  
## <a name="members"></a>Membri
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge (funzione)
Costruisce un nuovo oggetto OAuth2Challenge.

Parametri:  
* **autorità**: l'autorità con cui deve essere generato il token. 


* **Resource**: la risorsa su cui è impostato il token. 


* **scope**: ambito su cui è impostato il token.


  
### <a name="getauthority-function"></a>Getauthority (funzione)
Ottenere la stringa dell'autorità.

  
**Restituisce**: la stringa dell'autorità.
  
### <a name="getresource-function"></a>Funzione GetResource
Ottenere la stringa di risorsa.

  
**Restituisce**: la stringa di risorsa.
  
### <a name="getscope-function"></a>Funzione GetScope
Ottenere la stringa dell'ambito.

  
**Restituisce**: la stringa dell'ambito.
  
### <a name="getclaims-function"></a>Getclaims (funzione)
Ottenere la stringa delle attestazioni.

  
**Restituisce**: stringa Claims.