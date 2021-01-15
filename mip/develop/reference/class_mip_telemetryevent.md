---
title: Classe TelemetryEvent
description: 'Documenta la classe telemetryevent:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8776eff24a889a1132fc71d11c38b02c49822263
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225032"
---
# <a name="class-telemetryevent"></a>Classe TelemetryEvent 
Singolo evento di telemetria.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Ottenere il nome dell'evento.
public EventLevel GetLevel () const  |  Ottenere il livello di evento, che indica se i dati di servizio necessari (NSD) sono considerati o meno.
public const std:: Chrono:: steady_clock:: time_point& GetStartTime () const  |  Ottiene l'ora di inizio dell'evento.
public void AddProperty (const std:: shared_ptr \<EventProperty\>& prop)  |  Aggiungere una proprietà all'evento.
public void AddProperty (const std:: String& Name, valore bool)  |  Aggiungere una proprietà bool all'evento.
public void AddProperty (const std:: String& Name, Double value, pii PII)  |  Aggiungere una proprietà Double all'evento.
public void AddProperty (const std:: String& Name, int64_t value, pii PII)  |  Aggiungere una proprietà Int64 all'evento.
public void AddProperty (const std:: String& Name, const std:: String& value, pii PII)  |  Aggiungere una proprietà di stringa all'evento.
public void AddAuditOnlyProperty (const std:: String& Name, const std:: String& value)  |  Aggiungere una proprietà di stringa di solo controllo all'evento.
public std:: Vector \<std::shared_ptr\<EventProperty\> \> GetProperties () const  |  Ottiene tutte le proprietà dell'evento.
public std:: shared_ptr \<EventProperty\> GetProperty (const std:: string& Name)  |  Ottiene la proprietà con il nome specificato, se disponibile.
  
## <a name="members"></a>Membri
  
### <a name="getname-function"></a>GetName (funzione)
Ottenere il nome dell'evento.

  
**Restituisce**: nome evento
  
### <a name="getlevel-function"></a>GetLevel (funzione)
Ottenere il livello di evento, che indica se i dati di servizio necessari (NSD) sono considerati o meno.

  
**Restituisce**: livello dell'evento
  
### <a name="getstarttime-function"></a>GetStartTime (funzione)
Ottiene l'ora di inizio dell'evento.

  
**Restituisce**: ora di inizio dell'evento
  
### <a name="addproperty-function"></a>AddProperty (funzione)
Aggiungere una proprietà all'evento.

Parametri  
* **prop**: proprietà da aggiungere


  
### <a name="addproperty-function"></a>AddProperty (funzione)
Aggiungere una proprietà bool all'evento.

Parametri  
* **nome**: nome proprietà 


* **valore**: valore della proprietà


  
### <a name="addproperty-function"></a>AddProperty (funzione)
Aggiungere una proprietà Double all'evento.

Parametri  
* **nome**: nome proprietà 


* **valore**: valore della proprietà 


* informazioni **personali**: classificazione pii


  
### <a name="addproperty-function"></a>AddProperty (funzione)
Aggiungere una proprietà Int64 all'evento.

Parametri  
* **nome**: nome proprietà 


* **valore**: valore della proprietà 


* informazioni **personali**: classificazione pii


  
### <a name="addproperty-function"></a>AddProperty (funzione)
Aggiungere una proprietà di stringa all'evento.

Parametri  
* **nome**: nome proprietà 


* **valore**: valore della proprietà 


* informazioni **personali**: classificazione pii


  
### <a name="addauditonlyproperty-function"></a>AddAuditOnlyProperty (funzione)
Aggiungere una proprietà di stringa di solo controllo all'evento.

Parametri  
* **nome**: nome proprietà 


* **valore**: valore della proprietà


Una proprietà di solo controllo contiene informazioni riservate e non deve essere scritta nei log di file o in qualsiasi pipeline, ad eccezione di audit, fino a quando non viene ripulita manualmente.
  
### <a name="getproperties-function"></a>GetProperties (funzione)
Ottiene tutte le proprietà dell'evento.

  
**Restituisce**: Proprietà evento
  
### <a name="getproperty-function"></a>GetProperty (funzione)
Ottiene la proprietà con il nome specificato, se disponibile.

Parametri  
* **nome**: nome della proprietà da ottenere



  
**Restituisce**: proprietà con il nome specificato oppure nullptr se None