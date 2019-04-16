---
title: Classe mip::RecommendLabelAction
description: Documenta la classe mip::recommendlabelaction di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: eeab9022b257ff327e2c83b1d8860662355180e5
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573164"
---
# <a name="class-miprecommendlabelaction"></a>Classe mip::RecommendLabelAction 
Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  Ottiene l'ID dell'etichetta suggerito.
Public std:: Vector const\<std:: String\>& GetClassificationIds() const  |  Ottenere gli ID di classificazione che associati e ha causato questa etichetta da visualizzare.
public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).

## <a name="members"></a>Membri
  
### <a name="getlabelid-function"></a>GetLabelId (funzione)
Ottiene l'ID dell'etichetta suggerito.

  
**Restituisce**: L'ID etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottenere gli ID di classificazione che associati e ha causato questa etichetta da visualizzare.

  
**Restituisce**: Const std:: Vector < std:: String > e un elenco di classificazione degli ID che ha causato questa etichetta da visualizzare.

### <a name="gettype-function"></a>Funzione GetType    
Specifica il tipo di [Action](class_mip_action.md).  

**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.