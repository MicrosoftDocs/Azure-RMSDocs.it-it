---
title: Classe mip::ClassificationResult
description: Documenta la classe mip::classificationresult di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6a048dd7902e8148e4f32f8cc9e62d63110b2b4a
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573565"
---
# <a name="class-mipclassificationresult"></a>Classe mip::ClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Ottiene l'ID dei criteri di classificazione.
public int GetCount() const  |  Ottiene il numero di istanze.
public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
Public std:: String GetSensitiveInformationDetections() const  |  Ottenere i rilevamenti di informazioni riservate.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getcount-function"></a>GetCount (funzione)
Ottiene il numero di istanze.

  
**Restituisce**: Il numero di istanze.
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel (funzione)
Ottiene l'attendibilità del risultato.
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections (funzione)
Ottenere i rilevamenti di informazioni riservate.

  
**Restituisce**: Stringa JSON di tutti i rilevamenti di informazioni riservate.