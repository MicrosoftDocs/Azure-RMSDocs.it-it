---
title: Classe mip::ApplyLabelAction
description: 'Documenta la classe MIP:: applylabelaction di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 3e5ba734400000b1b1a324520e9595828c2f6ff9
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056303"
---
# <a name="class-mipapplylabelaction"></a>Classe mip::ApplyLabelAction 
Per applicare le azioni di etichetta, è necessario che l'applicazione chiamante applichi un'etichetta specifica.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::\<shared_ptr\>Label & GetLabel () const  |  Ottenere l'etichetta obbligatoria.
public const std::\<vector std::\>String & GetClassificationIds () const  |  Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottenere l'etichetta obbligatoria.

  
**Restituisce**: Etichetta.
  
### <a name="getclassificationids-function"></a>GetClassificationIds (funzione)
Ottiene gli ID di classificazione che corrispondono e ha causato la visualizzazione di questa etichetta.

  
**Restituisce**: Const std:: Vector < std:: String > & un elenco di ID di classificazione che hanno causato la visualizzazione di questa etichetta.