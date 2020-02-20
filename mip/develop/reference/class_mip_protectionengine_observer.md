---
title: Classe mip::ProtectionEngine::Observer
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 688bc59b992e885b2b9724111c19f69f860badd9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489674"
---
# <a name="class-mipprotectionengineobserver"></a>Classe mip::ProtectionEngine::Observer 
Interfaccia che riceve le notifiche correlate a ProtectionEngine.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: Vector\<std:: shared_ptr\<TemplateDescriptor\>\>& templateDescriptors, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando il recupero dei modelli genera un errore.
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& Rights, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando i diritti vengono recuperati correttamente.
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.
public virtual void OnLoadUserCertSuccess (const std:: shared_ptr\<void\>& context)  |  Chiamato quando il certificato utente viene caricato correttamente.
public virtual void OnLoadUserCertFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Chiamato quando il certificato utente è stato caricato.
  
## <a name="members"></a>Members
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess (funzione)
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri:  
* **templateDescriptors**: riferimento all'elenco di descrittori di modelli 


* **context**: lo stesso contesto passato a ProtectionEngine:: GetTemplatesAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetTemplatesAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnGetTemplatesSuccess o ProtectionEngine:: O bserver:: OnGetTemplatesFailure
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure (funzione)
Viene chiamato quando il recupero dei modelli genera un errore.

Parametri:  
* **errore**: si è verificato un errore durante il recupero dei modelli 


* **context**: lo stesso contesto passato a ProtectionEngine:: GetTemplatesAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetTemplatesAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnGetTemplatesSuccess o ProtectionEngine:: O bserver:: OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess (funzione)
Viene chiamato quando i diritti vengono recuperati correttamente.

Parametri:  
* **rights**: riferimento all'elenco dei diritti recuperati 


* **context**: lo stesso contesto passato a ProtectionEngine:: GetRightsForLabelIdAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetRightsForLabelIdAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess o ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure (funzione)
Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.

Parametri:  
* **errore**: errore che si è verificato durante il recupero dei diritti 


* **context**: lo stesso contesto passato a ProtectionEngine:: GetRightsForLabelIdAsync


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: GetRightsForLabelIdAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess o ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess (funzione)
Chiamato quando il certificato utente viene caricato correttamente.

Parametri:  
* **context**: lo stesso contesto passato a ProtectionEngine:: LoadUserCert


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: LoadUserCertAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnLoadUserCertSuccess o ProtectionEngine:: O bserver:: OnLoadUserCertFailure
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure (funzione)
Chiamato quando il certificato utente è stato caricato.

Parametri:  
* **errore**: errore che si è verificato durante il recupero dei diritti 


* **context**: lo stesso contesto passato a ProtectionEngine:: LoadUserCert


Un'applicazione può passare qualsiasi tipo di contesto (ad esempio, std::p romise, std:: Function) a ProtectionEngine:: LoadUserCertAsync e lo stesso contesto verrà inoltrato così com'è a ProtectionEngine:: Observer:: OnLoadUserCertSuccess o ProtectionEngine:: O bserver:: OnLoadUserCertFailure