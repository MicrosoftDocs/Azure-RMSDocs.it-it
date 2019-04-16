---
title: Classe mip::ProtectionEngine::Observer
description: Documenta la classe mip::protectionengine di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2473e4bc1e64e3e8de498d2976d07b5324346a53
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573497"
---
# <a name="class-mipprotectionengineobserver"></a>Classe mip::ProtectionEngine::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
OnGetTemplatesSuccess void virtuale pubblico (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& templateIds, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
OnGetTemplatesFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il recupero dei modelli genera un errore.
OnGetRightsForLabelIdSuccess void virtuale pubblico (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& diritti, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando i diritti vengono recuperati correttamente.
OnGetRightsForLabelIdFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.
  
## <a name="members"></a>Membri
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess (funzione)
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri:  
* **templateIds**: Recuperare un riferimento all'elenco dei modelli 


* **context**: Lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure (funzione)
Viene chiamato quando il recupero dei modelli genera un errore.

Parametri:  
* **error**: [Errore](class_mip_error.md) che si è verificato durante il recupero dei modelli 


* **context**: Lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess (funzione)
Viene chiamato quando i diritti vengono recuperati correttamente.

Parametri:  
* **diritti**: Recupera un riferimento all'elenco di diritti 


* **context**: Lo stesso contesto passato a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure (funzione)
Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.

Parametri:  
* **error**: [Errore](class_mip_error.md) che si è verificato durante il recupero dei diritti 


* **context**: Lo stesso contesto passato a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)