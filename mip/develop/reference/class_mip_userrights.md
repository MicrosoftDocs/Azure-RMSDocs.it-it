---
title: Classe mip::UserRights
description: 'Documenta la classe MIP:: userrights di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 1df26089f37b1e89be8749aa1bc862f0d3a729ba
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558389"
---
# <a name="class-mipuserrights"></a>Classe mip::UserRights 
Gruppo di utenti e diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRights (const std:: Vector\<std:: String\>& Users, const std:: Vector\<std:: String\>& Rights)  |  Costruttore UserRights.
public const std:: Vector\<std:: String\>& Users () const  |  Ottiene gli utenti associati a un set di diritti.
public const std:: Vector\<std:: String\>& Rights () const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
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