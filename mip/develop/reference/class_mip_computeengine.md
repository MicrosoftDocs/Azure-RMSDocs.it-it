---
title: 'Classe MIP:: ComputeEngine'
description: 'Documenta la classe MIP:: computeengine di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 1faae8e64bbc2e2f2de54f8152b1227148c7d3de
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490388"
---
# <a name="class-mipcomputeengine"></a>Classe MIP:: ComputeEngine 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<std:: shared_ptr\<label\>\>& ListSensitivityLabels ()  | _Non ancora documentato._
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (ComputeEngineContext & context, const DocumentState & state)  | _Non ancora documentato._
public std:: Vector\<std:: shared_ptr\<azione\>\> ComputeActions (ComputeEngineContext & context, const DocumentState & documentState, const ApplicationActionState & actionState)  | _Non ancora documentato._
public std::p Air\<std:: Vector\<std:: shared_ptr\<Action\>\>, bool\> ComputeActionsWithRemoteState (ComputeEngineContext & context, const DocumentState & localDocumentState, const DocumentState & remoteDocumentState, const ApplicationActionState & actionState)  |  Calcola le azioni durante la scelta tra lo stato remoto e quello locale.
public void NotifyCommittedActions (ComputeEngineContext & context, const DocumentState & documentState, const ApplicationActionState & actionState)  | _Non ancora documentato._
public virtual ~ ComputeEngine ()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
_Non ancora documentato._

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (funzione)
_Non ancora documentato._

  
### <a name="computeactions-function"></a>ComputeActions (funzione)
_Non ancora documentato._

  
### <a name="computeactionswithremotestate-function"></a>ComputeActionsWithRemoteState (funzione)
Calcola le azioni durante la scelta tra lo stato remoto e quello locale.
Lo stato è selezionato con questa priorità. Tipi di protezione sconosciuti (modello o ad hoc non nel criterio). Lo stato di protezione è sempre preferibile allo stato non protetto. Lo stato del documento con etichetta è preferito sopra uno senza. È preferibile l'ordine delle etichette. Timestamp etichetta, preferisce il documento più recente con etichetta. DocumentState LastModifiedTime, facoltativamente implementato, preferisce il file appena modificato.

Parametri:  
* **contesto**: contesto del motore di calcolo. 


* **localDocumentState**: stato del documento locale. 


* **remoteDocumentState**: stato del documento remoto. 


* **actionState**: stato dell'azione dell'applicazione.



  
**Restituisce**: i metodi restituiscono una coppia. contiene prima di tutto un elenco dell'azione, il secondo è se deve essere applicato all'oggetto locale, se le azioni false devono essere applicate nel documento remoto e deve essere usato lo stato del documento.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
_Non ancora documentato._

  
### <a name="computeengine-function"></a>~ ComputeEngine (funzione)
_Non ancora documentato._
