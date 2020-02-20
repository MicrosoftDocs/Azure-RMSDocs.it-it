---
title: Classe mip::UserRoles
description: 'Documenta la classe MIP:: UserRoles di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d22f66c8fff22b54e5e7e30f425adc2c889e5db0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489283"
---
# <a name="class-mipuserroles"></a>Classe mip::UserRoles 
Gruppo di utenti e ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: Vector\<std:: String\>& Users, const std:: Vector\<std:: String\>& Roles)  |  Costruttore UserRoles.
public const std:: Vector\<std:: String\>& Users () const  |  Ottiene gli utenti associati a un set di ruoli.
public const std:: Vector\<std:: String\>& Roles () const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Members
  
### <a name="userroles-function"></a>UserRoles (funzione)
Costruttore UserRoles.

Parametri:  
* **users**: gruppo di utenti che condividono gli stessi ruoli 


* **roles**: ruoli condivisi dal gruppo di utenti


  
### <a name="users-function"></a>Funzione Users
Ottiene gli utenti associati a un set di ruoli.

  
**Restituisce**: utenti associati a un set di ruoli
  
### <a name="roles-function"></a>Roles-funzione
Ottiene i ruoli associati a un gruppo di utenti.

  
**Restituisce**: ruoli associati a un gruppo di utenti