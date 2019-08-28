---
title: 'Classe MIP:: Identity'
description: 'Documenta la classe MIP:: Identity di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8bb4e30398e6f12214605df6f5ad194334d3eeff
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054782"
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