---
title: Classe ClassificationResult
description: 'Documenta la classe classificationresult:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4e64abc1cca11f11b19238282c9061dc26b29290
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567230"
---
# <a name="class-classificationresult"></a>Classe ClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Ottiene l'ID dei criteri di classificazione.
public std::string GetName() const  |  Ottenere il nome dei criteri di classificazione.
public int GetCount() const  |  Ottiene il numero di istanze.
public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
public std:: String GetSensitiveInformationDetections () const  |  Ottenere i rilevamenti sensibili delle informazioni.
public virtual std:: Vector \<std::shared_ptr\<mip::DetailedClassificationResult\> \> GetDetailedClassificationAttributes () const  |  Ottenere le bande di rilevamento specifiche se è abilitata la classificazione con probabilità.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getname-function"></a>GetName (funzione)
Ottenere il nome dei criteri di classificazione.

  
**Restituisce**: nome dei criteri di classificazione.
  
### <a name="getcount-function"></a>Funzione GetCount
Ottiene il numero di istanze.

  
**Restituisce**: numero di istanze.
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel (funzione)
Ottiene l'attendibilità del risultato.
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections (funzione)
Ottenere i rilevamenti sensibili delle informazioni.

  
**Restituisce**: stringa JSON di tutti i rilevamenti di informazioni sensibili. Se non è vuoto, deve essere un formato JSON valido.
  
### <a name="getdetailedclassificationattributes-function"></a>GetDetailedClassificationAttributes (funzione)
Ottenere le bande di rilevamento specifiche se è abilitata la classificazione con probabilità.

  
**Restituisce**: un vettore di conteggi di istanze con soglie di confidenza diverse