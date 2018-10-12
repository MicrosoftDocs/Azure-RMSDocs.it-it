---
title: Classe mip PolicyProfile
description: Riferimento per la classe mip PolicyProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 387e28780cb0ef02d56050f534d4783fdebc286e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446862"
---
# <a name="class-mippolicyprofile"></a>Classe mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene le impostazioni configurate nel profilo.

  
**Restituisce**: impostazioni configurate nel profilo.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Avvia l'operazione di elenco motori.

Parametri:  
* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Avvia lo scaricamento del motore dei criteri con l'ID specificato.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà inoltrato in modo non trasparente alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).
  
### <a name="addengineasync"></a>AddEngineAsync
Avvia l'aggiunta di un nuovo motore dei criteri al profilo.

Parametri:  
* **settings**: oggetto [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) che specifica le impostazioni del motore. 


* **context**: parametro che verrà inoltrato in modo non trasparente alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.

Parametri:  
* **id**: ID univoco del motore. 


* **context**: parametro che verrà passato alle funzioni observer. 


In base all'esito positivo o negativo dell'operazione verrà chiamato [PolicyProfile::Observer](class_mip_policyprofile_observer.md).