---
title: Classe mip::PolicyProfile::Observer
description: Documenta la classe MIP::p olicyprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 1315f4c1289c63184b8fa029b3668b363b88b143
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054205"
---
# <a name="class-mippolicyprofileobserver"></a>Classe mip::PolicyProfile::Observer 
Interfaccia [Observer](class_mip_policyprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std::\<shared_ptr\>PolicyProfile & profile, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess (const std::\<vector std::\>String & engineIds, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
public virtual void OnUnloadEngineSuccess (const std::\<shared_ptr\>void & context)  |  Viene chiamato quando un motore è stato scaricato correttamente.
public virtual void OnUnloadEngineFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando lo scaricamento di un motore ha causato un errore.
public virtual void OnAddEngineSuccess (const std::\<shared_ptr\>PolicyEngine & Engine, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineStarting (bool requiresPolicyFetch)  |  Chiamato prima della creazione del motore per descrivere se i dati dei criteri del motore devono essere recuperati dal server o se possono essere creati dai dati memorizzati nella cache locale.
public virtual void OnAddEngineFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
public virtual void OnDeleteEngineSuccess (const std::\<shared_ptr\>void & context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando l'eliminazione di un motore ha causato un errore.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Viene chiamato quando i criteri vengono modificati per il motore con l'ID specificato o quando i tipi di riservatezza personalizzati caricati sono stati modificati.
  
## <a name="members"></a>Members
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: profilo corrente usato per avviare l'operazione. 


* **context**: contesto passato all'operazione LoadAsync.


  
### <a name="onloadfailure-function"></a>OnLoadFailure (funzione)
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di caricamento. 


* **context**: contesto passato all'operazione LoadAsync.


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (funzione)
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **context**: contesto passato all'operazione ListEnginesAsync.


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (funzione)
Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: contesto passato all'operazione ListEnginesAsync.


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess (funzione)
Viene chiamato quando un motore è stato scaricato correttamente.

Parametri:  
* **context**: contesto passato all'operazione UnloadEngineAsync.


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure (funzione)
Viene chiamato quando lo scaricamento di un motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di scaricamento motore. 


* **context**: contesto passato all'operazione UnloadEngineAsync.


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (funzione)
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.

Parametri:  
* **motore**: il motore appena aggiunto 


* **context**: contesto passato all'operazione AddEngineAsync


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting (funzione)
Chiamato prima della creazione del motore per descrivere se i dati dei criteri del motore devono essere recuperati dal server o se possono essere creati dai dati memorizzati nella cache locale.

Parametri:  
* **requiresPolicyFetch**: Descrive se i dati del motore devono essere recuperati tramite HTTP o se verranno caricati dalla cache


Questo callback facoltativo può essere utilizzato da un'applicazione per essere informati se un'operazione AddEngineAsync richiede un'operazione HTTP (con il ritardo associato) per il completamento.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (funzione)
Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: contesto passato all'operazione AddEngineAsync.


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (funzione)
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **context**: contesto passato all'operazione DeleteEngineAsync.


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (funzione)
Viene chiamato quando l'eliminazione di un motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: contesto passato all'operazione DeleteEngineAsync.


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged (funzione)
Viene chiamato quando i criteri vengono modificati per il motore con l'ID specificato o quando i tipi di riservatezza personalizzati caricati sono stati modificati.

Parametri:  
* **engineId**: motore 


Per caricare i nuovi criteri è necessario chiamare di nuovo AddEngineAsync con l'ID motore specificato.