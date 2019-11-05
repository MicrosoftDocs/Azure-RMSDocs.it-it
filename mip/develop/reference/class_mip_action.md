---
title: Classe mip::Action
description: "Documenta la classe MIP:: Action dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d3cc1aecfb5ca8bf2d78dd9d6c8c280b5541389d
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560422"
---
# <a name="class-mipaction"></a>Classe mip::Action 
Interfaccia per un'azione. Ogni azione viene convertita in un passaggio che deve essere eseguito dall'applicazione per applicare l'etichetta (definita nei criteri)
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  Ottiene il tipo di azione.
  
## <a name="members"></a>Membri
  
### <a name="gettype-function"></a>Funzione GetType
Ottiene il tipo di azione.

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.