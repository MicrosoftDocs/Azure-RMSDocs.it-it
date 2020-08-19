---
title: Classe ServiceDisabledError
description: 'Documenta la classe servicedisablederror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3dc6d73f12dc1512d1850d465a966e99d13b52c9
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564454"
---
# <a name="class-servicedisablederror"></a>Classe ServiceDisabledError

L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione di un servizio.
  
## <a name="summary"></a>Riepilogo

| Membri                          | Descrizioni
|----------------------------------|--------------------------------------------------------
| Extent pubblico GetExtent () const  | Ottiene l'extent per il quale il servizio è disabilitato.
| Extent enum                      | Descrive l'ambito per cui il servizio è disabilitato.
  
## <a name="members"></a>Membri
  
### <a name="getextent-function"></a>Funzione GetExtent
Ottiene l'extent per il quale il servizio è disabilitato.

**Restituisce**: extent per il quale il servizio è disabilitato
  
### <a name="extent-enum"></a>Enumerazione extent

Descrive l'ambito per cui il servizio è disabilitato.

| Valori   | Descrizioni
|----------|---------------------------------------
| Utente     | Il servizio è disabilitato per l'utente.
| Dispositivo   | Il servizio è disabilitato per il dispositivo.
| Piattaforma | Il servizio è disabilitato per la piattaforma.
| Tenant   | Il servizio è disabilitato per il tenant.
