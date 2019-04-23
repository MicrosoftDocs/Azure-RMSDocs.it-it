---
title: Classe mip::RemoveContentFooterAction
description: 'Classe MIP:: removecontentfooteraction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 14afd4688c13f419ab3019e9c268ba7d355121c8
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184315"
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