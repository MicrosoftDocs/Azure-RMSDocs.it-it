---
title: Classe mip::ProtectionEngine::Observer
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7873ed66eb131e3d551c19fb103eb04f9279dc54
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883469"
---
# <a name="class-mipprotectionengineobserver"></a>Classe mip::ProtectionEngine::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std::\<shared_ptr std::\<vector std::\>String\>& templateIds, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il recupero dei modelli genera un errore.
public virtual void OnGetRightsForLabelIdSuccess (const std::\<shared_ptr std::\<vector std::\>String\>& Rights, const std\<:\>: shared_ptr void & context)  |  Viene chiamato quando i diritti vengono recuperati correttamente.
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.
  
## <a name="members"></a>Members
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess (funzione)
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri:  
* **templateIds**: Riferimento all'elenco di modelli recuperati 


* **context**: Lo stesso contesto passato a [ProtectionEngine:: GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure (funzione)
Viene chiamato quando il recupero dei modelli genera un errore.

Parametri:  
* **errore**: [Errore](class_mip_error.md) che si è verificato durante il recupero dei modelli 


* **context**: Lo stesso contesto passato a [ProtectionEngine:: GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess (funzione)
Viene chiamato quando i diritti vengono recuperati correttamente.

Parametri:  
* **diritti**: Riferimento all'elenco dei diritti recuperati 


* **context**: Lo stesso contesto passato a ProtectionEngine:: GetRightsForLabelIdAsync.


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetRightsForLabelIdAsync. e lo stesso contesto verrà trasmesso così com'è a [ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure (funzione)
Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.

Parametri:  
* **errore**: [Errore](class_mip_error.md) che si è verificato durante il recupero dei diritti 


* **context**: Lo stesso contesto passato a ProtectionEngine:: GetRightsForLabelIdAsync.


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetRightsForLabelIdAsync e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)