---
title: Classe mip::ProtectionHandler::Observer
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8f661f3ebf9bc657a4dd6f6356b26cd582d4aa2e
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486818"
---
# <a name="class-mipprotectionhandlerobserver"></a>Classe mip::ProtectionHandler::Observer 
Interfaccia che riceve le notifiche correlate a ProtectionHandler.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler, const std:: shared_ptr\<void\>& context)  |  Chiamato quando ProtectionHandler è stato creato correttamente.
public virtual void OnCreateProtectionHandlerFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Chiamato quando la creazione del ProtectionHandler non è riuscita.
  
## <a name="members"></a>Members
  
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