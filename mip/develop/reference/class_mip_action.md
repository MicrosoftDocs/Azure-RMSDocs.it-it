---
title: Classe mip Action
description: Riferimento per la classe mip Action
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 97b082a0a3da1e8b6726d181f42e741f002a7e29
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445972"
---
# <a name="class-mipaction"></a>Classe mip::Action 
Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.