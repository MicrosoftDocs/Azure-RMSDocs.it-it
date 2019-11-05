---
title: Classe mip::RecommendLabelAction
description: 'Documenta la classe MIP:: recommendlabelaction di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 629e6410657fcb799e3f71c0ccb3752b82437428
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560020"
---
# <a name="class-miprecommendlabelaction"></a>Classe mip::RecommendLabelAction 
Consigliare le azioni dell'etichetta serve a suggerire un'etichetta agli utenti. L'eliminazione di questa chiamata dopo che un utente ignora l'etichetta consigliata deve essere eseguita tramite le azioni supportate sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<label\>& GetLabel () const  |  Ottiene l'etichetta suggerita.
public const std:: Vector\<std:: String\>& GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Membri
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'etichetta suggerita.

  
**Restituisce**: l'etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: const std:: Vector < std:: string > & un elenco di ID di classificazione che ha causato la visualizzazione di questa etichetta.