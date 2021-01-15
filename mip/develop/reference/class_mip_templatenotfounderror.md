---
title: Classe TemplateNotFoundError
description: 'Documenta la classe templatenotfounderror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 48182ae5d821aeed65e8c28b086dce0349b9af03
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212859"
---
# <a name="class-templatenotfounderror"></a>Classe TemplateNotFoundError 
ID modello non riconosciuto dal servizio RMS.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String mMessage  | _Non ancora documentato._
public std:: Map \<std::string, std::string\> mDebugInfo  | _Non ancora documentato._
public std:: string mName  | _Non ancora documentato._
public ErrorCode GetErrorCode () const  |  Ottiene il codice errorCode dell'input errato.
public char const* what() const  |  Ottiene il messaggio di errore.
public std::shared_ptr\<Error\> Clone() const  |  Clona l'errore.
public virtual ErrorType GetErrorType() const  |  Ottiene il tipo di errore.
public const std:: String& geterrorname () const  |  Ottiene il nome dell'errore.
public const std:: String& GetMessage () const  |  Ottiene il messaggio di errore.
public void semessage (const std:: String& msg)  |  Imposta il messaggio di errore.
public void AddDebugInfo (const std:: String& Key, const std:: String& value)  |  Aggiungere la voce di informazioni di debug.
public const std:: Map \<std::string, std::string\>& GetDebugInfo () const  |  Ottenere le informazioni di debug.
ErrorCode enum  |  Errore di input errato.
  
## <a name="members"></a>Membri
  
### <a name="mmessage"></a>mMessage
_Non ancora documentato._

  
### <a name="mdebuginfo"></a>mDebugInfo
_Non ancora documentato._

  
### <a name="mname"></a>mName
_Non ancora documentato._

  
### <a name="geterrorcode-function"></a>GetErrorCode (funzione)
Ottiene il codice errorCode dell'input errato.

  
**Restituisce**: codice errore errore di input errato
  
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
  
### <a name="errorcode-enum"></a>Enumerazione ErrorCode

Errore di input errato.

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Generale            | Errore generale di input non valido
FileIsTooLargeForProtection            | Il file è troppo grande per la protezione
