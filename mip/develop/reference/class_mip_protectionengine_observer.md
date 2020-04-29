---
title: 'Classe ProtectionEngine:: Observer'
description: "Documenta la classe protectionengine:: Observer dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: ca1f9c3251df30166b123ae31c8e3c5fceef67fc
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764613"
---
# <a name="class-protectionengineobserver"></a>Classe ProtectionEngine:: Observer 
Interfaccia che riceve le notifiche correlate a ProtectionEngine.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std::\<vector std::\<shared_ptr\> \> TemplateDescriptor& templateDescriptors, const std:\<:\> shared_ptr void& context)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
public virtual void OnGetTemplatesFailure (const std:: exception_ptr& Error, const std:\<:\> shared_ptr void& context)  |  Viene chiamato quando il recupero dei modelli genera un errore.
public virtual void OnGetRightsForLabelIdSuccess (const std::\<shared_ptr std::\<vector std::\> \> String& Rights, const std\<:\> : shared_ptr void& context)  |  Viene chiamato quando i diritti vengono recuperati correttamente.
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr& Error, const std:\<:\> shared_ptr void& context)  |  Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.
public virtual void OnLoadUserCertSuccess (const std::\<shared_ptr\> void& context)  |  Chiamato quando il certificato utente viene caricato correttamente.
public virtual void OnLoadUserCertFailure (const std:: exception_ptr& Error, const std:\<:\> shared_ptr void& context)  |  Chiamato quando il certificato utente è stato caricato.
public virtual void OnRegisterContentForTrackingAndRevocationSuccess (const std::\<shared_ptr\> void& context)  |  Chiamato quando la registrazione del contenuto per il rilevamento & la revoca ha esito positivo.
public virtual void OnRegisterContentForTrackingAndRevocationFailure (const std:: exception_ptr& Error, const std:\<:\> shared_ptr void& context)  |  Chiamato quando la registrazione del contenuto per il rilevamento & la revoca ha esito negativo.
public virtual void OnRevokeContentSuccess (const std::\<shared_ptr\> void& context)  |  Chiamato quando la revoca di ha esito positivo.
public virtual void OnRevokeContentFailure (const std:: exception_ptr& Error, const std:\<:\> shared_ptr void& context)  |  Chiamato quando la revoca del contenuto non riesce.
  
## <a name="members"></a>Members
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess (funzione)
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri  
* **templateDescriptors**: riferimento all'elenco di descrittori di modelli 


* **context**: lo stesso contesto passato a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md)


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetTemplatesAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnGetTemplatesSuccess o ProtectionEngine:: Observer:: OnGetTemplatesFailure.
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure (funzione)
Viene chiamato quando il recupero dei modelli genera un errore.

Parametri  
* **errore**: si è verificato un errore durante il recupero dei modelli 


* **context**: lo stesso contesto passato a ProtectionEngine::GetTemplatesAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a ProtectionEngine::GetTemplatesAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnGetTemplatesSuccess o ProtectionEngine::Observer::OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess (funzione)
Viene chiamato quando i diritti vengono recuperati correttamente.

Parametri  
* **rights**: riferimento all'elenco dei diritti recuperati 


* **context**: lo stesso contesto passato a [ProtectionEngine:: GetRightsForLabelIdAsync](class_mip_protectionengine.md).


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetRightsForLabelIdAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess o ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure.
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure (funzione)
Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.

Parametri  
* **errore**: errore che si è verificato durante il recupero dei diritti 


* **context**: lo stesso contesto passato a ProtectionEngine::GetRightsForLabelIdAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio std::promise, std::function) a ProtectionEngine::GetRightsForLabelIdAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess o ProtectionEngine::Observer::OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess (funzione)
Chiamato quando il certificato utente viene caricato correttamente.

Parametri  
* **context**: lo stesso contesto passato a ProtectionEngine:: LoadUserCert.


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a [ProtectionEngine:: LoadUserCertAsync e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine:: Observer:: OnLoadUserCertSuccess](class_mip_protectionengine_observer.md) o [ProtectionEngine:: Observer:: OnLoadUserCertFailure](class_mip_protectionengine_observer.md)
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure (funzione)
Chiamato quando il certificato utente è stato caricato.

Parametri  
* **errore**: errore che si è verificato durante il recupero dei diritti 


* **context**: lo stesso contesto passato a ProtectionEngine:: LoadUserCert


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: LoadUserCertAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnLoadUserCertSuccess o ProtectionEngine:: Observer:: OnLoadUserCertFailure
  
### <a name="onregistercontentfortrackingandrevocationsuccess-function"></a>OnRegisterContentForTrackingAndRevocationSuccess (funzione)
Chiamato quando la registrazione del contenuto per il rilevamento & la revoca ha esito positivo.

Parametri  
* **context**: lo stesso contesto passato a ProtectionEngine:: RegisterContentForTrackingAndRevocationAsync.


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: RegisterContentForTrackingAndRevocationAsync e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationSuccess](class_mip_protectionengine_observer.md) o [ProtectionEngine:: Observer::](class_mip_protectionengine_observer.md) OnRegisterContentForTrackingAndRevocationFailure
  
### <a name="onregistercontentfortrackingandrevocationfailure-function"></a>OnRegisterContentForTrackingAndRevocationFailure (funzione)
Chiamato quando la registrazione del contenuto per il rilevamento & la revoca ha esito negativo.

Parametri  
* **errore**: si è verificato un errore durante la registrazione del contenuto 


* **context**: lo stesso contesto passato a ProtectionEngine:: RegisterContentForTrackingAndRevocationAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: RegisterContentForTrackingAndRevocationAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationSuccess o ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationFailure
  
### <a name="onrevokecontentsuccess-function"></a>OnRevokeContentSuccess (funzione)
Chiamato quando la revoca di ha esito positivo.

Parametri  
* **context**: lo stesso contesto passato a ProtectionEngine:: RevokeContentAsync.


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: RevokeContentAsync e lo stesso contesto verrà inoltrato così com'è a [ProtectionEngine:: Observer:: OnRevokeContentSuccess](class_mip_protectionengine_observer.md) o [ProtectionEngine:: Observer::](class_mip_protectionengine_observer.md) OnRevokeContentFailure
  
### <a name="onrevokecontentfailure-function"></a>OnRevokeContentFailure (funzione)
Chiamato quando la revoca del contenuto non riesce.

Parametri  
* **errore**: si è verificato un errore durante la revoca del contenuto 


* **context**: lo stesso contesto passato a ProtectionEngine:: RevokeContentAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: RevokeContentAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnRevokeContentSuccess o ProtectionEngine:: Observer:: OnRevokeContentFailure