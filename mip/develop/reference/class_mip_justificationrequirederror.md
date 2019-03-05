---
title: Classe mip::JustificationRequiredError
description: 'Classe MIP:: justificationrequirederror di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 0215d68bafa0243ebcf576755bec90ce5e2540a4
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333093"
---
# <a name="class-mipjustificationrequirederror"></a>Classe mip::JustificationRequiredError 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr virtual\<errore\> clone () const  |  Clona l'errore.
public char const* what() const  |  Ottiene il messaggio di errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="clone-function"></a>Funzioni di clone
Clona l'errore.

  
**Restituisce**: Un clone dell'errore.
  
### <a name="what-function"></a>tipo di funzione
Ottiene il messaggio di errore.

  
**Restituisce**: Il messaggio di errore
  
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

