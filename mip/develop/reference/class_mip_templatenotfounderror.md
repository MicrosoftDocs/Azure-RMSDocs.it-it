---
title: 'Classe MIP:: TemplateNotFoundError'
description: 'Documenta la classe MIP:: templatenotfounderror di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: babcf77de224a75b2beec7e0b15c867698b49c15
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489317"
---
# <a name="class-miptemplatenotfounderror"></a>Classe MIP:: TemplateNotFoundError 
ID modello non riconosciuto dal servizio RMS.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String mMessage  | _Non ancora documentato._
public std:: Map\<std:: String, std:: String\> mDebugInfo  | _Non ancora documentato._
public char const* what() const  |  Ottiene il messaggio di errore.
public std:: shared_ptr\<Error\> Clone () const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public const std:: String & geterrorname () const  |  Ottiene il nome dell'errore.
public const std:: String & GetMessage () const  |  Ottiene il messaggio di errore.
public void semessage (const std:: String & msg)  |  Imposta il messaggio di errore.
public void AddDebugInfo (const std:: String & Key, const std:: String & value)  |  Aggiungere la voce di informazioni di debug.
public const std:: Map\<std:: String, std:: String\>& GetDebugInfo () const  |  Ottenere le informazioni di debug.
  
## <a name="members"></a>Members
  
### <a name="mmessage"></a>mMessage
_Non ancora documentato._

  
### <a name="mdebuginfo"></a>mDebugInfo
_Non ancora documentato._

  
### <a name="what-function"></a>funzione
Ottiene il messaggio di errore.

  
**Restituisce**: messaggio di errore
  
### <a name="clone-function"></a>Funzione clone
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

  
**Restituisce**: messaggio di errore.
  
### <a name="setmessage-function"></a>Funzione semessage
Imposta il messaggio di errore.

Parametri:  
* **msg**: messaggio di errore.


  
### <a name="adddebuginfo-function"></a>AddDebugInfo (funzione)
Aggiungere la voce di informazioni di debug.

Parametri:  
* **chiave**: chiave informazioni di debug 


* **valore**: valore informazioni di debug


  
### <a name="getdebuginfo-function"></a>GetDebugInfo (funzione)
Ottenere le informazioni di debug.

  
**Restituisce**: informazioni di debug (chiavi/valori)