---
title: classe mip::ConsentDelegate
description: Documenta la classe mip::consentdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ff6666afa2c87f8988f2d9e92d77eb07e3ce9bb0
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184723"
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