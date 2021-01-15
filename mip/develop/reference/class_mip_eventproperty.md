---
title: Classe EventProperty
description: 'Documenta la classe EventProperty:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5ee28e454aa5d7854c572df8ef6e4642482c1104
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225062"
---
# <a name="class-eventproperty"></a>Classe EventProperty 
Una singola proprietà di controllo/telemetria.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public EventPropertyType GetPropertyType () const  |  Ottiene il tipo di dati sottostante per questa proprietà.
public const std::string& GetName() const  |  Ottenere il nome della proprietà.
public pii GetPii () const  |  Ottenere la classificazione delle informazioni personali (PII), se disponibile.
public bool IsAuditOnly () const  |  Ottiene un valore che indica se questa proprietà è limitata alla pipeline di controllo.
public double GetDouble () const  |  Ottieni valore proprietà (Double)
public int64_t GetInt64 () const  |  Ottieni valore proprietà (Int64)
public const std:: String& GetString () const  |  Ottieni valore proprietà (stringa)
  
## <a name="members"></a>Membri
  
### <a name="getpropertytype-function"></a>GetPropertyType (funzione)
Ottiene il tipo di dati sottostante per questa proprietà.

  
**Restituisce**: tipo di dati sottostante
  
### <a name="getname-function"></a>GetName (funzione)
Ottenere il nome della proprietà.

  
**Restituisce**: nome della proprietà
  
### <a name="getpii-function"></a>GetPii (funzione)
Ottenere la classificazione delle informazioni personali (PII), se disponibile.

  
**Restituisce**: classificazione pii
  
### <a name="isauditonly-function"></a>IsAuditOnly (funzione)
Ottiene un valore che indica se questa proprietà è limitata alla pipeline di controllo.

  
**Restituisce**: indipendentemente dal fatto che questa proprietà sia limitata o meno alla pipeline di controllo se è true, la proprietà contiene informazioni riservate e non deve essere scritta nei log di file o in qualsiasi pipeline, ad eccezione di audit, fino a quando non viene ripulita manualmente.
  
### <a name="getdouble-function"></a>GetDouble (funzione)
Ottieni valore proprietà (Double)

  
**Restituisce**: valore della proprietà
  
### <a name="getint64-function"></a>Funzione GetInt64
Ottieni valore proprietà (Int64)

  
**Restituisce**: valore della proprietà
  
### <a name="getstring-function"></a>GetString (funzione)
Ottieni valore proprietà (stringa)

  
**Restituisce**: valore della proprietà