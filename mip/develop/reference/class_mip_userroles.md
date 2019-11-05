---
title: Classe mip::UserRoles
description: 'Documenta la classe MIP:: UserRoles di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e77ed6ae4d4b5467964f855a081cc22780d9869c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560473"
---
# <a name="class-mipuserroles"></a>Classe mip::UserRoles 
Gruppo di utenti e ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: Vector\<std:: String\>& Users, const std:: Vector\<std:: String\>& Roles)  |  Costruttore UserRoles.
public const std:: Vector\<std:: String\>& Users () const  |  Ottiene gli utenti associati a un set di ruoli.
public const std:: Vector\<std:: String\>& Roles () const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
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