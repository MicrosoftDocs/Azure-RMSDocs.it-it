---
title: Classe mip::MetadataAction
description: 'Documenta la classe MIP:: metadataaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 85d2742d5602dc2e36d9370a33fd04050fbeee9d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487719"
---
# <a name="class-mipmetadataaction"></a>Classe mip::MetadataAction 
Azione che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<std:: String\>& GetMetadataToRemove () const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetMetadataToAdd () const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
  
## <a name="members"></a>Members
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove (funzione)
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (funzione)
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: Const std::vector<std::pair<std::string, std::string>>& La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.