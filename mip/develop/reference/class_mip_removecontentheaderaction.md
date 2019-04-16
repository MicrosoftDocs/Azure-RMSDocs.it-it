---
title: Classe mip::RemoveContentHeaderAction
description: 'Classe MIP:: removecontentheaderaction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3cc2fbdcfeae4e168e342a3c7af0edc971039db4
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574313"
---
# <a name="class-mipremovecontentheaderaction"></a>Classe mip::RemoveContentHeaderAction 
Classe di azione che specifica la rimozione dell'intestazione contenuto dal documento.
  
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