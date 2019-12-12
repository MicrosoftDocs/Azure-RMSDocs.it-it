---
title: 'Classe MIP:: MsgInspector'
description: 'Documenta la classe MIP:: msginspector di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d1234168e4ce3996077b705e904f5765b761ec4c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558618"
---
# <a name="class-mipmsginspector"></a>Classe MIP:: MsgInspector 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<uint8_t\>& GetBody ()  |  Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.
public BodyType GetBodyType () const  |  Ottiene il tipo di corpo.
public const std:: Vector\<std:: unique_ptr\<MsgAttachmentData\>\>& GetAttributes () const  |  Ottenere un elenco di allegati come oggetti dati dell'allegato msg.
  
## <a name="members"></a>Membri
  
### <a name="getbody-function"></a>Funzione GetBody
Ottenere il corpo del messaggio. se TXT/HTML è formattato come UTF8.

  
**Restituisce**: un vettore di byte.
  
### <a name="getbodytype-function"></a>GetBodyType (funzione)
Ottiene il tipo di corpo.

  
**Returns**: tipo di corpo del messaggio.
  
### <a name="getattachments-function"></a>Funzione GetAttributes
Ottenere un elenco di allegati come oggetti dati dell'allegato msg.

  
**Restituisce**: un vettore di STD:: unique_ptr<MsgAttachmentData>