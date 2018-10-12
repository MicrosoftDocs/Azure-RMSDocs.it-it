---
title: Classe mip UserRights
description: Riferimento per la classe mip UserRights
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c1ef7aaba00bf595d80f07f318aa5808f3a56409
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445122"
---
# <a name="class-mipuserrights"></a>Classe mip::UserRights 
Un gruppo di utenti e i diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRights(const std::vector<std::string>& users, const std::vector<std::string>& rights)  |  Costruttore [UserRights](class_mip_userrights.md).
public const std::vector<std::string>& Users() const  |  Ottiene gli utenti associati a un set di diritti.
public const std::vector<std::string>& Rights() const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userrights"></a>UserRights
Costruttore [UserRights](class_mip_userrights.md).

Parametri:  
* **users**: gruppo di utenti che condividono gli stessi diritti 


* **rights**: diritti condivisi dal gruppo di utenti


  
### <a name="users"></a>Users
Ottiene gli utenti associati a un set di diritti.

  
**Restituisce**: utenti associati a un set di diritti
  
### <a name="rights"></a>Diritti
Ottiene i diritti associati a un gruppo di utenti.

  
**Restituisce**: diritti associati a un gruppo di utenti