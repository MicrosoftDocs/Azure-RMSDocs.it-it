---
title: classe PolicyEngine
description: 'Documenta la classe PolicyEngine:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 10f913029af2be9f0430c55b8296269eb04beb7b
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213437"
---
# <a name="class-policyengine"></a>classe PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottiene Settings del motore dei criteri.
public const std:: Vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels (const std:: Vector \<std::string\>& contentFormats)  |  elenca le etichette di riservatezza associate al motore dei criteri in base al contentFormats fornito.
public const std:: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& ListSensitivityTypes () const  |  elencare i tipi di riservatezza associati al motore dei criteri.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public bool IsLabelingRequired (const std:: String& contentFormat) const  |  Verifica se i criteri stabiliscono che un contenuto deve essere etichettato o meno in base al contentFormat fornito.
public const std:: shared_ptr \<Label\> GetDefaultSensitivityLabel (const std:: string& contentFormat) const  |  Ottiene l'etichetta di riservatezza predefinita in base all'oggetto contentFormat specificato.
public std:: shared_ptr \<Label\> GetLabelById (const std:: string& ID) const  |  Ottiene l'etichetta in base all'ID fornito.
public std:: shared_ptr \<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled, bool isGetSensitivityLabelAuditDiscoveryEnabled)  |  Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
public const std:: String& GetTenantId () const  |  Ottiene l'ID tenant associato al motore.
public const std:: String& GetPolicyDataXml () const  |  Ottiene i dati XML dei criteri che descrivono le impostazioni, le etichette e le regole associate a questo criterio.
public const std:: String& GetSensitivityTypesDataXml () const  |  Ottiene i dati XML dei tipi di riservatezza che descrivono i tipi di riservatezza associati a questi criteri.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Ottiene un elenco di impostazioni personalizzate.
public const std:: String& GetPolicyFileId () const  |  Ottiene l'ID del file di criteri.
public const std:: String& GetSensitivityFileId () const  |  Ottiene l'ID del file di riservatezza.
public bool HasClassificationRules (const std:: Vector \<std::string\>& contentFormats) const  |  Ottiene se il criterio ha regole automatiche o consigliate in base al contentFormats fornito.
public std:: Chrono:: time_point \<std::chrono::system_clock\> GetLastPolicyFetchTime () const  |  Ottiene l'ora dell'ultimo recupero dei criteri.
public uint32_t GetWxpMetadataVersion () const  |  Ottiene la versione dei metadati WXP (Word, Excel, PowerPoint) consigliata, attualmente 0 per la versione precedente di versione 1 per la versione abilitata per la creazione di co-creazione.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottiene Settings del motore dei criteri.

  
**Restituisce**: impostazioni del motore dei criteri. 
  
**Vedere anche**: mip::P olicyengine:: Settings
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
elenca le etichette di riservatezza associate al motore dei criteri in base al contentFormats fornito.

Parametri  
* **contentFormats**: contentFormats Vector of formats per filtrare le etichette di riservatezza, ad esempio "file", "email" e così via. Impostare contentFormats su un vettore vuoto per filtrare le etichette di riservatezza in base ai formati predefiniti.



  
**Restituisce**: elenco di etichette di riservatezza.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
elencare i tipi di riservatezza associati al motore dei criteri.

  
**Restituisce**: elenco di etichette di riservatezza. Empty se LoadSensitivityTypesEnabled è false (
  
**Vedere anche**: PolicyEngine:: Settings.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: URL in formato stringa.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Verifica se i criteri stabiliscono che un contenuto deve essere etichettato o meno in base al contentFormat fornito.

Parametri  
* **contentFormat**: formato in base al quale filtrare quando si determina se un'etichetta è obbligatoria, ad esempio "file", "email" e così via. Impostare contentFormat su una stringa vuota per determinare se è necessaria l'etichettatura per il formato predefinito.



  
**Restituisce**: true se l'assegnazione di etichette è obbligatoria, in caso contrario false.
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza predefinita in base all'oggetto contentFormat specificato.

Parametri  
* **contentFormat**: formato in base al quale filtrare durante il recupero dell'etichetta di riservatezza predefinita, ad esempio "file", "email" e così via. Impostare contentFormat su una stringa vuota per recuperare l'etichetta di riservatezza predefinita per il formato predefinito.



  
**Restituisce**: etichetta di riservatezza predefinita se esistente, nullptr se non è impostata un'etichetta predefinita.
  
### <a name="getlabelbyid-function"></a>GetLabelById (funzione)
Ottiene l'etichetta in base all'ID fornito.

Parametri  
* **ID**: identificatore per l'etichetta.



  
**Restituisce**: etichetta
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler (funzione)
Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.

Parametri  
* **isAuditDiscoveryEnabled**: descrive se l'individuazione del controllo è abilitata o meno.



  
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
Ottiene se il criterio ha regole automatiche o consigliate in base al contentFormats fornito.

Parametri  
* **contentFormat**: vettore di formati da considerare quando si determina se una regola è definita per qualsiasi formato fornito. Imposta contentFormats su un vettore vuoto indica che i contentFormats specificati sono formati predefiniti.



  
**Restituisce** un valore booleano che indica se nel criterio sono presenti regole automatiche o consigliate.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero dei criteri.

  
**Restituisce**: l'ora dell'ultimo recupero dei criteri
  
### <a name="getwxpmetadataversion-function"></a>GetWxpMetadataVersion (funzione)
Ottiene la versione dei metadati WXP (Word, Excel, PowerPoint) consigliata, attualmente 0 per la versione precedente di versione 1 per la versione abilitata per la creazione di co-creazione.

  
**Restituisce**: Uint32_t int indecating quale versione dei metadati supporta il tenant per i file WXP.