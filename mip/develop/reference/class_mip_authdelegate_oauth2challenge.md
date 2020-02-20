---
title: 'Classe MIP:: AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe MIP:: authdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8e3119e18d465c9ad66dd1cbbece003b96d1a3b7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489062"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>Classe MIP:: AuthDelegate:: OAuth2Challenge 
classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std:: String & Authority, const std:: String & Resource, const std:: String & scope, const std:: String & Claims)  |  Costruisce un nuovo oggetto OAuth2Challenge.
public const std:: String & getauthority () const  |  Ottenere la stringa dell'autorità.
public const std:: String & GetResource () const  |  Ottenere la stringa di risorsa.
public const std:: String & GetScope () const  |  Ottenere la stringa dell'ambito.
public const std:: String & getclaims () const  |  Ottenere la stringa delle attestazioni.
  
## <a name="members"></a>Members
  
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