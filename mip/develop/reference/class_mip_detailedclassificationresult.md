---
title: Classe DetailedClassificationResult
description: 'Documenta la classe detailedclassificationresult:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 9b1921c046867207d6b1d9a67df46f442fb95977
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211636"
---
# <a name="class-detailedclassificationresult"></a>Classe DetailedClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
public int GetCount() const  |  Ottiene il numero di istanze.
  
## <a name="members"></a>Membri
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel (funzione)
Ottiene l'attendibilità del risultato.

  
**Restituisce**: attendibilità numerica nel conteggio da 0-100.
  
### <a name="getcount-function"></a>Funzione GetCount
Ottiene il numero di istanze.

  
**Restituisce**: numero di istanze.