---
title: Identità della classe
description: 'Documents the Identity:: undefined Class of the Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d1ec599e486466a1e5016025d1c5e04ae09e64ee
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215239"
---
# <a name="class-identity"></a>Identità della classe 
Astrazione per Identity.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Identità pubblica ()  |  Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
Identità pubblica (const Identity& other)  |  Costruttore di copia Identity.
Identità esplicita pubblica (const std:: String& email)  |  Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.
Identità esplicita pubblica (const std:: String& email, const std:: String& Name)  |  Costruttore di identità utilizzato quando un indirizzo di posta elettronica utente e un nome utente sono noti.
public const std:: String& getEmail () const  |  Ricevere il messaggio di posta elettronica.
public const std::string& GetName() const  |  Ottenere il nome descrittivo dell'utente. utilizzato per contrassegnare il testo.
  
## <a name="members"></a>Membri
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di copia Identity.

Parametri  
* **Identity**: usata per creare la copia.


  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.

Parametri  
* **email**: deve essere un indirizzo di posta elettronica valido.


  
### <a name="identity-function"></a>Identity (funzione)
Costruttore di identità utilizzato quando un indirizzo di posta elettronica utente e un nome utente sono noti.

Parametri  
* **email**: deve essere un indirizzo di posta elettronica valido. 


* **nome**: nome utente.


  
### <a name="getemail-function"></a>Funzione getEmail
Ricevere il messaggio di posta elettronica.

  
**Restituisce**: il messaggio di posta elettronica.
  
### <a name="getname-function"></a>GetName (funzione)
Ottenere il nome descrittivo dell'utente. utilizzato per contrassegnare il testo.

  
**Returns**: nome descrittivo.