---
title: Classe ConsentDelegate
description: Riferimento per la classe ConsentDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 841049b1e6b369eb2f6a34d9701ed34eca028af6
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446363"
---
# <a name="class-consentdelegate"></a>Classe ConsentDelegate 
Delegato per le operazioni relative al consenso.
Questo delegato viene implementato da un'applicazione client per sapere quando è necessario mostrare all'utente una notifica di una richiesta di consenso.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  Viene chiamato quando l'SDK richiede il consenso dell'utente per connettersi a un endpoint di servizio.
  
## <a name="members"></a>Membri
  
### <a name="consent"></a>Consent
Viene chiamato quando l'SDK richiede il consenso dell'utente per connettersi a un endpoint di servizio.

Parametri:  
* **url**: URL per cui l'SDK richiede il consenso dell'utente



  
**Restituisce**: enumerazione di consenso con la decisione dell'utente.
Quando l'SDK richiede il consenso dell'utente con questo metodo, l'applicazione client deve presentare all'utente l'URL. Le applicazioni client devono offrire un modo per ottenere il consenso dell'utente e restituire l'enumerazione di consenso appropriata che corrisponde alla decisione dell'utente.