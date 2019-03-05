---
title: classe mip::NoPermissionsError
description: Documenta la classe mip::nopermissionserror di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ea7edbc6e30d3ac529d55ddeaeecc63f140c512f
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329421"
---
# <a name="class-mipnopermissionserror"></a>classe mip::NoPermissionsError 
L'utente non è riuscito a ottenere l'accesso al contenuto, ad esempio per mancanza di autorizzazioni o contenuto revocato.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  Ottiene il contatto in caso di mancanti diritti al documento.
public std::string GetOwner() const  | _Non ancora documentato._
public char const* what() const  |  Ottiene il messaggio di errore.
Public std:: shared_ptr\<errore\> clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="getreferrer-function"></a>GetReferrer (funzione)
Ottiene il contatto in caso di mancanti diritti al documento.

  
**Restituisce**: Il contatto in caso di mancanti diritti al documento.
  
### <a name="getowner-function"></a>GetOwner (funzione)
_Non ancora documentato._

  
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

