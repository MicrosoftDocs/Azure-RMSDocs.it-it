---
title: 'Classe MIP:: Identity'
description: 'Documenta la classe MIP:: Identity di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d2fefceb87a1bab042fc8b0aeb817421cd9025f1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885552"
---
# <a name="class-mipidentity"></a>Classe MIP:: Identity 
Astrazione per Identity.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Identità pubblica ()  |  Costruttore di [identità](class_mip_identity.md) predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
Identità pubblica (const Identity & other)  |  Costruttore di copia [Identity](class_mip_identity.md) .
Identità esplicita pubblica (const std:: String & email)  |  Costruttore di [identità](class_mip_identity.md) usato quando un indirizzo di posta elettronica dell'utente è noto.
public const std:: String & getEmail () const  |  Ricevere il messaggio di posta elettronica.
  
## <a name="members"></a>Members
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di [identità](class_mip_identity.md) predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di copia [Identity](class_mip_identity.md) .

Parametri:  
* **[Identity](class_mip_identity.md)** : usata per creare la copia.


  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di [identità](class_mip_identity.md) usato quando un indirizzo di posta elettronica dell'utente è noto.

Parametri:  
* **email**: indirizzo di posta elettronica dell'utente.


  
### <a name="getemail-function"></a>Funzione getEmail
Ricevere il messaggio di posta elettronica.

  
**Restituisce**: Messaggio di posta elettronica.