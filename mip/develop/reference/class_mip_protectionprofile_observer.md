---
title: Classe mip ProtectionProfile Observer
description: Riferimento per la classe mip ProtectionProfile Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3678e6c1e1659f28b2f1dcc36f61295a8d29393e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446431"
---
# <a name="class-mipprotectionprofileobserver"></a>Classe mip::ProtectionProfile::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'eliminazione di un motore ha restituito un errore.
  
## <a name="members"></a>Membri
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: riferimento all'oggetto [ProtectionProfile](class_mip_protectionprofile.md) appena creato


* **context**: lo stesso contesto passato a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il caricamento 


* **context**: lo stesso contesto passato a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **context**: lo stesso contesto passato a [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync)


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: lo stesso contesto passato a [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync)


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.

Parametri:  
* **motore**: motore appena creato 


* **context**: lo stesso contesto passato a [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync)


  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: lo stesso contesto passato a [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync)


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **context**: lo stesso contesto passato a [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync)


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
Viene chiamato quando l'eliminazione di un motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: lo stesso contesto passato a [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync)

