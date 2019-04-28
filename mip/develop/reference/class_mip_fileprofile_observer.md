---
title: Classe mip::FileProfile::Observer
description: 'Classe MIP:: fileprofile di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7b9c3440d577e9ba2e08bdba6ed890d3a480c783
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60174103"
---
# <a name="class-mipfileprofileobserver"></a>Classe mip::FileProfile::Observer 
Interfaccia [Observer](class_mip_fileprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _Non ancora documentato._
OnLoadSuccess void virtuale pubblico (const std:: shared_ptr\<MIP:: fileprofile\>& profilo, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il profilo è stato caricato correttamente.
OnLoadFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
OnListEnginesSuccess void virtuale pubblico (const std:: Vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
OnListEnginesFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
OnUnloadEngineSuccess void virtuale pubblico (const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando un motore è stato scaricato correttamente.
OnUnloadEngineFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando lo scaricamento di un motore ha causato un errore.
OnAddEngineSuccess void virtuale pubblico (const std:: shared_ptr\<MIP:: fileengine\>& motore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
OnAddEngineFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
OnDeleteEngineSuccess void virtuale pubblico (const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando un motore è stato eliminato correttamente.
OnDeleteEngineFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando l'eliminazione di un motore ha causato un errore.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Viene chiamato quando i criteri del motore con l'ID specificato sono cambiati.
OnAddPolicyEngineStarting void virtuale pubblico (bool requiresPolicyFetch)  |  Chiamato prima della creazione motore per descrivere o meno i dati dei criteri del motore dei criteri devono essere recuperati dal server o se può essere creato dai dati memorizzati nella cache locale.
protected Observer()  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="observer-function"></a>~ Funzione observer
_Non ancora documentato._

  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.
  
### <a name="onloadfailure-function"></a>Funzione OnLoadFailure
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
Chiamato prima della creazione motore per descrivere o meno i dati dei criteri del motore dei criteri devono essere recuperati dal server o se può essere creato dai dati memorizzati nella cache locale.

Parametri:  
* **requiresPolicyFetch**: Descrive se i dati del motore devono essere recuperati tramite HTTP o se venga caricato dalla cache


Questo callback facoltativo potrebbe utilizzabile da un'applicazione per essere informati o meno un'operazione AddEngineAsync richiederanno un'operazione HTTP (con il ritardo associato) per completare.
  
### <a name="observer-function"></a>Funzione Observer
_Non ancora documentato._
