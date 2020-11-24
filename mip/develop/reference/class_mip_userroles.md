---
title: Classe UserRoles
description: 'Documenta la classe UserRoles:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc6e5f77c68ecde2582cfd622624c0c6b986500b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566621"
---
# <a name="class-userroles"></a>Classe UserRoles 
Un gruppo di utenti e i ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: Vector \<std::string\>& Users, const std:: vector \<std::string\>& Roles)  |  Costruttore UserRoles.
public const std:: Vector \<std::string\>& Users () const  |  Ottiene gli utenti associati a un set di ruoli.
public const std:: Vector \<std::string\>& Roles () const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
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