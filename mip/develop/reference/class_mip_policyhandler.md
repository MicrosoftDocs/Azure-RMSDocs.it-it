---
title: Classe mip::PolicyHandler
description: Documenta la classe mip::policyhandler di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6c5979706b9868bd7d0b6b1adad5d96bd5d3e0ce
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329591"
---
# <a name="class-mippolicyhandler"></a>Classe mip::PolicyHandler 
Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (ExecutionState const & state)  |  Ottiene l'etichetta di riservatezza dal contenuto esistente.
Public std:: Vector\<std:: shared_ptr\<azione\> \> ComputeActions (ExecutionState const & state)  |  Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
public void NotifyCommittedActions(const ExecutionState& state)  |  Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.
  
## <a name="members"></a>Membri
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza dal contenuto esistente.

Parametri:  
* **state**: Stato corrente del contenuto 



  
**Restituisce**: Etichetta attualmente applicato al contenuto. Se non è presente alcuna etichetta, restituisce un valore vuoto.
  
### <a name="computeactions-function"></a>ComputeActions (funzione)
Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 



  
**Restituisce**: Elenco di azioni da applicare al contenuto.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto dopo che è stato eseguito il commit delle azioni 


: Questa chiamata invia un evento di controllo
