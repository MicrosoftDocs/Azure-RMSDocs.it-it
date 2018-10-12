---
title: Classe mip CustomAction
description: Riferimento per la classe mip CustomAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a94a41c0e7f7848201e2af44187cce2540579b27
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444724"
---
# <a name="class-mipcustomaction"></a>Classe mip::CustomAction 
[CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetName() const  |  Ottiene il nome dell'azione.
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  Ottiene l'elenco di coppie valore-chiave delle proprietà.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getname"></a>GetName
Ottiene il nome dell'azione.

  
**Restituisce**: il nome dell'azione, se esistente. In caso contrario restituisce una stringa vuota.
  
### <a name="getproperties"></a>GetProperties
Ottiene l'elenco di coppie valore-chiave delle proprietà.

  
**Restituisce**: elenco di coppie chiave-valore.
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.