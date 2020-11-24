---
title: Classe ComputeEngine
description: 'Documenta la classe computeengine:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7371c72cb10e1f08fcacaf286597f9534737996d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567225"
---
# <a name="class-computeengine"></a>Classe ComputeEngine 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<std::shared_ptr\<Label\> \>& ListSensitivityLabels ()  | _Non ancora documentato._
public std:: shared_ptr \<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& context, const DocumentState& state)  | _Non ancora documentato._
public std:: Vector \<std::shared_ptr\<Action\> \> ComputeActions (ComputeEngineContext& context, const documentState& DocumentState, const ApplicationActionState& actionState)  | _Non ancora documentato._
public std::p aria \<std::vector\<std::shared_ptr\<Action\> \> , bool \> ComputeActionsWithRemoteState (ComputeEngineContext& context, const DocumentState& localDocumentState, const DocumentState& remoteDocumentState, const ApplicationActionState& actionState)  |  Calcola le azioni durante la scelta tra lo stato remoto e quello locale.
public void NotifyCommittedActions (ComputeEngineContext& context, const DocumentState& documentState, const ApplicationActionState& actionState)  | _Non ancora documentato._
public const std:: shared_ptr \<Label\>& GetDefaultLabel () const  | _Non ancora documentato._
public const std::string& GetMoreInfoUrl() const  | _Non ancora documentato._
public const std:: String& GetUpn () const  | _Non ancora documentato._
public bool IsLabelingRequired() const  | _Non ancora documentato._
public const std:: String& GetFileId () const  | _Non ancora documentato._
public bool HasClassificationRules () const  | _Non ancora documentato._
public bool IsEnhancedClassificationEnabled () const  | _Non ancora documentato._
public std:: shared_ptr \<Label\> GetLabelById (const std:: string& ID) const  | _Non ancora documentato._
public const std:: String& GetTenantId () const  | _Non ancora documentato._
public void SetSensitivityTypesRulePackages (STD:: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \> && Custom)  | _Non ancora documentato._
public const std:: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& GetSensitivityTypesRulePackages () const  | _Non ancora documentato._
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  | _Non ancora documentato._
public uint32_t GetOpcMetadataVersion () const  | _Non ancora documentato._
public const std:: String& GetUserObjectId () const  | _Non ancora documentato._
public virtual ~ ComputeEngine ()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Non ancora documentato.

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (funzione)
Non ancora documentato.

  
### <a name="computeactions-function"></a>ComputeActions (funzione)
Non ancora documentato.

  
### <a name="computeactionswithremotestate-function"></a>ComputeActionsWithRemoteState (funzione)
Calcola le azioni durante la scelta tra lo stato remoto e quello locale.
Lo stato è selezionato con questa priorità. Tipi di protezione sconosciuti (modello o ad hoc non nel criterio). Lo stato di protezione è sempre preferibile allo stato non protetto. Lo stato del documento con etichetta è preferito sopra uno senza. È preferibile l'ordine delle etichette. Timestamp etichetta, preferisce il documento più recente con etichetta. DocumentState LastModifiedTime, facoltativamente implementato, preferisce il file appena modificato.

Parametri  
* **contesto**: contesto del motore di calcolo. 


* **localDocumentState**: stato del documento locale. 


* **remoteDocumentState**: stato del documento remoto. 


* **actionState**: stato dell'azione dell'applicazione.



  
**Restituisce**: i metodi restituiscono una coppia. contiene prima di tutto un elenco dell'azione, il secondo è se deve essere applicato all'oggetto locale, se le azioni false devono essere applicate nel documento remoto e deve essere usato lo stato del documento.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (funzione)
Non ancora documentato.

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel (funzione)
Non ancora documentato.

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Non ancora documentato.

  
### <a name="getupn-function"></a>GetUpn (funzione)
Non ancora documentato.

  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Non ancora documentato.

  
### <a name="getfileid-function"></a>GetFileId (funzione)
Non ancora documentato.

  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
Non ancora documentato.

  
### <a name="isenhancedclassificationenabled-function"></a>IsEnhancedClassificationEnabled (funzione)
Non ancora documentato.

  
### <a name="getlabelbyid-function"></a>GetLabelById (funzione)
Non ancora documentato.

  
### <a name="gettenantid-function"></a>GetTenantId (funzione)
Non ancora documentato.

  
### <a name="setsensitivitytypesrulepackages-function"></a>SetSensitivityTypesRulePackages (funzione)
Non ancora documentato.

  
### <a name="getsensitivitytypesrulepackages-function"></a>GetSensitivityTypesRulePackages (funzione)
Non ancora documentato.

  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Non ancora documentato.

  
### <a name="getopcmetadataversion-function"></a>GetOpcMetadataVersion (funzione)
Non ancora documentato.

  
### <a name="getuserobjectid-function"></a>GetUserObjectId (funzione)
Non ancora documentato.

  
### <a name="computeengine-function"></a>~ ComputeEngine (funzione)
Non ancora documentato.
