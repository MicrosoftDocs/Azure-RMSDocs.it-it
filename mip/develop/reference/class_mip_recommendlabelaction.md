---
title: Classe mip::RecommendLabelAction
description: 'Documenta la classe MIP:: recommendlabelaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: dd3d2d0ecf7b549105e1a6373a998e77d4e77de8
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883204"
---
# <a name="class-miprecommendlabelaction"></a>Classe mip::RecommendLabelAction 
Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::\<shared_ptr\>Label & GetLabel () const  |  Ottiene l'etichetta suggerita.
public const std::\<vector std::\>String & GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'etichetta suggerita.

  
**Restituisce**: Etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: Const std:: Vector < std:: String > & un elenco di ID di classificazione che hanno causato la visualizzazione di questa etichetta.