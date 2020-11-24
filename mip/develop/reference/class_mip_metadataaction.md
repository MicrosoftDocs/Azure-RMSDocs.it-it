---
title: Classe MetadataAction
description: 'Documenta la classe metadataaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 082a4332482bce35a436b70d4fa86ee7320d6f52
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566780"
---
# <a name="class-metadataaction"></a>Classe MetadataAction 
Classe Action che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<std::string\>& GetMetadataToRemove () const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
public const std:: Vector \<MetadataEntry\>& GetMetadataToAdd () const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
  
## <a name="members"></a>Members
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove (funzione)
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (funzione)
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: const std:: Vector <MetadataEntry>& la rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.