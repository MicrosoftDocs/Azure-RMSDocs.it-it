---
title: Classe UserRights
description: 'Documenta la classe userrights:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 37943d284eaa00524797605158e320c25e52e17b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567392"
---
# <a name="class-userrights"></a>Classe UserRights 
Gruppo di utenti e diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRights (const std:: Vector \<std::string\>& Users, const std:: vector \<std::string\>& Rights)  |  Costruttore UserRights.
public const std:: Vector \<std::string\>& Users () const  |  Ottiene gli utenti associati a un set di diritti.
public const std:: Vector \<std::string\>& Rights () const  |  Ottiene i diritti associati a un gruppo di utenti.
  
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