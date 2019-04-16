---
title: classe mip::AuthDelegate::OAuth2Challenge
description: Documenta la classe mip::authdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d404d6f60e7b2472bc97181b45fae3b4dabc387b
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574245"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>classe mip::AuthDelegate::OAuth2Challenge 
una classe che contiene tutte le informazioni richieste dall'applicazione chiamante per generare un token oauth2.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
pubblica OAuth2Challenge (const std:: String & autorità, const std:: String & risorsa, const std:: String & ambito)  |  Creare una nuova [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) oggetto.
public const std::string& GetAuthority() const  |  Ottenere la stringa di autorità.
Public std:: String const & GetResource() const  |  Ottenere la stringa di risorsa.
Public std:: String const & GetScope() const  |  Ottenere la stringa di ambito.
  
## <a name="members"></a>Membri
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge (funzione)
Creare una nuova [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) oggetto.

Parametri:  
* **autorità**: l'autorità deve essere generato con il token. 


* **risorsa**: la risorsa a cui il token è impostato. 


* **ambito**: l'ambito in cui il token è impostato.


  
### <a name="getauthority-function"></a>GetAuthority (funzione)
Ottenere la stringa di autorità.

  
**Restituisce**: La stringa di autorità.
  
### <a name="getresource-function"></a>GetResource (funzione)
Ottenere la stringa di risorsa.

  
**Restituisce**: La stringa di risorsa.
  
### <a name="getscope-function"></a>GetScope (funzione)
Ottenere la stringa di ambito.

  
**Restituisce**: La stringa di ambito.