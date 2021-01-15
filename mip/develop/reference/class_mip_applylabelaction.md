---
title: Classe ApplyLabelAction
description: 'Documenta la classe applylabelaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: a88a913ea5dfd958e5ed073f0dff6f0bac1b527f
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212247"
---
# <a name="class-applylabelaction"></a>Classe ApplyLabelAction 
Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr \<Label\>& GetLabel () const  |  Ottenere l'etichetta obbligatoria.
public const std:: Vector \<std::string\>& GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Membri
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottenere l'etichetta obbligatoria.

  
**Restituisce**: l'etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: const std:: Vector<std:: String>& un elenco di ID di classificazione che ha causato la visualizzazione di questa etichetta.