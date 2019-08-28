---
title: Classe mip::PolicyHandler
description: Documenta la classe MIP::p olicyhandler dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 58186e1b445bdfc6d1d3d1ebfa2680697ab67404
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055772"
---
# <a name="class-mippolicyhandler"></a>Classe mip::PolicyHandler 
Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (const ExecutionState & state)  |  Ottiene l'etichetta di riservatezza dal contenuto esistente.
public std:: Vector\<std:: shared_ptr\<Action\> \> ComputeActions (const ExecutionState & state)  |  Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
public void NotifyCommittedActions(const ExecutionState& state)  |  Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.
  
## <a name="members"></a>Members
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza dal contenuto esistente.

Parametri:  
* **state**: Stato corrente del contenuto. 



  
**Restituisce**: Etichetta attualmente applicata al contenuto. Se non è presente alcuna etichetta, restituisce un valore vuoto.
  
### <a name="computeactions-function"></a>ComputeActions (funzione)
Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 



  
**Restituisce**: Elenco di azioni da applicare al contenuto.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.

Parametri:  
* **stato**: lo stato di esecuzione corrente del contenuto dopo che è stato eseguito il commit delle azioni. 


: Questa chiamata invia un evento di controllo.