---
title: Classe mip::PolicyEngine
description: 'Classe MIP:: policyengine di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ce8ef7df12cdc9823a62234b5dadaaacdb7fed37
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173649"
---
# <a name="class-mippolicyengine"></a>Classe mip::PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene [Settings](class_mip_policyengine_settings.md) del motore dei criteri.
Public std:: Vector const\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Elenca le etichette di riservatezza associate al motore dei criteri.
Public std:: Vector const\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Elenca i tipi di riservatezza associati al motore di criteri.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere o meno etichettato.
public std::shared_ptr\<Label\> GetDefaultSensitivityLabel()  |  Ottiene l'etichetta di riservatezza predefinita.
Public std:: shared_ptr\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
public const std::string& GetPolicyDataXml() const  |  Ottiene i dati dei criteri XML che descrive le impostazioni, le etichette e regole associate a questo criterio.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene un elenco di impostazioni personalizzate.
Public std:: String const & GetPolicyId() const  |  Ottiene l'ID criteri.
public bool HasClassificationRules() const  |  Ottiene se il criterio ha regole automatico o raccomandazione.
pubblica std::chrono::time_point\<std\> GetLastPolicyFetchTime() const  |  Ottiene l'ora dell'ultimo recupero quando il criterio.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene [Settings](class_mip_policyengine_settings.md) del motore dei criteri.

  
**Restituisce**: Impostazioni del motore dei criteri. 
  
**Vedere anche**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Elenca le etichette di riservatezza associate al motore dei criteri.

  
**Restituisce**: Un elenco di etichette di riservatezza.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
Elenca i tipi di riservatezza associati al motore di criteri.

  
**Restituisce**: Un elenco di etichette di riservatezza. vuoto se LoadSensitivityTypesEnabled era (false
  
**Vedere anche**: [PolicyEngine::Settings](class_mip_policyengine_settings.md)).
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: Un url in formato stringa.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Controlla se il criterio determina che un documento deve essere o meno etichettato.

  
**Restituisce**: True se l'assegnazione di etichette è obbligatorio, altrimenti false.
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: Etichetta di riservatezza predefinita se esistente, nullptr se è presente alcun set di etichetta predefinita.
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler (funzione)
Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.

Parametri:  
* **Oggetto**: bool che indica se il rilevamento di controllo è abilitato o meno.



  
**Restituisce**: Gestore dei criteri.
Applicazione deve mantenere l'oggetto di gestore dei criteri per la durata del documento.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (funzione)
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri:  
* **livello**: del livello di log: Info/errore/avviso. 


* **eventType**: una descrizione del tipo di evento. 


* **eventData**: i dati associati all'evento.


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml (funzione)
Ottiene i dati dei criteri XML che descrive le impostazioni, le etichette e regole associate a questo criterio.

  
**Restituisce**: Dati dei criteri XML.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di impostazioni personalizzate.

  
**Restituisce**: Vettore di impostazioni personalizzate.
  
### <a name="getpolicyid-function"></a>GetPolicyId (funzione)
Ottiene l'ID criteri.

  
**Restituisce**: Stringa che rappresenta l'ID dei criteri
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
Ottiene se il criterio ha regole automatico o raccomandazione.

  
**Restituisce**: Un valore booleano che indica se esiste qualsiasi automatico o recommandation regole nel criterio
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero quando il criterio.

  
**Restituisce**: L'ora dell'ultimo recupero quando il criterio