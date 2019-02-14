---
title: Classe mip::ProtectByTemplateAction
description: 'Classe MIP:: protectbytemplateaction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9c7114bcceceef537675ca04499cdb1710456b82
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252368"
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
