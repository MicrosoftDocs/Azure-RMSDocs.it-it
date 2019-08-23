---
title: Classe mip::MetadataAction
description: 'Documenta la classe MIP:: metadataaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 26a189d714001f4145ce328c163a052313923136
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885426"
---
# <a name="class-mipmetadataaction"></a>Classe mip::MetadataAction 
Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::\<vector std::\>String & GetMetadataToRemove () const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
public const std::\<vector std::p\<Air std:: String, std::\>String\>& GetMetadataToAdd () const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
  
## <a name="members"></a>Members
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove (funzione)
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: Vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (funzione)
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: Const std:: Vector < std::p Air < std:: String, std:: String > > & la rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.