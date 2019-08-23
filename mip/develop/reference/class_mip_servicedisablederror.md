---
title: 'Classe MIP:: ServiceDisabledError'
description: 'Documenta la classe MIP:: servicedisablederror di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 6496b2b8967571454c205b84b01a6e4b74456c17
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882927"
---
# <a name="class-mipservicedisablederror"></a>Classe MIP:: ServiceDisabledError 
L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione di un servizio.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Extent pubblico GetExtent () const  |  Ottiene l'extent per il quale il servizio è disabilitato.
Extent enum  |  Descrive l'ambito per cui il servizio è disabilitato.
  
## <a name="members"></a>Members
  
### <a name="getextent-function"></a>Funzione GetExtent
Ottiene l'extent per il quale il servizio è disabilitato.

  
**Restituisce**: Extent per cui il servizio è disabilitato
  
### <a name="extent-enum"></a>Enumerazione extent
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Utente            | Il servizio è disabilitato per l'utente.
Dispositivo            | Il servizio è disabilitato per il dispositivo.
Piattaforma            | Il servizio è disabilitato per la piattaforma.
Tenant            | Il servizio è disabilitato per il tenant.
Descrive l'ambito per cui il servizio è disabilitato.