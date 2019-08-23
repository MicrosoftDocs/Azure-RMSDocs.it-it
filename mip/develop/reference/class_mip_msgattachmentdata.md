---
title: 'Classe MIP:: MsgAttachmentData'
description: 'Documenta la classe MIP:: msgattachmentdata di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 963968008e1098209270d990e9c6b1ab273b0971
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893311"
---
# <a name="class-mipmsgattachmentdata"></a>Classe MIP:: MsgAttachmentData 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::\<vector\>uint8_t & GetBytes ()  |  Ottenere un allegato come vettore di byte binario.
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