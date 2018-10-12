---
title: Classe mip ApplyLabelAction
description: Riferimento per la classe mip ApplyLabelAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06a17ef1e60503cfb7d690bea9bb72316544f16d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445768"
---
# <a name="class-mipapplylabelaction"></a>Classe mip::ApplyLabelAction 
Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetLabelId() const  |  Ottiene l'ID dell'etichetta necessario.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getlabelid"></a>GetLabelId
Ottiene l'ID dell'etichetta necessario.

  
**Restituisce**: ID dell'etichetta.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.