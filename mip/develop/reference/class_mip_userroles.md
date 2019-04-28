---
title: Classe mip::UserRoles
description: 'Classe MIP:: UserRoles di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7e9e750f5b327dbad5e9b46fa1eca2a3291abdd3
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173242"
---
# <a name="class-mipuserroles"></a>Classe mip::UserRoles 
Gruppo di utenti e ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
ruoli utente pubblica (const std:: Vector\<std:: String\>& users, const std:: Vector\<std:: String\>& ruoli)  |  Costruttore [UserRoles](class_mip_userroles.md).
Public std:: Vector const\<std:: String\>& Users() const  |  Ottiene gli utenti associati a un set di ruoli.
Public std:: Vector const\<std:: String\>& Roles() const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userroles-function"></a>Funzione UserRoles
Costruttore [UserRoles](class_mip_userroles.md).

Parametri:  
* **gli utenti**: Gruppo di utenti che condividono gli stessi ruoli 


* **ruoli**: Ruoli condivisi dal gruppo di utenti


  
### <a name="users-function"></a>Funzione di utenti
Ottiene gli utenti associati a un set di ruoli.

  
**Restituisce**: Utenti associati a un set di ruoli
  
### <a name="roles-function"></a>Funzione di ruoli
Ottiene i ruoli associati a un gruppo di utenti.

  
**Restituisce**: Ruoli associati a un gruppo di utenti