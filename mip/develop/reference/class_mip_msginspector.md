---
title: 'Classe MIP:: MsgInspector'
description: 'Documenta la classe MIP:: msginspector di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: cb0b85b0de42eae46d6cd7c9c6d6e18680b2e545
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69892750"
---
# <a name="class-mipmsginspector"></a>Classe MIP:: MsgInspector 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::\<vector\>uint8_t & GetBody ()  |  Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.
public BodyType GetBodyType () const  |  Ottiene il tipo di corpo.
public const std::\<vector std::\<unique_ptr\>MsgAttachmentData\>& GetAttributes () const  |  Ottenere un elenco di allegati come oggetti dati dell'allegato msg.
public InspectorType GetInspectorType () const  |  Ottenere i tipi di file.
public std:: shared_ptr\<Stream\> GetFileStream () const  |  Ottenere il flusso di file.
  
## <a name="members"></a>Members
  
### <a name="getbody-function"></a>Funzione GetBody
Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.

  
**Restituisce**: Vettore di byte.
  
### <a name="getbodytype-function"></a>GetBodyType (funzione)
Ottiene il tipo di corpo.

  
**Restituisce**: Tipo di corpo del messaggio.
  
### <a name="getattachments-function"></a>Funzione GetAttributes
Ottenere un elenco di allegati come oggetti dati dell'allegato msg.

  
**Restituisce**: Vettore di STD:: unique_ptr<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType (funzione)
Ottenere i tipi di file.

  
**Restituisce**: InspectorType.
  
### <a name="getfilestream-function"></a>Funzione GetFileStream
Ottenere il flusso di file.

  
**Restituisce**: Un PTR condiviso al flusso di file.