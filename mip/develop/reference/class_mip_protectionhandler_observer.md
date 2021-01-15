---
title: 'Classe ProtectionHandler:: Observer'
description: "Documenta la classe protectionhandler:: Observer dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd7a2b24b5eb80b3b17c025c43b0e0b31589a00a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214542"
---
# <a name="class-protectionhandlerobserver"></a>Classe ProtectionHandler:: Observer 
Interfaccia che riceve le notifiche correlate a ProtectionHandler.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr\<ProtectionHandler\>& protectionHandler, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando ProtectionHandler è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando la creazione di ProtectionHandler non è riuscita.
  
## <a name="members"></a>Membri
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess (funzione)
Viene chiamato quando ProtectionHandler è stato creato correttamente.

Parametri  
* **protectionHandler**: nuovo ProtectionHandler creato


* **context**: lo stesso contesto passato a ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure (funzione)
Viene chiamato quando la creazione di ProtectionHandler non è riuscita.

Parametri  
* **error**: errore che si è verificato durante la creazione 


* **context**: lo stesso contesto passato a ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure