---
title: 'Classe MIP:: ServiceDisabledError'
description: 'Documenta la classe MIP:: servicedisablederror di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 1481e81707e84d7ba977d36bec152ba86b5e60b6
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489419"
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

  
**Restituisce**: extent per il quale il servizio è disabilitato
  
### <a name="extent-enum"></a>Enumerazione extent
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Utente            | Il servizio è disabilitato per l'utente.
Dispositivo            | Il servizio è disabilitato per il dispositivo.
Platform            | Il servizio è disabilitato per la piattaforma.
Tenant            | Il servizio è disabilitato per il tenant.
Descrive l'ambito per cui il servizio è disabilitato.