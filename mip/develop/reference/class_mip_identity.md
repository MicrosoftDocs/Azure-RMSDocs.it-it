---
title: 'Classe MIP:: Identity'
description: 'Documenta la classe MIP:: Identity di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 633a0ac8536f7bbd285eee67934f27d65b399bf4
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560153"
---
# <a name="class-mipidentity"></a>Classe MIP:: Identity 
Astrazione per Identity.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Identità pubblica ()  |  Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
Identità pubblica (const Identity & other)  |  Costruttore di copia Identity.
Identità esplicita pubblica (const std:: String & email)  |  Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.
public const std:: String & getEmail () const  |  Ricevere il messaggio di posta elettronica.
  
## <a name="members"></a>Membri
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di copia Identity.

Parametri:  
* **Identity**: usata per creare la copia.


  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.

Parametri:  
* **email**: indirizzo di posta elettronica dell'utente.


  
### <a name="getemail-function"></a>Funzione getEmail
Ricevere il messaggio di posta elettronica.

  
**Restituisce**: il messaggio di posta elettronica.