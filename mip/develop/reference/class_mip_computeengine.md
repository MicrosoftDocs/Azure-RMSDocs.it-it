---
title: Classe ComputeEngine
description: 'Documenta la classe computeengine:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3b33c9a91f40422c29282ddee9292f6bbbad90c9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763511"
---
# <a name="class-computeengine"></a>Classe ComputeEngine 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::\<vector std::\<shared_ptr\> \> label& ListSensitivityLabels ()  | _Non ancora documentato._
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& context, const DocumentState& state)  | _Non ancora documentato._
public std:: Vector\<std:: shared_ptr\<Action\> \> ComputeActions (ComputeEngineContext& context, const DocumentState& DocumentState, const ApplicationActionState& actionState)  | _Non ancora documentato._
public std::p Air\<std:: Vector\<std:: shared_ptr\<Action\>\>, bool\> ComputeActionsWithRemoteState (ComputeEngineContext& context, const DocumentState& localDocumentState, const DocumentState& remoteDocumentState, const ApplicationActionState& actionState)  |  Calcola le azioni durante la scelta tra lo stato remoto e quello locale.
public void NotifyCommittedActions (ComputeEngineContext& context, const DocumentState& documentState, const ApplicationActionState& actionState)  | _Non ancora documentato._
public const std::\<shared_ptr\> label& GetDefaultLabel () const  | _Non ancora documentato._
public const std::string& GetMoreInfoUrl() const  | _Non ancora documentato._
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
Lo stato è selezionato con questa priorità. Tipi di protezione sconosciuti (modello o ad hoc non nel criterio). Lo stato di protezione è sempre preferibile allo stato non protetto. Lo stato del documento con etichetta è preferito sopra uno senza. È preferibile l'ordine delle etichette. Timestamp etichetta, preferisce il documento più recente con etichetta. [DocumentState](class_mip_documentstate.md) LastModifiedTime implementato facoltativamente, preferisce il file appena modificato.

Parametri  
* **contesto**: contesto del motore di calcolo. 


* **localDocumentState**: stato del documento locale. 


* **remoteDocumentState**: stato del documento remoto. 


* **actionState**: stato dell'azione dell'applicazione.



  
**Restituisce**: i metodi restituiscono una coppia. contiene prima di tutto un elenco dell'azione, il secondo è se deve essere applicato all'oggetto locale, se le azioni false devono essere applicate nel documento remoto e deve essere usato lo stato del documento.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
_Non ancora documentato._

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel (funzione)
_Non ancora documentato._

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
_Non ancora documentato._

  
### <a name="computeengine-function"></a>~ ComputeEngine (funzione)
_Non ancora documentato._
