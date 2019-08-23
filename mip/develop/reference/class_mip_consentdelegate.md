---
title: 'Classe MIP:: ConsentDelegate'
description: 'Documenta la classe MIP:: consentdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: ea088c9d92712243f3c628c17fadb0e61831103b
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884424"
---
# <a name="class-mipconsentdelegate"></a>Classe MIP:: ConsentDelegate 
Delegato per le operazioni relative al consenso.
Questo delegato viene implementato da un'applicazione client per sapere quando è necessario mostrare all'utente una notifica di una richiesta di consenso.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  Viene chiamato quando l'SDK richiede il consenso dell'utente per connettersi a un endpoint di servizio.
  
## <a name="members"></a>Members
  
### <a name="getuserconsent-function"></a>GetUserConsent (funzione)
Viene chiamato quando l'SDK richiede il consenso dell'utente per connettersi a un endpoint di servizio.

Parametri:  
* **URL**: URL per cui l'SDK richiede il consenso dell'utente



  
**Restituisce**: Enum di consenso con la decisione dell'utente.
Quando l'SDK richiede il consenso dell'utente con questo metodo, l'applicazione client deve presentare all'utente l'URL. Le applicazioni client devono offrire un modo per ottenere il consenso dell'utente e restituire l'enumerazione di consenso appropriata che corrisponde alla decisione dell'utente.