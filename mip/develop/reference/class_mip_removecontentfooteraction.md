---
title: Classe mip::RemoveContentFooterAction
description: 'Classe MIP:: removecontentfooteraction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 006c8ad45da57b0223b35084456e8917411802f3
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330237"
---
# <a name="class-mipremovecontentfooteraction"></a>Classe mip::RemoveContentFooterAction 
Classe di azione che specifica la rimozione del piè di pagina contenuto dal documento.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: Vector const\<std:: String\>& GetUIElementNames()  |  Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementnames-function"></a>GetUIElementNames (funzione)
Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.

  
**Restituisce**: Elenco di nomi di elementi dell'interfaccia utente.
  
### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.
