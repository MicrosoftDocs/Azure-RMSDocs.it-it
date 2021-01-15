---
title: Classe DelegationLicense
description: 'Documenta la classe delegationlicense:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: cfb719a68650b2159574dd6f8d92fb3d0c15a2c1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225072"
---
# <a name="class-delegationlicense"></a>Classe DelegationLicense 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<uint8_t\>& GetSerializedDelegationJsonLicense ()  |  Ottiene la licenza di delega.
public const std:: Vector \<uint8_t\>& GetSerializedUserLicense (ProtectionHandler::P formato relicenseformat)  |  Ottiene la licenza utente, se richiesta.
public const std:: String& GetUser ()  |  Ottiene l'utente per il quale è stata creata la licenza.
  
## <a name="members"></a>Membri
  
### <a name="getserializeddelegationjsonlicense-function"></a>GetSerializedDelegationJsonLicense (funzione)
Ottiene la licenza di delega.

  
**Returns**: licenza serializzata questa licenza è associata all'identità dell'utente che ha effettuato la richiesta
  
### <a name="getserializeduserlicense-function"></a>GetSerializedUserLicense (funzione)
Ottiene la licenza utente, se richiesta.

Parametri  
* **formato**: formato di licenza



  
**Restituisce**: licenza utente serializzata se richiesto; in caso contrario, Vector vuoto questa licenza è associata all'utente delegato nella richiesta
  
### <a name="getuser-function"></a>GetUser (funzione)
Ottiene l'utente per il quale è stata creata la licenza.

  
**Restituisce**: l'utente