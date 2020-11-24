---
title: Classe ServiceDisabledError
description: 'Documenta la classe servicedisablederror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: b4ccba889ce025f343293d458f76ae7d63457f4f
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567051"
---
# <a name="class-servicedisablederror"></a>Classe ServiceDisabledError 
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
Piattaforma            | Il servizio è disabilitato per la piattaforma.
Tenant            | Il servizio è disabilitato per il tenant.

Descrive l'ambito per cui il servizio è disabilitato.