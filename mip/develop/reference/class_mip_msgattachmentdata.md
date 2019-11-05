---
title: 'Classe MIP:: MsgAttachmentData'
description: 'Documenta la classe MIP:: msgattachmentdata di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: bef08b98e09f9c6802ac9e39de293e9ec25bd380
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558625"
---
# <a name="class-mipmsgattachmentdata"></a>Classe MIP:: MsgAttachmentData 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<uint8_t\>& GetBytes ()  |  Ottenere un allegato come vettore di byte binario.
public std:: shared_ptr\<Stream\> GetStream () const  |  Ottenere un allegato come flusso binario.
public const std::string& GetName() const  |  Ottenere il nome dell'allegato sotto forma di stringa.
public const std:: String & getlongname () const  |  Ottenere il nome lungo dell'allegato sotto forma di stringa.
public const std::string& GetPath() const  |  Ottenere il nome del percorso dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
public const std:: String & GetLongPath () const  |  Ottiene il nome del percorso lungo dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
  
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