---
title: 'Classe AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe authdelegate:: oauth2challenge di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: f8a350a8c9ddd68f484a98b0e63860d2965bd890
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763611"
---
# <a name="class-authdelegateoauth2challenge"></a>Classe AuthDelegate:: OAuth2Challenge 
classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std:: String& Authority, const std:: String& Resource, const std:: String& scope, const std:: String& Claims)  |  Costruisce un nuovo oggetto OAuth2Challenge.
public const std:: String& getauthority () const  |  Ottenere la stringa dell'autorità.
public const std:: String& GetResource () const  |  Ottenere la stringa di risorsa.
public const std:: String& GetScope () const  |  Ottenere la stringa dell'ambito.
public const std:: String& getclaims () const  |  Ottenere la stringa delle attestazioni.
  
## <a name="members"></a>Members
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge (funzione)
Costruisce un nuovo oggetto OAuth2Challenge.

Parametri  
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