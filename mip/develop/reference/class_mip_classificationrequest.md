---
title: Classe ClassificationRequest
description: 'Documenta la classe classificationrequest:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5903c0bcccf7899449d7097c99e79feef038c988
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211941"
---
# <a name="class-classificationrequest"></a>Classe ClassificationRequest 
Classe che contiene la richiesta di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String GetClassificationId () const  |  Ottiene l'ID dei criteri di classificazione.
public std:: String GetRulePackageId () const  |  Ottenere l'ID del pacchetto di regole.
  
## <a name="members"></a>Membri
  
### <a name="getclassificationid-function"></a>GetClassificationId (funzione)
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getrulepackageid-function"></a>GetRulePackageId (funzione)
Ottenere l'ID del pacchetto di regole.

  
**Restituisce**: ID del pacchetto di regole. le classificazioni predefinite verranno impostate su un GUID vuoto.