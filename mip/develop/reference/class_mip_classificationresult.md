---
title: Classe mip::ClassificationResult
description: 'Documenta la classe MIP:: classificationresult di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a245cd4d9505de8adbf3cc1a2de6d2fa20369ce7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490405"
---
# <a name="class-mipclassificationresult"></a>Classe mip::ClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Ottiene l'ID dei criteri di classificazione.
public std::string GetName() const  |  Ottenere il nome dei criteri di classificazione.
public int GetCount() const  |  Ottiene il numero di istanze.
public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
public std:: String GetSensitiveInformationDetections () const  |  Ottenere i rilevamenti sensibili delle informazioni.
  
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