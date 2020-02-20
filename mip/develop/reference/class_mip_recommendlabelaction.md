---
title: Classe mip::RecommendLabelAction
description: 'Documenta la classe MIP:: recommendlabelaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 2038c8eb1a6baa52dc696be998853ca6774edccf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489538"
---
# <a name="class-miprecommendlabelaction"></a>Classe mip::RecommendLabelAction 
Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<label\>& GetLabel () const  |  Ottiene l'etichetta suggerita.
public const std:: Vector\<std:: String\>& GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'etichetta suggerita.

  
**Restituisce**: l'etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: const std:: Vector < std:: string > & un elenco di ID di classificazione che ha causato la visualizzazione di questa etichetta.