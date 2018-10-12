---
title: Classe mip PolicyProfile Observer
description: Riferimento per la classe mip PolicyProfile Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5de2156f4906c14e4ebc1418df8acb092c089d7d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446871"
---
# <a name="class-mippolicyprofileobserver"></a>Classe mip::PolicyProfile::Observer 
Interfaccia [Observer](class_mip_policyprofile_observer.md) per il recupero delle notifiche degli eventi correlati al profilo da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<PolicyProfile>& profile, const std::shared_ptr<void>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  Viene chiamato quando un motore è stato scaricato correttamente.
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando lo scaricamento di un motore ha causato un errore.
public virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'eliminazione di un motore ha causato un errore.
 public virtual void OnPolicyChanged(const std::string& engineId)  |  Viene chiamato quando i criteri del motore con l'ID specificato sono cambiati.
  
## <a name="members"></a>Membri
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: profilo corrente usato per avviare l'operazione. 


* **context**: contesto passato all'operazione.


  
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di caricamento. 


* **context**: contesto passato all'operazione.


  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **context**: contesto passato all'operazione.


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
Viene chiamato quando il recupero dell'elenco dei motori ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: contesto passato all'operazione.


  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Viene chiamato quando un motore è stato scaricato correttamente.

Parametri:  
* **context**: contesto passato all'operazione.


  
### <a name="onunloadenginefailure"></a>OnUnloadEngineFailure
Viene chiamato quando lo scaricamento di un motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di scaricamento motore. 


* **context**: contesto passato all'operazione.


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
Viene chiamato quando l'aggiunta di un nuovo motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: contesto passato all'operazione.


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **context**: contesto passato all'operazione.


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
Viene chiamato quando l'eliminazione di un motore ha causato un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: contesto passato all'operazione.


  
### <a name="onpolicychanged"></a>OnPolicyChanged
Viene chiamato quando i criteri del motore con l'ID specificato sono cambiati.

Parametri:  
* **engineId**: motore 


Per caricare i nuovi criteri è necessario chiamare di nuovo AddEngineAsync con l'ID motore specificato.