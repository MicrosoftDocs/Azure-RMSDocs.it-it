---
title: Classe mip ProtectionHandler Observer
description: Riferimento per la classe mip ProtectionHandler Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 7fed286dec42f16d7dfa8e375ec739264bd365ba
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446176"
---
# <a name="class-mipprotectionhandlerobserver"></a>Classe mip::ProtectionHandler::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.
  
## <a name="members"></a>Membri
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.

Parametri:  
* **protectionHandler**: nuovo [ProtectionHandler](class_mip_protectionhandler.md) creato


* **context**: lo stesso contesto passato a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure"></a>OnCreateProtectionHandlerFailure
Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.

Parametri:  
* **error**: errore che si è verificato durante la creazione 


* **context**: lo stesso contesto passato a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure