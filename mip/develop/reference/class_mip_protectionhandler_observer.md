---
title: Classe mip::ProtectionHandler::Observer
description: Documenta la classe mip::protectionhandler di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 00d74069374850a562547cd161ad4c5f15927b0a
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333722"
---
# <a name="class-mipprotectionhandlerobserver"></a>Classe mip::ProtectionHandler::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
OnCreateProtectionHandlerSuccess void virtuale pubblico (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.
OnCreateProtectionHandlerFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.
  
## <a name="members"></a>Membri
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess (funzione)
Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.

Parametri:  
* **protectionHandler**: L'oggetto appena creato [ProtectionHandler](class_mip_protectionhandler.md)


* **context**: Lo stesso contesto passato a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure (funzione)
Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.

Parametri:  
* **error**: Errore che si sono verificati durante la creazione 


* **context**: Lo stesso contesto passato a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
