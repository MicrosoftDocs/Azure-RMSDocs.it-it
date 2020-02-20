---
title: 'Classe MIP:: MsgAttachmentData'
description: 'Documenta la classe MIP:: msgattachmentdata di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f9f47ca1503c912840fe1ed43542b5a4b4f2d0ec
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487668"
---
# <a name="class-mipmsgattachmentdata"></a>Classe MIP:: MsgAttachmentData 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<uint8_t\>& GetBytes ()  |  Ottenere un allegato come vettore di byte binario.
public std:: shared_ptr\<Stream\> GetStream () const  |  Ottenere un allegato come flusso binario.
public const std::string& GetName() const  |  Ottenere il nome dell'allegato sotto forma di stringa.
public const std:: String & getlongname () const  |  Ottenere il nome lungo dell'allegato sotto forma di stringa.
public const std::string& GetPath() const  |  Ottenere il nome del percorso dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
public const std:: String & GetLongPath () const  |  Ottiene il nome del percorso lungo dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
  
## <a name="members"></a>Members
  
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