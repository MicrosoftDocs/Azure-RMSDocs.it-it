---
title: Classe DelegationLicenseSettings
description: 'Documenta la classe delegationlicensesettings:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 947accd8104f8eda9f7b7320a1fbdb956810f34d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224925"
---
# <a name="class-delegationlicensesettings"></a>Classe DelegationLicenseSettings 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr \<const PublishingLicenseInfo\> GetLicenseInfo () const  |  Ottiene PublishingLicenseInfo, la licenza di pubblicazione.
public const std:: Vector \<std::string\>& GetUsers () const  |  Ottiene l'elenco di utenti per la richiesta.
public bool GetAquireEndUserLicenses () const  |  Ottiene il valore booleano che indica se ottenere la licenza per l'utente finale oltre alla licenza delegata.
  
## <a name="members"></a>Membri
  
### <a name="getlicenseinfo-function"></a>GetLicenseInfo (funzione)
Ottiene PublishingLicenseInfo, la licenza di pubblicazione.

  
**Restituisce**: PublishingLicenseInfo
  
### <a name="getusers-function"></a>GetUsers (funzione)
Ottiene l'elenco di utenti per la richiesta.

  
**Restituisce**: gli utenti
  
### <a name="getaquireenduserlicenses-function"></a>GetAquireEndUserLicenses (funzione)
Ottiene il valore booleano che indica se ottenere la licenza per l'utente finale oltre alla licenza delegata.

  
**Restituisce**: indica se acquisire le licenze dell'utente finale