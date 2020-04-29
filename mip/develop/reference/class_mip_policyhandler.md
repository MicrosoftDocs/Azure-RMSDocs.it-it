---
title: Classe PolicyHandler
description: 'Documenta la classe PolicyHandler:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: c46b72f3a040204b4485da14f00f38ca69fa8222
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760946"
---
# <a name="class-policyhandler"></a>Classe PolicyHandler 
Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (const ExecutionState& state)  |  Ottiene l'etichetta di riservatezza dal contenuto esistente.
public std:: Vector\<std:: shared_ptr\<Action\> \> ComputeActions (const ExecutionState& state)  |  Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
public void NotifyCommittedActions(const ExecutionState& state)  |  Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.
  
## <a name="members"></a>Members
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza dal contenuto esistente.

Parametri  
* **stato**: stato corrente del contenuto. 



  
**Restituisce**: etichetta attualmente applicata al contenuto. Se non è presente alcuna etichetta, restituisce un valore vuoto.
  
### <a name="computeactions-function"></a>ComputeActions (funzione)
Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.

Parametri  
* **state**: stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 



  
**Restituisce**: elenco di azioni da applicare al contenuto.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.

Parametri  
* **stato**: lo stato di esecuzione corrente del contenuto dopo che è stato eseguito il commit delle azioni. 


: Questa chiamata invia un evento di controllo.