---
title: 'Classe ProtectionHandler:: Observer'
description: "Documenta la classe protectionhandler:: Observer dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 092448f4af5c27625b8a19f7cfea039e9bcd8071
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567140"
---
# <a name="class-protectionhandlerobserver"></a>Classe ProtectionHandler:: Observer 
Interfaccia che riceve le notifiche correlate a ProtectionHandler.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr\<ProtectionHandler\>& protectionHandler, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando ProtectionHandler è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando la creazione di ProtectionHandler non è riuscita.
  
## <a name="members"></a>Members
  
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