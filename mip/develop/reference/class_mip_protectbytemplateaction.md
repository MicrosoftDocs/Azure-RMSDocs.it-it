---
title: Classe mip::ProtectByTemplateAction
description: 'Classe MIP:: protectbytemplateaction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 18bdf3caa5eba2f335376d81f525fe93da4d0352
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173258"
---
# <a name="class-mipprotectbytemplateaction"></a>Classe mip::ProtectByTemplateAction 
Classe di azione che specifica l'aggiunta della protezione basata su modello al documento.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetTemplateId() const  |  Ottiene l'ID modello di protezione associato all'azione.
public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).

## <a name="members"></a>Membri
  
### <a name="gettemplateid-function"></a>GetTemplateId (funzione)
Ottiene l'ID modello di protezione associato all'azione.

  
**Restituisce**: ID del modello di protezione.


### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.