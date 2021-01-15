---
title: Classe ClassificationResult
description: 'Documenta la classe classificationresult:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: c1f4154bbc12613726aac8f56a322cb6cd4d5a53
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211873"
---
# <a name="class-classificationresult"></a>Classe ClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Ottiene l'ID dei criteri di classificazione.
public std::string GetName() const  |  Ottenere il nome dei criteri di classificazione.
public int GetCount() const  |  Ottiene il numero di istanze.
public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
public std:: String GetSensitiveInformationDetections () const  |  Ottenere i rilevamenti sensibili delle informazioni.
public virtual std:: Vector \<std::shared_ptr\<mip::DetailedClassificationResult\> \> GetDetailedClassificationAttributes () const  |  Ottenere le bande di rilevamento specifiche se è abilitata la classificazione con probabilità.
  
## <a name="members"></a>Membri
  
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