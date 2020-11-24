---
title: 'Classe ProtectionProfile:: Observer'
description: "Documenta la classe protectionprofile:: Observer dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d72a5a7d5818ee4482b2f25f8df45f6a2152f898
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567104"
---
# <a name="class-protectionprofileobserver"></a>Classe ProtectionProfile:: Observer 
Interfaccia che riceve le notifiche correlate a ProtectionProfile.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr\<ProtectionProfile\>& profile, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il profilo è stato caricato correttamente.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il caricamento di un profilo ha causato un errore.
public virtual void OnListEnginesSuccess (const std:: Vector \<std::string\>& engineIds, const std:: shared_ptr \<void\>& context)  |  Viene chiamato quando l'elenco dei motori è stato generato correttamente.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.
public virtual void OnAddEngineSuccess(const std::shared_ptr\<ProtectionEngine\>& engine, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando un nuovo motore è stato aggiunto correttamente.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Viene chiamato quando un motore è stato eliminato correttamente.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando l'eliminazione di un motore ha restituito un errore.
  
## <a name="members"></a>Members
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (funzione)
Viene chiamato quando il profilo è stato caricato correttamente.

Parametri  
* **profile**: riferimento all'oggetto ProtectionProfile appena creato


* **context**: lo stesso contesto passato a ProtectionProfile::LoadAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a ProtectionProfile::LoadAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionProfile::Observer::OnLoadSuccess o ProtectionProfile::Observer::OnLoadFailure
  
### <a name="onloadfailure-function"></a>OnLoadFailure (funzione)
Viene chiamato quando il caricamento di un profilo ha causato un errore.

Parametri  
* **errore**: si è verificato un errore durante il caricamento 


* **context**: lo stesso contesto passato a ProtectionProfile::LoadAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a ProtectionProfile::LoadAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionProfile::Observer::OnLoadSuccess o ProtectionProfile::Observer::OnLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (funzione)
Viene chiamato quando l'elenco dei motori è stato generato correttamente.

Parametri  
* **engineIds**: elenco di ID di motore disponibili. 


* **context**: lo stesso contesto passato a ProtectionProfile::ListEnginesAsync


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (funzione)
Viene chiamato quando il recupero dell'elenco dei motori ha restituito un errore.

Parametri  
* **error**: errore che ha causato il fallimento dell'operazione di elenco motori. 


* **context**: lo stesso contesto passato a ProtectionProfile::ListEnginesAsync


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (funzione)
Viene chiamato quando un nuovo motore è stato aggiunto correttamente.

Parametri  
* **motore**: motore appena creato 


* **context**: lo stesso contesto passato a ProtectionProfile::AddEngineAsync


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (funzione)
Viene chiamato quando l'aggiunta di un nuovo motore ha restituito un errore.

Parametri  
* **error**: errore che ha causato il fallimento dell'operazione di aggiunta motore. 


* **context**: lo stesso contesto passato a ProtectionProfile::AddEngineAsync


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (funzione)
Viene chiamato quando un motore è stato eliminato correttamente.

Parametri  
* **context**: lo stesso contesto passato a ProtectionProfile::DeleteEngineAsync


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (funzione)
Viene chiamato quando l'eliminazione di un motore ha restituito un errore.

Parametri  
* **error**: errore che ha causato il fallimento dell'operazione di eliminazione motore. 


* **context**: lo stesso contesto passato a ProtectionProfile::DeleteEngineAsync

