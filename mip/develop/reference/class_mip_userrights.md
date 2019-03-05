---
title: Classe mip::UserRights
description: 'Classe MIP:: userrights di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2a45f7bc9947984f9189b10bd886a53807b3abdb
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332671"
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
