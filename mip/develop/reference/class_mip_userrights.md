---
title: Classe mip::UserRights
description: 'Documenta la classe MIP:: userrights di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f44ff30c890a5a8ab3dbce2426a6c1898df1f0e5
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489300"
---
# <a name="class-mipuserrights"></a>Classe mip::UserRights 
Un gruppo di utenti e i diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRights (const std:: Vector\<std:: String\>& Users, const std:: Vector\<std:: String\>& Rights)  |  Costruttore UserRights.
public const std:: Vector\<std:: String\>& Users () const  |  Ottiene gli utenti associati a un set di diritti.
public const std:: Vector\<std:: String\>& Rights () const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Members
  
### <a name="userrights-function"></a>UserRights (funzione)
Costruttore UserRights.

Parametri:  
* **users**: gruppo di utenti che condividono gli stessi diritti 


* **rights**: diritti condivisi dal gruppo di utenti


  
### <a name="users-function"></a>Funzione Users
Ottiene gli utenti associati a un set di diritti.

  
**Restituisce**: utenti associati a un set di diritti
  
### <a name="rights-function"></a>Rights-funzione
Ottiene i diritti associati a un gruppo di utenti.

  
**Restituisce**: diritti associati a un gruppo di utenti