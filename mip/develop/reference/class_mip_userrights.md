---
title: Classe mip::UserRights
description: 'Classe MIP:: userrights di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: aadf12606f74d508ba3ebdc1ce0770febd49e142
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251303"
---
# <a name="class-mipuserrights"></a>Classe mip::UserRights 
Gruppo di utenti e diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
pubblica UserRights (const std:: Vector\<std:: String\>& users, const std:: Vector\<std:: String\>& rights)  |  Costruttore [UserRights](class_mip_userrights.md).
Public std:: Vector const\<std:: String\>& Users() const  |  Ottiene gli utenti associati a un set di diritti.
Public std:: Vector const\<std:: String\>& Rights() const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userrights-function"></a>Funzione UserRights
Costruttore [UserRights](class_mip_userrights.md).

Parametri:  
* **gli utenti**: Gruppo di utenti che condividono gli stessi diritti 


* **diritti**: Diritti condivisi dal gruppo di utenti


  
### <a name="users-function"></a>Funzione di utenti
Ottiene gli utenti associati a un set di diritti.

  
**Restituisce**: Utenti associati a un set di diritti
  
### <a name="rights-function"></a>Diritti (funzione)
Ottiene i diritti associati a un gruppo di utenti.

  
**Restituisce**: Diritti associati a un gruppo di utenti
