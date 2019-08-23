---
title: Classe mip::ProtectionProfile::Observer
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: bf3a43f28c4a445a5e2040108152832d2bffcfcd
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885096"
---
# <a name="class-mipprotectionprofileobserver"></a>Classe mip::ProtectionProfile::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionProfile](class_mip_protectionprofile.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std::\<shared_ptr\>ProtectionProfile & profile, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess (const std::\<vector std::\>String & engineIds, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.
public virtual void OnAddEngineSuccess (const std::\<shared_ptr\>ProtectionEngine & Engine, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.
public virtual void OnDeleteEngineSuccess (const std::\<shared_ptr\>void & context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando l'eliminazione di un motore ha restituito un errore.
  
## <a name="members"></a>Members
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profilo**: Riferimento al [ProtectionProfile](class_mip_protectionprofile.md) appena creato


* **context**: Lo stesso contesto passato a [ProtectionProfile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onloadfailure-function"></a>OnLoadFailure (funzione)
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **errore**: [Errore](class_mip_error.md) che si è verificato durante il caricamento 


* **context**: Lo stesso contesto passato a [ProtectionProfile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (funzione)
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **context**: Lo stesso contesto passato a [ProtectionProfile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (funzione)
Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: Lo stesso contesto passato a [ProtectionProfile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (funzione)
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.

Parametri:  
* **motore**di: Motore appena creato 


* **context**: Lo stesso contesto passato a [ProtectionProfile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (funzione)
Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: Lo stesso contesto passato a [ProtectionProfile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (funzione)
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **context**: Lo stesso contesto passato a [ProtectionProfile::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (funzione)
Viene chiamato quando l'eliminazione di un motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: Lo stesso contesto passato a [ProtectionProfile::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)

