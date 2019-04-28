---
title: Classe mip::PolicyProfile
description: Documenta la classe mip::policyprofile di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 45af1f4d072a1d8a690aa8f459950ae500df3db8
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173338"
---
# <a name="class-mippolicyprofile"></a>Classe mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& contesto)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync (const std:: String & id, const std:: shared_ptr\<void\>& contesto)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
pubblica AddEngineAsync void (PolicyEngine::Settings const & impostazioni, const std:: shared_ptr\<void\>& contesto)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public void DeleteEngineAsync (const std:: String & id, const std:: shared_ptr\<void\>& contesto)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni configurate nel profilo.

  
**Restituisce**: Le impostazioni configurate nel profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà inoltrato in modo non trasparente alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore dei criteri al profilo.

Parametri:  
* **settings**: oggetto [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) che specifica le impostazioni del motore. 


* **context**: parametro che verrà inoltrato in modo non trasparente alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).