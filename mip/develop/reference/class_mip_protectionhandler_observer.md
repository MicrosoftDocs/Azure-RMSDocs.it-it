---
title: Classe mip::ProtectionHandler::Observer
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 0e1a1d039928e1244d6c279fe055330eac7f9577
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883395"
---
# <a name="class-mipprotectionhandlerobserver"></a>Classe mip::ProtectionHandler::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionHandler](class_mip_protectionhandler.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std::\<shared_ptr\>ProtectionHandler & ProtectionHandler, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.
  
## <a name="members"></a>Members
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess (funzione)
Viene chiamato quando [ProtectionHandler](class_mip_protectionhandler.md) è stato creato correttamente.

Parametri:  
* **protectionHandler**: [ProtectionHandler](class_mip_protectionhandler.md) appena creato


* **context**: Lo stesso contesto passato a [ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure (funzione)
Viene chiamato quando la creazione di [ProtectionHandler](class_mip_protectionhandler.md) non è riuscita.

Parametri:  
* **errore**: Errore che si è verificato durante la creazione 


* **context**: Lo stesso contesto passato a [ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure