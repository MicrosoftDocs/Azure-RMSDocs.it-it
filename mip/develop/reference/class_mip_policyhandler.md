---
title: Classe mip PolicyHandler
description: Riferimento per la classe mip PolicyHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 23de5616558a298189cb885727d69a20373a3609
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445938"
---
# <a name="class-mippolicyhandler"></a>Classe mip::PolicyHandler 
Questa classe fornisce un'interfaccia per tutte le funzioni del gestore dei criteri in un file.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  Ottiene l'etichetta di riservatezza dal contenuto esistente.
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.
 public void NotifyCommittedActions(const ExecutionState& state)  |  Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.
  
## <a name="members"></a>Membri
  
### <a name="contentlabel"></a>ContentLabel
Ottiene l'etichetta di riservatezza dal contenuto esistente.

Parametri:  
* **state**: stato corrente del contenuto 



  
**Restituisce**: etichetta attualmente applicata al contenuto. Se non è presente alcuna etichetta, restituisce un valore vuoto.
  
### <a name="action"></a>Azione
Esegue le regole nel gestore in base allo stato specificato e restituisce l'elenco di azioni da eseguire.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto su cui sono in esecuzione le regole. 



  
**Restituisce**: elenco di azioni da applicare al contenuto.
  
### <a name="notifycommittedactions"></a>NotifyCommittedActions
Viene chiamato dopo che sono state applicate le operazioni calcolate ed è stato eseguito il commit dei dati su disco.

Parametri:  
* **state**: stato di esecuzione corrente del contenuto dopo che è stato eseguito il commit delle azioni 


: questa chiamata invia un evento di controllo