---
title: 'Classe AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe authdelegate:: oauth2challenge di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 3062130037142ebe3b5c227da0dd12a8f38065c1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212077"
---
# <a name="class-authdelegateoauth2challenge"></a>Classe AuthDelegate:: OAuth2Challenge 
classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token OAuth2.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std:: String& Authority, const std:: String& Resource, const std:: String& scope, const std:: String& Claims)  |  Costruisce un nuovo oggetto OAuth2Challenge.
public const std:: String& getauthority () const  |  Ottenere la stringa dell'autorità.
public const std:: String& GetResource () const  |  Ottenere la stringa di risorsa.
public const std:: String& GetScope () const  |  Ottenere la stringa dell'ambito.
public const std:: String& getclaims () const  |  Ottenere la stringa delle attestazioni.
  
## <a name="members"></a>Membri
  
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