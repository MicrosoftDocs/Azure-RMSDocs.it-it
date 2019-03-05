---
title: Classe mip::ApplyLabelAction
description: Documenta la classe mip::applylabelaction di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ad1367480497ede6c8efd33d6ebc60c4c6ca34c5
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332228"
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
