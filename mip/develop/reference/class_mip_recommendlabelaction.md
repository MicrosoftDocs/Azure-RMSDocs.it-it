---
title: Classe RecommendLabelAction
description: 'Documenta la classe recommendlabelaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d86f9a77a7e198ed47b633bd74da49db41edda15
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213267"
---
# <a name="class-recommendlabelaction"></a>Classe RecommendLabelAction 
Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr \<Label\>& GetLabel () const  |  Ottiene l'etichetta suggerita.
public const std:: Vector \<std::string\>& GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Membri
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'etichetta suggerita.

  
**Restituisce**: l'etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: const std:: Vector<std:: String>& un elenco di ID di classificazione che ha causato la visualizzazione di questa etichetta.