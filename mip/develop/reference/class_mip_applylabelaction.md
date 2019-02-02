---
title: Classe mip::ApplyLabelAction
description: Documenta la classe mip::applylabelaction di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ce813a544504ce18b382cdb86bd31d89b6626fad
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650494"
---
# <a name="class-mipapplylabelaction"></a>Classe mip::ApplyLabelAction 
Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  Ottiene l'ID dell'etichetta necessario.
Public std:: Vector const\<std:: String\>& GetClassificationIds() const  |  Ottenere gli ID di classificazione che associati e ha causato questa etichetta da visualizzare.
public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getlabelid-function"></a>GetLabelId (funzione)
Ottiene l'ID dell'etichetta necessario.

  
**Restituisce**: L'ID etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottenere gli ID di classificazione che associati e ha causato questa etichetta da visualizzare.

  
**Restituisce**: Const std:: Vector < std:: String > e un elenco di classificazione degli ID che ha causato questa etichetta da visualizzare.
  
### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.