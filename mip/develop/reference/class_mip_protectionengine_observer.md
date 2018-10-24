---
title: Classe mip ProtectionEngine Observer
description: Riferimento per la classe mip ProtectionEngine Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5c5b5e807a80c8db3cbdb69ea5d09da1e79aec6e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446584"
---
# <a name="class-mipprotectionengineobserver"></a>Classe mip::ProtectionEngine::Observer 
Interfaccia che riceve le notifiche correlate a [ProtectionEngine](class_mip_protectionengine.md).
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei modelli genera un errore.
public virtual void OnGetRightsForLabelIdSuccess(const std::shared_ptr<std::vector<std::string>>& rights, const std::shared_ptr<void>& context)  |  Viene chiamato quando i diritti vengono recuperati correttamente.
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.
public virtual void OnGetGrantingLabelIdsSuccess(const std::shared_ptr<std::vector<std::string>>& lableIds, const std::shared_ptr<void>& context)  |  Viene chiamato quando gli ID etichetta vengono recuperati correttamente.
public virtual void OnGetGrantingLabelIdsFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando si recuperano gli ID etichetta per l'utente.
  
## <a name="members"></a>Membri
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri:  
* **templateIds**: riferimento all'elenco di modelli recuperati 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
Viene chiamato quando il recupero dei modelli genera un errore.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il recupero dei modelli 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongetrightsforlabelidsuccess"></a>OnGetRightsForLabelIdSuccess
Viene chiamato quando i diritti vengono recuperati correttamente.

Parametri:  
* **rights**: riferimento all'elenco dei diritti recuperati 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetrightsforlabelidfailure"></a>OnGetRightsForLabelIdFailure
Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il recupero dei diritti 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetgrantinglabelidssuccess"></a>OnGetGrantingLabelIdsSuccess
Viene chiamato quando gli ID etichetta vengono recuperati correttamente.

Parametri:  
* **lableIds**: riferimento all'elenco di ID etichetta recuperati 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) o [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)
  
### <a name="ongetgrantinglabelidsfailure"></a>OnGetGrantingLabelIdsFailure
Viene chiamato quando si recuperano gli ID etichetta per l'utente.

Parametri:  
* **error**: evento [Error](class_mip_error.md) che si è verificato durante il recupero degli ID etichetta 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) o [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)