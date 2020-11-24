---
title: Classe MsgAttachmentData
description: 'Documenta la classe msgattachmentdata:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c729b2907878aa383b058689c55072e53541a595
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566753"
---
# <a name="class-msgattachmentdata"></a>Classe MsgAttachmentData 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<uint8_t\>& GetBytes ()  |  Ottenere un allegato come vettore di byte binario.
public std:: shared_ptr \<Stream\> GetStream () const  |  Ottenere un allegato come flusso binario.
public const std::string& GetName() const  |  Ottenere il nome dell'allegato sotto forma di stringa.
public const std:: String& getlongname () const  |  Ottenere il nome lungo dell'allegato sotto forma di stringa.
public const std::string& GetPath() const  |  Ottenere il nome del percorso dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
public const std:: String& GetLongPath () const  |  Ottiene il nome del percorso lungo dell'allegato sotto forma di stringa. Se il percorso non è vuoto, fare riferimento all'allegato.
  
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