---
title: Classe mip::ProtectionEngine::Observer
description: Documenta la classe MIP::p rotectionengine dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e5196535dc474d2649c084b55c55a80c3af349b9
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560750"
---
# <a name="class-mipprotectionengineobserver"></a>Classe mip::ProtectionEngine::Observer 
Interfaccia che riceve le notifiche correlate a ProtectionEngine.
Questa interfaccia deve essere implementata dalle applicazioni che usano l'SDK di protezione
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& templateIds, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando i modelli vengono recuperati correttamente.
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando il recupero dei modelli genera un errore.
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& Rights, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando i diritti vengono recuperati correttamente.
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & Error, const std:: shared_ptr\<void\>& context)  |  Viene chiamato quando si recuperano i diritti per un ID etichetta per l'utente.
  
## <a name="members"></a>Membri
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess (funzione)
Viene chiamato quando i modelli vengono recuperati correttamente.

Parametri:  
* **templateIds**: riferimento all'elenco di modelli recuperati 


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