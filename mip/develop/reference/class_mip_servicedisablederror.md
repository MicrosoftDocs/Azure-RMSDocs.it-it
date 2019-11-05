---
title: 'Classe MIP:: ServiceDisabledError'
description: 'Documenta la classe MIP:: servicedisablederror di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 766d3747c2dbe6a9fdecc6cb6e21eb3d4000d3ec
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558199"
---
# <a name="class-mipservicedisablederror"></a>Classe MIP:: ServiceDisabledError 
L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione di un servizio.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Extent pubblico GetExtent () const  |  Ottiene l'extent per il quale il servizio è disabilitato.
Extent enum  |  Descrive l'ambito per cui il servizio è disabilitato.
  
## <a name="members"></a>Membri
  
### <a name="getextent-function"></a>Funzione GetExtent
Ottiene l'extent per il quale il servizio è disabilitato.

  
**Restituisce**: extent per il quale il servizio è disabilitato
  
### <a name="extent-enum"></a>Enumerazione extent
 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Utente            | Il servizio è disabilitato per l'utente.
Dispositivo            | Il servizio è disabilitato per il dispositivo.
Piattaforma            | Il servizio è disabilitato per la piattaforma.
Tenant            | Il servizio è disabilitato per il tenant.
Descrive l'ambito per cui il servizio è disabilitato.