---
title: 'Classe MIP:: Identity'
description: 'Documenta la classe MIP:: Identity di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d50092be5277d5e88e6ec408280ca76bbc333a4c
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488025"
---
# <a name="class-mipidentity"></a>Classe MIP:: Identity 
Astrazione per Identity.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Identità pubblica ()  |  Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
Identità pubblica (const Identity & other)  |  Costruttore di copia Identity.
Identità esplicita pubblica (const std:: String & email)  |  Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.
Identità esplicita pubblica (const std:: String & email, const std:: String & name)  |  Costruttore di identità utilizzato quando un indirizzo di posta elettronica utente e un nome utente sono noti.
public const std:: String & getEmail () const  |  Ricevere il messaggio di posta elettronica.
public const std::string& GetName() const  |  Ottenere il nome descrittivo dell'utente. utilizzato per contrassegnare il testo.
  
## <a name="members"></a>Members
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di copia Identity.

Parametri:  
* **Identity**: usata per creare la copia.


  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.

Parametri:  
* **email**: deve essere un indirizzo di posta elettronica valido.


  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità utilizzato quando un indirizzo di posta elettronica utente e un nome utente sono noti.

Parametri:  
* **email**: deve essere un indirizzo di posta elettronica valido. 


* **nome**: nome utente.


  
### <a name="getemail-function"></a>Funzione getEmail
Ricevere il messaggio di posta elettronica.

  
**Restituisce**: il messaggio di posta elettronica.
  
### <a name="getname-function"></a>GetName (funzione)
Ottenere il nome descrittivo dell'utente. utilizzato per contrassegnare il testo.

  
**Returns**: nome descrittivo.