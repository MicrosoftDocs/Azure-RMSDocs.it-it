---
title: classe mip::ServiceDisabledError
description: Documenta la classe mip::servicedisablederror di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2d64d576ead748adff7804e9068aab71fd9672c0
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333025"
---
# <a name="class-mipservicedisablederror"></a>classe mip::ServiceDisabledError 
L'utente non è stato possibile ottenere l'accesso al contenuto a causa di un servizio viene disabilitato.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Extent GetExtent() const  |  Ottiene l'estensione per il quale il servizio è disabilitato.
public char const* what() const  |  Ottiene il messaggio di errore.
Public std:: shared_ptr\<errore\> clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public virtual const std::string& GetErrorName() const  |  Ottiene il nome dell'errore.
public virtual const std::string& GetMessage() const  |  Ottiene il messaggio di errore.
public virtual void SetMessage(const std::string& msg)  |  Imposta il messaggio di errore.
Enumerazione Extent  |  Descrive l'estensione per il quale il servizio è disabilitato.
  
## <a name="members"></a>Membri
  
### <a name="getextent-function"></a>GetExtent (funzione)
Ottiene l'estensione per il quale il servizio è disabilitato.

  
**Restituisce**: Estensione per il quale il servizio è disabilitato
  
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


  
### <a name="extent-enum"></a>Enumerazione extent
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Utente            | Servizio è disabilitato per l'utente.
Dispositivo            | Servizio è disabilitato per il dispositivo.
Piattaforma            | Servizio è disabilitato per la piattaforma.
Tenant            | Servizio è disabilitato per il tenant.
Descrive l'estensione per il quale il servizio è disabilitato.
