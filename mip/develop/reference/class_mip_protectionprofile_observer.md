---
title: Classe mip::ProtectionProfile::Observer
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a9138e497655dfa939a9ac9b15d7ed228331e9e0
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560709"
---
# <a name="class-mipprotectionprofileobserver"></a>Classe mip::ProtectionProfile::Observer 
Interfaccia che riceve le notifiche correlate a ProtectionProfile.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std:: shared_ptr\<ProtectionProfile\>& profile, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess (const std:: Vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<ProtectionEngine\>& Engine, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando l'eliminazione di un motore ha restituito un errore.
  
## <a name="members"></a>Membri
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri:  
* **profile**: riferimento al ProtectionProfile appena creato


* **context**: lo stesso contesto passato a ProtectionProfile::LoadAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionProfile:: LoadAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionProfile:: Observer:: OnLoadSuccess o ProtectionProfile:: Observer:: O nLoadFailure
  
### <a name="onloadfailure-function"></a>OnLoadFailure (funzione)
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri:  
* **errore**: si è verificato un errore durante il caricamento 


* **context**: lo stesso contesto passato a ProtectionProfile::LoadAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionProfile:: LoadAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionProfile:: Observer:: OnLoadSuccess o ProtectionProfile:: Observer:: O nLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (funzione)
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri:  
* **engineIds**: elenco degli ID motore disponibili. 


* **context**: lo stesso contesto passato a ProtectionProfile:: ListEnginesAsync


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (funzione)
Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: lo stesso contesto passato a ProtectionProfile:: ListEnginesAsync


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (funzione)
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.

Parametri:  
* **motore**: motore appena creato 


* **context**: lo stesso contesto passato a ProtectionProfile:: AddEngineAsync


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (funzione)
Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: lo stesso contesto passato a ProtectionProfile:: AddEngineAsync


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (funzione)
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri:  
* **context**: lo stesso contesto passato a ProtectionProfile::D eleteengineasync


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (funzione)
Viene chiamato quando l'eliminazione di un motore ha restituito un errore.

Parametri:  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: lo stesso contesto passato a ProtectionProfile::D eleteengineasync

