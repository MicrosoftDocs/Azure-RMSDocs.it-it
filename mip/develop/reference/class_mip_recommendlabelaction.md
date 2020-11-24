---
title: Classe RecommendLabelAction
description: 'Documenta la classe recommendlabelaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2a0318c0da7bfc3a2be72c1139754da1f7142d71
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566570"
---
# <a name="class-recommendlabelaction"></a>Classe RecommendLabelAction 
Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr \<Label\>& GetLabel () const  |  Ottiene l'etichetta suggerita.
public const std:: Vector \<std::string\>& GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'etichetta suggerita.

  
**Restituisce**: l'etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: const std:: Vector<std:: String>& un elenco di ID di classificazione che ha causato la visualizzazione di questa etichetta.