---
title: Classe RemoveWatermarkAction
description: 'Documenta la classe removewatermarkaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: eee2617a7f3c1225d789a5d1f6124caa3d3deec0
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567429"
---
# <a name="class-removewatermarkaction"></a>Classe RemoveWatermarkAction 
Classe di azione che specifica la rimozione della filigrana dal documento.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<std::string\>& GetUIElementNames ()  |  Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
public ActionType GetType() const  |  Specifica il tipo di Action.
  
## <a name="members"></a>Members
  
### <a name="getuielementnames-function"></a>GetUIElementNames (funzione)
Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.

  
**Restituisce**: un elenco di nomi di elementi dell'interfaccia utente.
  
### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di Action.

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.