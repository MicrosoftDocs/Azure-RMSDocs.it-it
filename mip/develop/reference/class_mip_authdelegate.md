---
title: classe mip::AuthDelegate
description: Documenta la classe mip::authdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bcc38bf4b55ca99cf926138279223a4140f7bbf4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184842"
---
# <a name="class-mipauthdelegate"></a>classe mip::AuthDelegate 
Delegato per l'autenticazione di operazioni correlate.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public bool AcquireOAuth2Token (const MIP, identità, const OAuth2Challenge & sfida, OAuth2Token & token)  |  Questo metodo viene chiamato quando un token di autorizzazione è necessario per il motore dei criteri con l'identità fornita e la richiesta di verifica specificato. Il client deve restituire se l'acquisizione di token è riuscita. Se l'operazione riesce, deve inizializzare l'oggetto di token specificato.
  
## <a name="members"></a>Membri
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (funzione)
Questo metodo viene chiamato quando un token di autorizzazione è necessario per il motore dei criteri con l'identità fornita e la richiesta di verifica specificato. Il client deve restituire se l'acquisizione di token è riuscita. Se l'operazione riesce, deve inizializzare l'oggetto di token specificato.

Parametri:  
* **identity**: 


* **challenge**: 


* **token**:

