---
title: classe mip::NoAuthTokenError
description: Documenta la classe mip::noauthtokenerror di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 8dca2231931ab33f243b71850757b2c009c492c9
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173175"
---
# <a name="class-mipnoauthtokenerror"></a>classe mip::NoAuthTokenError 
L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un token di autenticazione mancante.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Ottiene il messaggio di errore.
Public std:: shared_ptr\<errore\> clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="what-function"></a>tipo di funzione
Ottiene il messaggio di errore.

  
**Restituisce**: Il messaggio di errore
  
### <a name="clone-function"></a>Funzioni di clone
Clona l'errore.

  
**Restituisce**: Un clone dell'errore.
  
### <a name="geterrortype-function"></a>GetErrorType (funzione)
Ottiene il tipo di errore.

  
**Restituisce**: Il tipo di errore.
  
### <a name="geterrorname-function"></a>GetErrorName (funzione)
Ottiene il nome dell'errore.

  
**Restituisce**: Il nome di errore.
  
### <a name="getmessage-function"></a>GetMessage (funzione)
Ottiene il messaggio di errore.

  
**Restituisce**: Il messaggio di errore.
  
### <a name="setmessage-function"></a>SetMessage (funzione)
Imposta il messaggio di errore.

Parametri:  
* **msg**: messaggio di errore.