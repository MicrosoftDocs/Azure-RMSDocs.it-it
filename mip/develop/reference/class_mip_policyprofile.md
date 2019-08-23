---
title: Classe mip::PolicyProfile
description: Documenta la classe MIP::p olicyprofile dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 13d24afe87bc04f7a92dde8daf88c1ada38cedc2
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883760"
---
# <a name="class-mippolicyprofile"></a>Classe mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection. Un'applicazione tipica avrà bisogno di un solo [PolicyProfile](class_mip_policyprofile.md), ma se necessario può creare più profili.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene le impostazioni configurate nel profilo.
public void ListEnginesAsync (const std::\<shared_ptr\>void & context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync (const std:: String & ID, const std:\<:\>shared_ptr void & context)  |  Avvia lo scaricamento del motore dei criteri con l'ID specificato.
public void AddEngineAsync (const PolicyEngine:: Settings & Settings, const std:\<:\>shared_ptr void & context)  |  Avvia l'aggiunta di un nuovo motore dei criteri al profilo.
public void DeleteEngineAsync (const std:: String & ID, const std:\<:\>shared_ptr void & context)  |  Avvia l'eliminazione del motore dei criteri con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene le impostazioni configurate nel profilo.

  
**Restituisce**: Impostazioni impostate nel profilo.
  
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