---
title: Classe UserRoles
description: 'Documenta la classe UserRoles:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: ef881f184fd370665006c8fb4d73138b7c5e2f3c
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214134"
---
# <a name="class-userroles"></a>Classe UserRoles 
Un gruppo di utenti e i ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: Vector \<std::string\>& Users, const std:: vector \<std::string\>& Roles)  |  Costruttore UserRoles.
public const std:: Vector \<std::string\>& Users () const  |  Ottiene gli utenti associati a un set di ruoli.
public const std:: Vector \<std::string\>& Roles () const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
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