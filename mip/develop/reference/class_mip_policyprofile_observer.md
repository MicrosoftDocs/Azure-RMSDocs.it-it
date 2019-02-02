---
title: Classe mip::PolicyProfile::Observer
description: Documenta la classe mip::policyprofile di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 451cc2b9da086644e561d0a1dd1912de5f38c48c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651174"
---
# <a name="class-mippolicyprofileobserver"></a>Classe mip::PolicyProfile::Observer 
Interfaccia [Observer](class_mip_policyprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
OnLoadSuccess void virtuale pubblico (const std:: shared_ptr\<PolicyProfile\>& profilo, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il profilo è stato caricato correttamente.
OnLoadFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
OnListEnginesSuccess void virtuale pubblico (const std:: Vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
OnListEnginesFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
OnUnloadEngineSuccess void virtuale pubblico (const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando un motore è stato scaricato correttamente.
OnUnloadEngineFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando lo scaricamento di un motore ha causato un errore.
OnAddEngineSuccess void virtuale pubblico (const std:: shared_ptr\<PolicyEngine\>& motore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
OnAddEngineStarting void virtuale pubblico (bool requiresPolicyFetch)  |  Chiamato prima della creazione motore per descrivere o meno i dati dei criteri del motore devono essere recuperati dal server o se può essere creato dai dati memorizzati nella cache locale.
OnAddEngineFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
OnDeleteEngineSuccess void virtuale pubblico (const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando un motore è stato eliminato correttamente.
OnDeleteEngineFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando l'eliminazione di un motore ha causato un errore.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Chiamato quando i criteri vengono modificati per il motore con l'ID specificato o quando sono stati modificati i tipi di sensibilità personalizzato caricato.
  
## <a name="members"></a>Membri
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: profilo corrente usato per avviare l'operazione. 


* **contesto**: il contesto passato all'operazione LoadAsync.


  
### <a name="onloadfailure-function"></a>Funzione OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di caricamento. 


* **contesto**: il contesto passato all'operazione LoadAsync.


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (funzione)
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **contesto**: il contesto passato all'operazione ListEnginesAsync.


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (funzione)
Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **contesto**: il contesto passato all'operazione ListEnginesAsync.


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess (funzione)
Viene chiamato quando un motore è stato scaricato correttamente.

Parametri:  
* **contesto**: il contesto passato all'operazione UnloadEngineAsync.


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure (funzione)
Viene chiamato quando lo scaricamento di un motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di scaricamento motore. 


* **contesto**: il contesto passato all'operazione UnloadEngineAsync.


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (funzione)
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.

Parametri:  
* **motore**: il modulo appena aggiunto 


* **contesto**: il contesto passato all'operazione AddEngineAsync


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting (funzione)
Chiamato prima della creazione motore per descrivere o meno i dati dei criteri del motore devono essere recuperati dal server o se può essere creato dai dati memorizzati nella cache locale.

Parametri:  
* **requiresPolicyFetch**: Descrive se i dati del motore devono essere recuperati tramite HTTP o se venga caricato dalla cache


Questo callback facoltativo potrebbe utilizzabile da un'applicazione per essere informati o meno un'operazione AddEngineAsync richiederanno un'operazione HTTP (con il ritardo associato) per completare.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (funzione)
Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **contesto**: il contesto passato all'operazione AddEngineAsync.


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (funzione)
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **contesto**: il contesto passato all'operazione DeleteEngineAsync.


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (funzione)
Viene chiamato quando l'eliminazione di un motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **contesto**: il contesto passato all'operazione DeleteEngineAsync.


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged (funzione)
Chiamato quando i criteri vengono modificati per il motore con l'ID specificato o quando sono stati modificati i tipi di sensibilità personalizzato caricato.

Parametri:  
* **engineId**: motore 


Per caricare i nuovi criteri è necessario chiamare di nuovo AddEngineAsync con l'ID motore specificato.