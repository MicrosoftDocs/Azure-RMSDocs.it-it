---
title: 'Classe MIP:: MsgInspector'
description: 'Documenta la classe MIP:: msginspector di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 274ada562bae46add2429a2f87442bb77528ea05
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054265"
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