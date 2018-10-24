---
title: Classe mip MetadataAction
description: Riferimento per la classe mip MetadataAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 8f7480775a0226c7161c9ad770184e54427a5084
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444620"
---
# <a name="class-mipmetadataaction"></a>Classe mip::MetadataAction 
Classe [Action](class_mip_action.md) che aggiunge informazioni sui metadati al contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Ottiene l'elenco dei nomi dei metadati da rimuovere dal contenuto.

  
**Restituisce**: vettore di stringhe da rimuovere. La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Ottiene le coppie nome/valore dei metadati da aggiungere al contenuto.

  
**Restituisce**: Const std::vector<std::pair<std::string, std::string>>& La rimozione dei metadati deve essere eseguita prima dell'aggiunta dei metadati.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.