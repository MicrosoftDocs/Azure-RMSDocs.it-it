---
title: classe mip::ConsentDelegate
description: Documenta la classe mip::consentdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 69ffbe72ac9d8241115fecd5bbae28052fb93e33
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333229"
---
# <a name="class-mipconsentdelegate"></a>classe mip::ConsentDelegate 
Delegato per le operazioni relative al consenso.
Questo delegato viene implementato da un'applicazione client per sapere quando è necessario mostrare all'utente una notifica di una richiesta di consenso.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  Viene chiamato quando l'SDK richiede il consenso dell'utente per connettersi a un endpoint di servizio.
  
## <a name="members"></a>Membri
  
### <a name="getuserconsent-function"></a>GetUserConsent (funzione)
Viene chiamato quando l'SDK richiede il consenso dell'utente per connettersi a un endpoint di servizio.

Parametri:  
* **url**: L'URL per cui il SDK richiede il consenso dell'utente



  
**Restituisce**: Un'enumerazione di consenso dell'utente con la decisione dell'utente.
Quando l'SDK richiede il consenso dell'utente con questo metodo, l'applicazione client deve presentare all'utente l'URL. Le applicazioni client devono offrire un modo per ottenere il consenso dell'utente e restituire l'enumerazione di consenso appropriata che corrisponde alla decisione dell'utente.
