---
title: Classe mip::PolicyEngine
description: Documenta la classe MIP::p olicyengine dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a1938601e036f7fb4d84a9a5815016dbda4509b7
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558513"
---
# <a name="class-mippolicyengine"></a>Classe mip::PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Ottenere le impostazioni del motore dei criteri.
public const std:: Vector\<std:: shared_ptr\<label\>\>& ListSensitivityLabels ()  |  Elenca le etichette di riservatezza associate al motore dei criteri.
public const std:: Vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  elencare i tipi di riservatezza associati al motore dei criteri.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere o meno etichettato.
public std:: shared_ptr\<label\> GetDefaultSensitivityLabel ()  |  Ottiene l'etichetta di riservatezza predefinita.
public std:: shared_ptr\<label\> GetLabelById (const std:: String & ID) const  |  Ottiene l'etichetta in base all'ID fornito.
public std:: shared_ptr\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
public const std:: String & GetPolicyDataXml () const  |  Ottiene i dati XML dei criteri che descrivono le impostazioni, le etichette e le regole associate a questo criterio.
public const std:: String & GetSensitivityTypesDataXml () const  |  Ottiene i dati XML dei tipi di riservatezza che descrivono i tipi di riservatezza associati a questi criteri.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetCustomSettings () const  |  Ottiene un elenco di impostazioni personalizzate.
public const std:: String & GetPolicyFileId () const  |  Ottiene l'ID del file di criteri.
public const std:: String & GetSensitivityFileId () const  |  Ottiene l'ID del file di riservatezza.
public bool HasClassificationRules () const  |  Ottiene se il criterio ha regole automatiche o di raccomandazione.
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetLastPolicyFetchTime () const  |  Ottiene l'ora dell'ultimo recupero dei criteri.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Ottenere le impostazioni del motore dei criteri.

  
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

Parametri:  
* **R**: bool che indica se l'individuazione del controllo è abilitata o meno.



  
**Restituisce**: gestore dei criteri.
Per la durata del documento, l'applicazione deve contenere l'oggetto gestore dei criteri.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (funzione)
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri:  
* **livello**: del livello di registrazione: info/Error/Warning. 


* **eventType**: Descrizione del tipo di evento. 


* **EventData**: i dati associati all'evento.


  
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

  
**Restituisce**un valore booleano che indica se nel criterio sono presenti regole automatiche o consigliate.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero dei criteri.

  
**Restituisce**: l'ora dell'ultimo recupero dei criteri