---
title: Classe mip::ApplyLabelAction
description: 'Documenta la classe MIP:: applylabelaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e1551adddec611c6f9a0982c5a267fad39c436c4
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490677"
---
# <a name="class-mipapplylabelaction"></a>Classe mip::ApplyLabelAction 
Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<label\>& GetLabel () const  |  Ottenere l'etichetta obbligatoria.
public const std:: Vector\<std:: String\>& GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottenere l'etichetta obbligatoria.

  
**Restituisce**: l'etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: const std:: Vector < std:: string > & un elenco di ID di classificazione che ha causato la visualizzazione di questa etichetta.