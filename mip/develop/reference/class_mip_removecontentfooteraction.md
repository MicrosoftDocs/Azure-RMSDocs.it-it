---
title: Classe mip RemoveContentFooterAction
description: Riferimento per la classe mip RemoveContentFooterAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: d275e2256c8a65bf63fd16d5761f42563d7a7f07
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445632"
---
# <a name="class-mipremovecontentfooteraction"></a>Classe mip::RemoveContentFooterAction 
Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementnames"></a>GetUIElementNames
Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.

  
**Restituisce**: un elenco di nomi di elementi dell'interfaccia utente.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.