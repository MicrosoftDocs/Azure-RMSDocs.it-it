---
title: 'Classe MIP:: ServiceDisabledError'
description: 'Documenta la classe MIP:: servicedisablederror di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2fb7968ee2443d208ef3370308056eee4832e385
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057015"
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