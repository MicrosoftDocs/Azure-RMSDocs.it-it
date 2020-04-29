---
title: Classe TemplateNotFoundError
description: 'Documenta la classe templatenotfounderror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 9c8a1f1d89c581950bc1760a7bcb339e10114c2a
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764235"
---
# <a name="class-templatenotfounderror"></a>Classe TemplateNotFoundError 
ID modello non riconosciuto dal servizio RMS.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String mMessage  | _Non ancora documentato._
public std:: Map\<std:: String, std:: String\> mDebugInfo  | _Non ancora documentato._
public char const* what() const  |  Ottiene il messaggio di errore.
public std:: shared_ptr\<Error\> Clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public const std:: String& geterrorname () const  |  Ottiene il nome dell'errore.
public const std:: String& GetMessage () const  |  Ottiene il messaggio di errore.
public void semessage (const std:: String& msg)  |  Imposta il messaggio di errore.
public void AddDebugInfo (const std:: String& Key, const std:: String& value)  |  Aggiungere la voce di informazioni di debug.
public const std::\<map std:: String, std::\> String& GetDebugInfo () const  |  Ottenere le informazioni di debug.
  
## <a name="members"></a>Members
  
### <a name="mmessage"></a>mMessage
_Non ancora documentato._

  
### <a name="mdebuginfo"></a>mDebugInfo
_Non ancora documentato._

  
### <a name="what-function"></a>funzione
Ottiene il messaggio di errore.

  
**Returns**: messaggio di errore
  
### <a name="clone-function"></a>Funzione Clone
Clona l'errore.

  
**Restituisce**: clone dell'errore.
  
### <a name="geterrortype-function"></a>GetErrorType (funzione)
Ottiene il tipo di errore.

  
**Restituisce**: tipo di errore.
  
### <a name="geterrorname-function"></a>Geterrorname (funzione)
Ottiene il nome dell'errore.

  
**Restituisce**: nome dell'errore.
  
### <a name="getmessage-function"></a>GetMessage (funzione)
Ottiene il messaggio di errore.

  
**Restituisce**: il messaggio di errore.
  
### <a name="setmessage-function"></a>Funzione semessage
Imposta il messaggio di errore.

Parametri  
* **msg**: messaggio di errore.


  
### <a name="adddebuginfo-function"></a>AddDebugInfo (funzione)
Aggiungere la voce di informazioni di debug.

Parametri  
* **chiave**: chiave informazioni di debug 


* **valore**: valore informazioni di debug


  
### <a name="getdebuginfo-function"></a>GetDebugInfo (funzione)
Ottenere le informazioni di debug.

  
**Restituisce**: informazioni di debug (chiavi/valori)