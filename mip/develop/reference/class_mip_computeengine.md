---
title: Classe ComputeEngine
description: 'Documenta la classe computeengine:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd3f287022b567ba2531108f9f24f614a3bb6b01
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211907"
---
# <a name="class-computeengine"></a>Classe ComputeEngine 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels (const std:: Vector \<std::string\>& contentFormats)  | _Non ancora documentato._
public std:: shared_ptr \<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& context, const DocumentState& state)  | _Non ancora documentato._
public std:: Vector \<std::shared_ptr\<Action\> \> ComputeActions (ComputeEngineContext& context, const documentState& DocumentState, const ApplicationActionState& actionState)  | _Non ancora documentato._
public std::p aria \<std::vector\<std::shared_ptr\<Action\> \> , bool \> ComputeActionsWithRemoteState (ComputeEngineContext& context, const DocumentState& localDocumentState, const DocumentState& remoteDocumentState, const ApplicationActionState& actionState)  |  Calcola le azioni durante la scelta tra lo stato remoto e quello locale.
public void NotifyCommittedActions (ComputeEngineContext& context, const DocumentState& documentState, const ApplicationActionState& actionState)  | _Non ancora documentato._
public const std:: shared_ptr \<Label\> GetDefaultLabel (const std:: string& contentFormat) const  | _Non ancora documentato._
public const std::string& GetMoreInfoUrl() const  | _Non ancora documentato._
public const std:: String& GetUpn () const  | _Non ancora documentato._
public bool IsLabelingRequired (const std:: String& contentFormat) const  | _Non ancora documentato._
public const std:: String& GetFileId () const  | _Non ancora documentato._
public bool HasClassificationRules (const std:: Vector \<std::string\>& contentFormats) const  | _Non ancora documentato._
public bool IsEnhancedClassificationEnabled () const  | _Non ancora documentato._
public std:: shared_ptr \<Label\> GetLabelById (const std:: string& ID) const  | _Non ancora documentato._
public const std:: String& GetTenantId () const  | _Non ancora documentato._
public void SetSensitivityTypesRulePackages (STD:: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \> && Custom)  | _Non ancora documentato._
public const std:: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& GetSensitivityTypesRulePackages () const  | _Non ancora documentato._
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  | _Non ancora documentato._
public uint32_t GetOpcMetadataVersion () const  | _Non ancora documentato._
public const std:: String& GetUserObjectId () const  | _Non ancora documentato._
public virtual ~ ComputeEngine ()  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
_Non ancora documentato._

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (funzione)
_Non ancora documentato._

  
### <a name="computeactions-function"></a>ComputeActions (funzione)
_Non ancora documentato._

  
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
_Non ancora documentato._

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel (funzione)
_Non ancora documentato._

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
_Non ancora documentato._

  
### <a name="getupn-function"></a>GetUpn (funzione)
_Non ancora documentato._

  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
_Non ancora documentato._

  
### <a name="getfileid-function"></a>GetFileId (funzione)
_Non ancora documentato._

  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
_Non ancora documentato._

  
### <a name="isenhancedclassificationenabled-function"></a>IsEnhancedClassificationEnabled (funzione)
_Non ancora documentato._

  
### <a name="getlabelbyid-function"></a>GetLabelById (funzione)
_Non ancora documentato._

  
### <a name="gettenantid-function"></a>GetTenantId (funzione)
_Non ancora documentato._

  
### <a name="setsensitivitytypesrulepackages-function"></a>SetSensitivityTypesRulePackages (funzione)
_Non ancora documentato._

  
### <a name="getsensitivitytypesrulepackages-function"></a>GetSensitivityTypesRulePackages (funzione)
_Non ancora documentato._

  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
_Non ancora documentato._

  
### <a name="getopcmetadataversion-function"></a>GetOpcMetadataVersion (funzione)
_Non ancora documentato._

  
### <a name="getuserobjectid-function"></a>GetUserObjectId (funzione)
_Non ancora documentato._

  
### <a name="computeengine-function"></a>~ ComputeEngine (funzione)
_Non ancora documentato._
