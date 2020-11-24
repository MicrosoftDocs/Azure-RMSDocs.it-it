---
title: classe PolicyEngine
description: 'Documenta la classe PolicyEngine:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 733e1ced7a1f5ca1ec8d47709ef4c364c04e37a5
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566672"
---
# <a name="class-policyengine"></a>classe PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene Settings del motore dei criteri.
public const std:: Vector \<std::shared_ptr\<Label\> \>& ListSensitivityLabels ()  |  Elenca le etichette di riservatezza associate al motore dei criteri.
public const std:: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& ListSensitivityTypes () const  |  elencare i tipi di riservatezza associati al motore dei criteri.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere o meno etichettato.
public std::shared_ptr\<Label\> GetDefaultSensitivityLabel()  |  Ottiene l'etichetta di riservatezza predefinita.
public std:: shared_ptr \<Label\> GetLabelById (const std:: string& ID) const  |  Ottiene l'etichetta in base all'ID fornito.
public std:: shared_ptr \<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
public const std:: String& GetTenantId () const  |  Ottiene l'ID tenant associato al motore.
public const std:: String& GetPolicyDataXml () const  |  Ottiene i dati XML dei criteri che descrivono le impostazioni, le etichette e le regole associate a questo criterio.
public const std:: String& GetSensitivityTypesDataXml () const  |  Ottiene i dati XML dei tipi di riservatezza che descrivono i tipi di riservatezza associati a questi criteri.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Ottiene un elenco di impostazioni personalizzate.
public const std:: String& GetPolicyFileId () const  |  Ottiene l'ID del file di criteri.
public const std:: String& GetSensitivityFileId () const  |  Ottiene l'ID del file di riservatezza.
public bool HasClassificationRules () const  |  Ottiene se il criterio ha regole automatiche o di raccomandazione.
public ClassificationScheme GetClassificationScheme () const  |  Ottiene se i criteri devono essere classificati in base alla versione più recente.
public std:: Chrono:: time_point \<std::chrono::system_clock\> GetLastPolicyFetchTime () const  |  Ottiene l'ora dell'ultimo recupero dei criteri.
public uint32_t GetWxpMetadataVersion () const  |  Ottiene la versione dei metadati WXP (Windows, Excel, PowerPoint) consigliata attualmente 0 per versione precedente 1 per la versione abilitata per la creazione di co-creazione.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene Settings del motore dei criteri.

  
**Restituisce**: impostazioni del motore dei criteri. 
  
**Vedere anche**: mip::P olicyengine:: Settings
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Elenca le etichette di riservatezza associate al motore dei criteri.

  
**Restituisce**: elenco di etichette di riservatezza.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
elencare i tipi di riservatezza associati al motore dei criteri.

  
**Restituisce**: elenco di etichette di riservatezza. Empty se LoadSensitivityTypesEnabled è false (
  
**Vedere anche**: PolicyEngine:: Settings.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: URL in formato stringa.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Controlla se il criterio determina che un documento deve essere o meno etichettato.

  
**Restituisce**: true se l'assegnazione di etichette è obbligatoria, in caso contrario false.
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: etichetta di riservatezza predefinita se esistente, nullptr se non è impostata un'etichetta predefinita.
  
### <a name="getlabelbyid-function"></a>GetLabelById (funzione)
Ottiene l'etichetta in base all'ID fornito.
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler (funzione)
Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.

Parametri  
* **R**: bool che indica se l'individuazione del controllo è abilitata o meno.



  
**Restituisce**: gestore dei criteri.
Per la durata del documento, l'applicazione deve contenere l'oggetto gestore dei criteri.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (funzione)
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri  
* **livello**: del livello di registrazione: info/Error/Warning. 


* **eventType**: Descrizione del tipo di evento. 


* **EventData**: i dati associati all'evento.


  
### <a name="gettenantid-function"></a>GetTenantId (funzione)
Ottiene l'ID tenant associato al motore.

  
**Restituisce**: ID tenant
  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml (funzione)
Ottiene i dati XML dei criteri che descrivono le impostazioni, le etichette e le regole associate a questo criterio.

  
**Restituisce**: XML dei dati dei criteri.
  
### <a name="getsensitivitytypesdataxml-function"></a>GetSensitivityTypesDataXml (funzione)
Ottiene i dati XML dei tipi di riservatezza che descrivono i tipi di riservatezza associati a questi criteri.

  
**Restituisce**: dati XML dei tipi di riservatezza.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di impostazioni personalizzate.

  
**Restituisce**: un vettore di impostazioni personalizzate.
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId (funzione)
Ottiene l'ID del file di criteri.

  
**Restituisce**: stringa che rappresenta l'ID del file di criteri
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId (funzione)
Ottiene l'ID del file di riservatezza.

  
**Restituisce**: stringa che rappresenta l'ID del file di criteri
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
Ottiene se il criterio ha regole automatiche o di raccomandazione.

  
**Restituisce** un valore booleano che indica se nel criterio sono presenti regole automatiche o consigliate.
  
### <a name="getclassificationscheme-function"></a>GetClassificationScheme (funzione)
Ottiene se i criteri devono essere classificati in base alla versione più recente.

  
**Restituisce**: un tipo di motore che dirà al cliente quale motore utilizzare
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero dei criteri.

  
**Restituisce**: l'ora dell'ultimo recupero dei criteri
  
### <a name="getwxpmetadataversion-function"></a>GetWxpMetadataVersion (funzione)
Ottiene la versione dei metadati WXP (Windows, Excel, PowerPoint) consigliata attualmente 0 per versione precedente 1 per la versione abilitata per la creazione di co-creazione.

  
**Restituisce**: Uint32_t int indecating quale versione dei metadati supporta il tenant per i file WXP.