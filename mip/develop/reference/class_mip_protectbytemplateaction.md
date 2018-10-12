---
title: Classe mip ProtectByTemplateAction
description: Riferimento per la classe mip ProtectByTemplateAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: cb5f42b25e6f499bc09f3f460ec4a253627b45a5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445462"
---
# <a name="class-mipprotectbytemplateaction"></a>Classe mip::ProtectByTemplateAction 
Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetTemplateId() const  |  Ottiene l'ID modello di protezione associato all'azione.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="gettemplateid"></a>GetTemplateId
Ottiene l'ID modello di protezione associato all'azione.

  
**Restituisce**: l'ID del modello di protezione.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.