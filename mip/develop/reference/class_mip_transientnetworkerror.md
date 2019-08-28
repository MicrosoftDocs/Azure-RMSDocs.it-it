---
title: Classe mip::TransientNetworkError
description: 'Documenta la classe MIP:: transientnetworkerror di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: c39c1e512a266009c6cf635f66c5d6cc8a931be1
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056822"
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

