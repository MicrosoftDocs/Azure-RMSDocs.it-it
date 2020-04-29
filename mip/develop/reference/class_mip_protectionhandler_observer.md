---
title: 'Classe ProtectionHandler:: Observer'
description: "Documenta la classe protectionhandler:: Observer dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 66453d343505cc57427e177eac258b83a2663eb0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764444"
---
# <a name="class-protectionhandlerobserver"></a>Classe ProtectionHandler:: Observer 
Interfaccia che riceve le notifiche correlate a ProtectionHandler.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std::\<shared_ptr\> ProtectionHandler& ProtectionHandler, const std:\<:\> shared_ptr void& context)  |  Viene chiamato quando ProtectionHandler è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure (const std:: exception_ptr& Error, const std:\<:\> shared_ptr void& context)  |  Viene chiamato quando la creazione di ProtectionHandler non è riuscita.
  
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