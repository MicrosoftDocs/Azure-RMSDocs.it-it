---
title: Classe mip::UserRoles
description: 'Classe MIP:: UserRoles di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 1a060652ea61ed452867bb67d281c9531f4e1b98
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651514"
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