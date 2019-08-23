---
title: Classe mip::ApplyLabelAction
description: 'Documenta la classe MIP:: applylabelaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7d2067ad030e909d53602fcdb3eefa9b88af56bf
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884519"
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