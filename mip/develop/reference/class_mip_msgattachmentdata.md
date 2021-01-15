---
title: Classe MsgAttachmentData
description: 'Documenta la classe msgattachmentdata:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 6082b96649e32e282c544ac5ec46773e7b4be901
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213624"
---
# <a name="class-msgattachmentdata"></a>Classe MsgAttachmentData 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<uint8_t\>& GetBytes ()  |  Ottenere un allegato come vettore di byte binario.
public std:: shared_ptr \<Stream\> GetStream () const  |  Ottenere un allegato come flusso binario.
public const std::string& GetName() const  |  Ottenere il nome dell'allegato sotto forma di stringa.
public const std:: String& getlongname () const  |  Ottenere il nome lungo dell'allegato sotto forma di stringa.
public const std::string& GetPath() const  |  Ottenere il nome del percorso dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
public const std:: String& GetLongPath () const  |  Ottiene il nome del percorso lungo dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
  
## <a name="members"></a>Membri
  
### <a name="getbytes-function"></a>Funzione GetBytes
Ottenere un allegato come vettore di byte binario.
  
### <a name="getstream-function"></a>Funzione GetStream
Ottenere un allegato come flusso binario.
  
### <a name="getname-function"></a>GetName (funzione)
Ottenere il nome dell'allegato sotto forma di stringa.
  
### <a name="getlongname-function"></a>Getlongname (funzione)
Ottenere il nome lungo dell'allegato sotto forma di stringa.
  
### <a name="getpath-function"></a>GetPath (funzione)
Ottenere il nome del percorso dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
  
### <a name="getlongpath-function"></a>GetLongPath (funzione)
Ottiene il nome del percorso lungo dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.