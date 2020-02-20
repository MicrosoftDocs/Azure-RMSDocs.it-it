---
title: 'Classe MIP:: ConsentDelegate'
description: 'Documenta la classe MIP:: consentdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: bbeca67a1ffcd5a7b159883c97a2eb3a08bfb3e2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490320"
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
* **url**: URL per cui l'SDK richiede il consenso dell'utente



  
**Restituisce**: enumerazione di consenso con la decisione dell'utente.
Quando l'SDK richiede il consenso dell'utente con questo metodo, l'applicazione client deve presentare all'utente l'URL. Le applicazioni client devono offrire un modo per ottenere il consenso dell'utente e restituire l'enumerazione di consenso appropriata che corrisponde alla decisione dell'utente.