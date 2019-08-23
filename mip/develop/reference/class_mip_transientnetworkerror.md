---
title: Classe mip::TransientNetworkError
description: 'Documenta la classe MIP:: transientnetworkerror di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 5787c5742edc2daefee00a3c5a9b2bf826b81529
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882913"
---
# <a name="class-miptransientnetworkerror"></a>Classe mip::TransientNetworkError 
Errore di rete temporaneo. Causato da un comportamento imprevisto quando si effettuano chiamate di rete agli endpoint di servizio. È possibile ripetere l'operazione dal momento che l'errore è temporaneo.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Ottiene il messaggio di errore.
public std:: shared_ptr\<Error\> Clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Members
  
### <a name="what-function"></a>funzione
Ottiene il messaggio di errore.

  
**Restituisce**: Messaggio di errore
  
### <a name="clone-function"></a>Funzione clone
Clona l'errore.

  
**Restituisce**: Clone dell'errore.
  
### <a name="geterrortype-function"></a>GetErrorType (funzione)
Ottiene il tipo di errore.

  
**Restituisce**: Tipo di errore.
  
### <a name="geterrorname-function"></a>Geterrorname (funzione)
Ottiene il nome dell'errore.

  
**Restituisce**: Nome dell'errore.
  
### <a name="getmessage-function"></a>GetMessage (funzione)
Ottiene il messaggio di errore.

  
**Restituisce**: Messaggio di errore.
  
### <a name="setmessage-function"></a>Funzione semessage
Imposta il messaggio di errore.

Parametri:  
* **msg**: messaggio di errore.

