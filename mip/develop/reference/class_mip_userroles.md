---
title: Classe UserRoles
description: 'Documenta la classe UserRoles:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: bbff817578bb5ba1fe143c850632e25df8f78708
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764208"
---
# <a name="class-userroles"></a>Classe UserRoles 
Un gruppo di utenti e i ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRoles (const std::\<vector std::\> String& Users, const std\<:: Vector STD\> :: String& Roles)  |  Costruttore UserRoles.
public const std::\<vector std::\> String& Users () const  |  Ottiene gli utenti associati a un set di ruoli.
public const std::\<vector std::\> String& Roles () const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Members
  
### <a name="userroles-function"></a>UserRoles (funzione)
Costruttore UserRoles.

Parametri  
* **users**: gruppo di utenti che condividono gli stessi ruoli 


* **roles**: ruoli condivisi dal gruppo di utenti


  
### <a name="users-function"></a>Funzione Users
Ottiene gli utenti associati a un set di ruoli.

  
**Restituisce**: utenti associati a un set di ruoli
  
### <a name="roles-function"></a>Roles-funzione
Ottiene i ruoli associati a un gruppo di utenti.

  
**Restituisce**: ruoli associati a un gruppo di utenti