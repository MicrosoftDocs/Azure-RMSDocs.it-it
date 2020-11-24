---
title: Classe MsgInspector
description: 'Documenta la classe msginspector:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 9f19c53a2c6eca82cdf1469c63436ad56112dc52
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567944"
---
# <a name="class-msginspector"></a>Classe MsgInspector 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<uint8_t\>& GetBody () const  |  Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.
public unsigned int GetCodePage () const  |  Ottenere la tabella codici di codifica del corpo, pertinente per txt, formati HTML del corpo.
public BodyType GetBodyType () const  |  Ottiene il tipo di corpo.
public const std:: Vector \<std::shared_ptr\<MsgAttachmentData\> \>& GetAttributes () const  |  Ottenere un elenco di allegati come oggetti dati dell'allegato msg.
public InspectorType GetInspectorType () const  |  Ottenere i tipi di file.
public std:: shared_ptr \<Stream\> GetFileStream () const  |  Ottenere il flusso di file.
  
## <a name="members"></a>Members
  
### <a name="getbody-function"></a>Funzione GetBody
Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.

  
**Restituisce**: un vettore di byte.
  
### <a name="getcodepage-function"></a>GetCodePage (funzione)
Ottenere la tabella codici di codifica del corpo, pertinente per txt, formati HTML del corpo.

  
**Returns**: tabella codici senza segno. 
  
**Vedere anche**: [https://docs.microsoft.com/en-us/windows/win32/intl/code-page-identifiers](/windows/win32/intl/code-page-identifiers)
  
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