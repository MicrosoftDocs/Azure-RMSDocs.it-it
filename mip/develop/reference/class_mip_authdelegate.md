---
title: classe mip::AuthDelegate
description: Documenta la classe mip::authdelegate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cf6ea43b36518f2eec74b9ed0f8682466aa6b64d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258012"
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

