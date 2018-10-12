---
title: Classe mip ClassificationResult
description: Riferimento per la classe mip ClassificationResult
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ea312330c656b6daefbc1bcba690f53ebfbf419f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446295"
---
# <a name="class-mipclassificationresult"></a>Classe mip::ClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public std::string GetId() const  |  Ottiene l'ID dei criteri di classificazione.
 public int GetCount() const  |  Ottiene il numero di istanze.
 public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
  
## <a name="members"></a>Membri
  
### <a name="getid"></a>GetId
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getcount"></a>GetCount
Ottiene il numero di istanze.

  
**Restituisce**: numero di istanze.
  
### <a name="getconfidencelevel"></a>GetConfidenceLevel
Ottiene l'attendibilità del risultato.