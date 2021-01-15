---
title: Classe MetadataAction
description: 'Documenta la classe metadataaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 873901994f452f8a1b521653e9fc078ce1933883
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213675"
---
# <a name="class-metadataaction"></a>Classe MetadataAction 
Classe Action che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<std::string\>& GetMetadataToRemove () const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
public const std:: Vector \<MetadataEntry\>& GetMetadataToAdd () const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove (funzione)
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (funzione)
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: const std:: Vector <MetadataEntry>& la rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.