---
title: classe mip::AuthDelegate
description: Documenta la classe mip::authdelegate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6278d605dfbb9a9c4cf0cf1282a159c456c5561
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651997"
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

