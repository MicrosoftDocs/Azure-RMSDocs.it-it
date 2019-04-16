---
title: Classe mip::FileEngine
description: 'Classe MIP:: fileengine di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 15ce90a80430f50854580f6c7a2993d92db0a744
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573990"
---
# <a name="class-mipfileengine"></a>Classe mip::FileEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del motore.
Public std:: Vector const\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Elenca i tipi di riservatezza associati al motore di criteri.
Public std:: shared_ptr const\<etichetta\> GetDefaultSensitivityLabel() const  |  Ottiene l'etichetta di riservatezza predefinita.
Public std:: Vector const\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Restituisce un elenco di etichette di riservatezza.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
Public std:: String const & GetPolicyId() const  |  Ottiene l'ID criteri.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere etichettato.
pubblica std::chrono::time_point\<std\> GetLastPolicyFetchTime() const  |  Ottiene l'ora dell'ultimo recupero quando il criterio.
public void CreateFileHandlerAsync (const std:: String & inputFilePath, const std:: String & actualFilePath, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<FileHandler:: Observer\>& fileHandlerObserver const std:: shared_ptr\<void\>& context, const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato percorso file.
public void CreateFileHandlerAsync (const std:: shared_ptr\<Stream\>& inputStream, const std:: String & actualFilePath, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<FileHandler:: Observer \>& fileHandlerObserver, const std:: shared_ptr\<void\>& context, const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato flusso di file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene un elenco di impostazioni personalizzate.
public bool HasClassificationRules() const  |  Ottiene se il criterio ha regole automatico o raccomandazione.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del motore.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
Elenca i tipi di riservatezza associati al motore di criteri.

  
**Restituisce**: Un elenco di etichette di riservatezza. vuoto se LoadSensitivityTypesEnabled era (false
  
**Vedere anche**: [FileEngine::Settings](class_mip_fileengine_settings.md)).
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: Etichetta di riservatezza predefinita se esistente, nullptr se è presente alcun set di etichetta predefinita.
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Restituisce un elenco di etichette di riservatezza.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: Un url in formato stringa.
  
### <a name="getpolicyid-function"></a>GetPolicyId (funzione)
Ottiene l'ID criteri.

  
**Restituisce**: Stringa che rappresenta l'ID dei criteri
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Controlla se il criterio determina che un documento deve essere etichettato.

  
**Restituisce**: True se l'assegnazione di etichette è obbligatorio, altrimenti false.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero quando il criterio.

  
**Restituisce**: L'ora dell'ultimo recupero quando il criterio
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato percorso file.

Parametri:  
* **inputFilePath**: File da aprire. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **actualFilePath**: Il percorso del file (non temporanee) effettivo, verrà usato per il controllo. 


* **isAuditDiscoveryEnabled**: che indica se il rilevamento di controllo è abilitato o meno. 


* **fileHandlerObserver**: Classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contesto di client che verrà passato in maniera opaca all'observer.


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato flusso di file.

Parametri:  
* **inputStream**: Flusso contenente i dati del file. 


* **actualFilePath**: Percorso del file. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. userà anche per identificare il file nel controllo. 


* **isAuditDiscoveryEnabled**: che indica se il rilevamento di controllo è abilitato o meno. 


* **fileHandlerObserver**: Classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contesto di client che verrà passato in maniera opaca all'observer.


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (funzione)
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri:  
* **livello**: una descrizione del livello di log: Info/errore/avviso 


* **eventType**: descrizione del tipo di evento 


* **eventData**: dati associati all'evento


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di impostazioni personalizzate.

  
**Restituisce**: Un vettore di impostazioni personalizzate
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
Ottiene se il criterio ha regole automatico o raccomandazione.

  
**Restituisce**: Un valore booleano che indica se esiste qualsiasi automatico o recommandation regole nel criterio