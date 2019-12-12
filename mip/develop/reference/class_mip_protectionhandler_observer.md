---
title: Classe mip::ProtectionHandler::Observer
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8b48d6e5aacacb6f678fc7d5aea2aee531da88fa
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560096"
---
# <a name="class-mipprotectionhandlerobserver"></a>Classe mip::ProtectionHandler::Observer 
Interfaccia che riceve le notifiche correlate a ProtectionHandler.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler, const std:: shared_ptr\<void\>& context)  |  Chiamato quando ProtectionHandler è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Chiamato quando la creazione del ProtectionHandler non è riuscita.
  
## <a name="members"></a>Membri
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess (funzione)
Chiamato quando ProtectionHandler è stato creato correttamente.

Parametri:  
* **protectionHandler**: protectionHandler appena creato


* **context**: lo stesso contesto passato a ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync e lo stesso contesto verrà trasmesso così com'è a ProtectionEngine:: Observer:: OnCreateProtectionHandlerSuccess o ProtectionEngine:: Observer:: OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure (funzione)
Chiamato quando la creazione del ProtectionHandler non è riuscita.

Parametri:  
* **error**: errore che si è verificato durante la creazione 


* **context**: lo stesso contesto passato a ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync o ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync e lo stesso contesto verrà trasmesso così com'è a ProtectionEngine:: Observer:: OnCreateProtectionHandlerSuccess o ProtectionEngine:: Observer:: OnCreateProtectionHandlerFailure