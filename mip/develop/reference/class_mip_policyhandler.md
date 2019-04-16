---
title: Classe mip::PolicyHandler
description: Documenta la classe mip::policyhandler di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7cc1eeeafa4a086631f5d3c376643b5758002679
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59572835"
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
* **state**: Stato corrente del contenuto. 



  
**Restituisce**: Etichetta attualmente applicato al contenuto. Se non è presente alcuna etichetta, restituisce un valore vuoto.
  
### <a name="computeactions-function"></a>ComputeActions (funzione)
Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 



  
**Restituisce**: Elenco di azioni da applicare al contenuto.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.

Parametri:  
* **stato**: lo stato di esecuzione corrente del contenuto dopo le azioni sono state salvate. 


: Questa chiamata invia un evento di controllo.