---
title: 'Classe AuthDelegate:: OAuth2Challenge'
description: 'Documenta la classe authdelegate:: oauth2challenge di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: f422b99674213904316eab622bfc915f128228ec
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567272"
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