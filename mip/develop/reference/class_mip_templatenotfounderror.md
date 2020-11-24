---
title: Classe TemplateNotFoundError
description: 'Documenta la classe templatenotfounderror:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 0ba4eae1c1c3d846c5e696a55a8a089b18a583ed
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567393"
---
# <a name="class-templatenotfounderror"></a>Classe TemplateNotFoundError 
ID modello non riconosciuto dal servizio RMS.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
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
  
## <a name="members"></a>Members
  
### <a name="mmessage"></a>mMessage
Non ancora documentato.

  
### <a name="mdebuginfo"></a>mDebugInfo
Non ancora documentato.

  
### <a name="mname"></a>mName
Non ancora documentato.

  
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

 Valori                         | Descrizioni                                
--------------------------------|---------------------------------------------
Generale            | Errore generale di input non valido
FileIsTooLargeForProtection            | Il file è troppo grande per la protezione

Errore di input errato.