---
title: Classe UserRights
description: 'Documenta la classe userrights:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 13c9da9ef9cd8b5e1c9c42f48b7f249f69bd7b30
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212808"
---
# <a name="class-userrights"></a>Classe UserRights 
Gruppo di utenti e diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRights (const std:: Vector \<std::string\>& Users, const std:: vector \<std::string\>& Rights)  |  Costruttore UserRights.
public const std:: Vector \<std::string\>& Users () const  |  Ottiene gli utenti associati a un set di diritti.
public const std:: Vector \<std::string\>& Rights () const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userrights-function"></a>UserRights (funzione)
Costruttore UserRights.

Parametri  
* **users**: gruppo di utenti che condividono gli stessi diritti 


* **rights**: diritti condivisi dal gruppo di utenti


  
### <a name="users-function"></a>Funzione Users
Ottiene gli utenti associati a un set di diritti.

  
**Restituisce**: utenti associati a un set di diritti
  
### <a name="rights-function"></a>Rights-funzione
Ottiene i diritti associati a un gruppo di utenti.

  
**Restituisce**: diritti associati a un gruppo di utenti