---
title: Identità della classe
description: 'Documents the Identity:: undefined Class of the Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ae89ed32a48deae7132bc65adabf86f7fb63ffe1
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566872"
---
# <a name="class-identity"></a>Identità della classe 
Astrazione per Identity.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Identità pubblica ()  |  Costruttore di identità predefinito usato quando un indirizzo di posta elettronica dell'utente non è noto.
Identità pubblica (const Identity& other)  |  Costruttore di copia Identity.
Identità esplicita pubblica (const std:: String& email)  |  Costruttore di identità usato quando un indirizzo di posta elettronica dell'utente è noto.
Identità esplicita pubblica (const std:: String& email, const std:: String& Name)  |  Costruttore di identità utilizzato quando un indirizzo di posta elettronica utente e un nome utente sono noti.
public const std:: String& getEmail () const  |  Ricevere il messaggio di posta elettronica.
public const std::string& GetName() const  |  Ottenere il nome descrittivo dell'utente. utilizzato per contrassegnare il testo.
  
## <a name="members"></a>Members
  
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