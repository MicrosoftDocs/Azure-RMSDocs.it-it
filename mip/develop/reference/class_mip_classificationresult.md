---
title: Classe mip::ClassificationResult
description: 'Documenta la classe MIP:: classificationresult di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2744e2d5fe188667ff7c1c93a7f98719f200aecd
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056220"
---
# <a name="class-mipclassificationresult"></a>Classe mip::ClassificationResult 
Classe contenente il risultato di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Ottiene l'ID dei criteri di classificazione.
public int GetCount() const  |  Ottiene il numero di istanze.
public int GetConfidenceLevel() const  |  Ottiene l'attendibilità del risultato.
public std:: String GetSensitiveInformationDetections () const  |  Ottenere i rilevamenti sensibili delle informazioni.
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getcount-function"></a>Funzione GetCount
Ottiene il numero di istanze.

  
**Restituisce**: Numero di istanze.
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel (funzione)
Ottiene l'attendibilità del risultato.
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections (funzione)
Ottenere i rilevamenti sensibili delle informazioni.

  
**Restituisce**: Stringa JSON di tutti i rilevamenti sensibili delle informazioni.