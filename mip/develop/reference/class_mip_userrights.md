---
title: Classe UserRights
description: 'Documenta la classe userrights:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 1a3bf2c6c8f417d30fac24263f672f2603347960
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764256"
---
# <a name="class-userrights"></a>Classe UserRights 
Gruppo di utenti e diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRights (const std::\<vector std::\> String& Users, const std\<:: Vector STD\> :: String& Rights)  |  Costruttore UserRights.
public const std::\<vector std::\> String& Users () const  |  Ottiene gli utenti associati a un set di diritti.
public const std::\<vector std::\> String& Rights () const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Members
  
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