---
title: Classe MsgInspector
description: 'Documenta la classe msginspector:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: aaf9cc6803e0111cd37960f356d8a6bb19fd60a5
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215171"
---
# <a name="class-msginspector"></a>Classe MsgInspector 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<uint8_t\>& GetBody () const  |  Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.
public unsigned int GetCodePage () const  |  Ottenere la tabella codici di codifica del corpo, pertinente per txt, formati HTML del corpo.
public BodyType GetBodyType () const  |  Ottiene il tipo di corpo.
public const std:: Vector \<std::shared_ptr\<MsgAttachmentData\> \>& GetAttributes () const  |  Ottenere un elenco di allegati come oggetti dati dell'allegato msg.
public InspectorType GetInspectorType () const  |  Ottenere i tipi di file.
public std:: shared_ptr \<Stream\> GetFileStream () const  |  Ottenere il flusso di file.
  
## <a name="members"></a>Membri
  
### <a name="getbody-function"></a>Funzione GetBody
Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.

  
**Restituisce**: un vettore di byte.
  
### <a name="getcodepage-function"></a>GetCodePage (funzione)
Ottenere la tabella codici di codifica del corpo, pertinente per txt, formati HTML del corpo.

  
**Returns**: tabella codici senza segno. 
  
**Vedere anche**: [https://docs.microsoft.com/en-us/windows/win32/intl/code-page-identifiers](https://docs.microsoft.com/windows/win32/intl/code-page-identifiers)
  
### <a name="getbodytype-function"></a>GetBodyType (funzione)
Ottiene il tipo di corpo.

  
**Returns**: tipo di corpo del messaggio.
  
### <a name="getattachments-function"></a>Funzione GetAttributes
Ottenere un elenco di allegati come oggetti dati dell'allegato msg.

  
**Restituisce**: un vettore di STD:: unique_ptr<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType (funzione)
Ottenere i tipi di file.

  
**Restituisce**: InspectorType.
  
### <a name="getfilestream-function"></a>Funzione GetFileStream
Ottenere il flusso di file.

  
**Restituisce**: un PTR condiviso al flusso di file.