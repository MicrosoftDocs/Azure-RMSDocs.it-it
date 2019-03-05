---
title: Classe mip::MetadataAction
description: 'Classe MIP:: metadataaction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c180072eec94b2f71471c10b4344d65321ef49c6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332413"
---
# <a name="class-mipmetadataaction"></a>Classe mip::MetadataAction 
Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: Vector const\<std:: String\>& GetMetadataToRemove() const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetMetadataToAdd() const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove (funzione)
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: Un vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (funzione)
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: Const std:: Vector < std:: Pair < std:: String, std:: String >> & rimozione dei metadati deve essere eseguite prima dell'aggiunta di metadati.
  
### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.
