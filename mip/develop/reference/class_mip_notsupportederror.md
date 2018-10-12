---
title: Classe mip NotSupportedError
description: Riferimento per la classe mip NotSupportedError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6053c29463b34b938f919508cb24f4e03f504c47
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446465"
---
# <a name="class-mipnotsupportederror"></a>Classe mip::NotSupportedError 
L'operazione richiesta dall'applicazione non è supportata dall'SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public char const* what() const  |  Ottiene il messaggio di errore.
public std::shared_ptr<Error> Clone() const  |  Clona l'errore.
 public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
 public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
 public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
 public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
  
## <a name="members"></a>Membri
  
### <a name="what"></a>what
Ottiene il messaggio di errore.

  
**Restituisce**: messaggio di errore.
  
### <a name="error"></a>Errore
Clona l'errore.

  
**Restituisce**: clone dell'errore.
  
### <a name="errortype"></a>ErrorType
Ottiene il tipo di errore.

  
**Restituisce**: tipo di errore.
  
### <a name="geterrorname"></a>GetErrorName
Ottiene il nome dell'errore.

  
**Restituisce**: nome dell'errore.
  
### <a name="getmessage"></a>GetMessage
Ottiene il messaggio di errore.

  
**Restituisce**: messaggio di errore.
  
### <a name="setmessage"></a>SetMessage
Imposta il messaggio di errore.

Parametri:  
* **msg**: messaggio di errore.

