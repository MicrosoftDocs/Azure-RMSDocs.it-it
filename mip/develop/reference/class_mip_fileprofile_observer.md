---
title: 'Classe fileprofile:: Observer'
description: 'Documenta la classe fileprofile:: Observer di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 62e578f8f3527a4749fedfc88a2b32de5c6e95db
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566936"
---
# <a name="class-fileprofileobserver"></a>Classe fileprofile:: Observer 
Interfaccia Observer per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Tutti gli errori ereditano da mip::Error. I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _Non ancora documentato._
public virtual void OnLoadSuccess(const std::shared_ptr\<mip::FileProfile\>& profile, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess (const std:: Vector \<std::string\>& engineIds, const std:: shared_ptr \<void\>& context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
public virtual void OnUnloadEngineSuccess(const std::shared_ptr\<void\>& context)  |  Viene chiamato quando un motore è stato scaricato correttamente.
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando lo scaricamento di un motore ha causato un errore.
public virtual void OnAddEngineSuccess(const std::shared_ptr\<mip::FileEngine\>& engine, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando l'eliminazione di un motore ha causato un errore.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Viene chiamato quando i criteri del motore con l'ID specificato sono cambiati.
public virtual void OnAddPolicyEngineStarting (bool requiresPolicyFetch)  |  Chiamato prima della creazione del motore per descrivere se i dati dei criteri del motore dei criteri devono essere recuperati dal server o se possono essere creati da dati memorizzati localmente nella cache.
protected Observer()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="observer-function"></a>~ Observer (funzione)
Non ancora documentato.

  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.
  
### <a name="onloadfailure-function"></a>OnLoadFailure (funzione)
Viene chiamato quando il caricamento di un profilo ha causato un errore.
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (funzione)
Viene chiamato quando l'elenco dei motori è stato generato correttamente.
  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (funzione)
Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess (funzione)
Viene chiamato quando un motore è stato scaricato correttamente.
  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure (funzione)
Viene chiamato quando lo scaricamento di un motore ha causato un errore.
  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (funzione)
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (funzione)
Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (funzione)
Viene chiamato quando un motore è stato eliminato correttamente.
  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (funzione)
Viene chiamato quando l'eliminazione di un motore ha causato un errore.
  
### <a name="onpolicychanged-function"></a>OnPolicyChanged (funzione)
Viene chiamato quando i criteri del motore con l'ID specificato sono cambiati.
  
### <a name="onaddpolicyenginestarting-function"></a>OnAddPolicyEngineStarting (funzione)
Chiamato prima della creazione del motore per descrivere se i dati dei criteri del motore dei criteri devono essere recuperati dal server o se possono essere creati da dati memorizzati localmente nella cache.

Parametri  
* **requiresPolicyFetch**: descrive se i dati del motore devono essere recuperati tramite http o se verranno caricati dalla cache


Questo callback facoltativo può essere utilizzato da un'applicazione per essere informati se un'operazione AddEngineAsync richiede un'operazione HTTP (con il ritardo associato) per il completamento.
  
### <a name="observer-function"></a>Funzione Observer
Non ancora documentato.
