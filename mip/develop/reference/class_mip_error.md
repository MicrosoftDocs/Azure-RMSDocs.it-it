---
title: Classe mip::Error
description: 'Documenta la classe MIP:: Error di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f59a2b394cbf0bfa5deb555e2c4cdd8c427ed7ea
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560289"
---
# <a name="class-miperror"></a>Classe mip::Error 
Classe di base per tutti gli errori che verranno segnalati (generati o restituiti) da MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Ottiene il messaggio di errore.
public std:: shared_ptr\<Error\> Clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="what-function"></a>funzione
Ottiene il messaggio di errore.

  
**Restituisce**: messaggio di errore
  
### <a name="clone-function"></a>Funzione clone
Clona l'errore.

  
**Restituisce**: clone dell'errore.
  
### <a name="geterrortype-function"></a>GetErrorType (funzione)
Ottiene il tipo di errore.

  
**Restituisce**: tipo di errore.
  
### <a name="geterrorname-function"></a>Geterrorname (funzione)
Ottiene il nome dell'errore.

  
**Restituisce**: nome dell'errore.
  
### <a name="getmessage-function"></a>GetMessage (funzione)
Ottiene il messaggio di errore.

  
**Restituisce**: messaggio di errore.
  
### <a name="setmessage-function"></a>Funzione semessage
Imposta il messaggio di errore.

Parametri:  
* **msg**: messaggio di errore.

