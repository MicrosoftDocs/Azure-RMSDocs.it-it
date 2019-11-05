---
title: Classe mip::MetadataAction
description: 'Documenta la classe MIP:: metadataaction di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 405bb153527cb3fde346203d3b11c09c97110f12
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558688"
---
# <a name="class-mipmetadataaction"></a>Classe mip::MetadataAction 
Azione che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<std:: String\>& GetMetadataToRemove () const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetMetadataToAdd () const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove (funzione)
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (funzione)
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: Const std::vector<std::pair<std::string, std::string>>& La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.