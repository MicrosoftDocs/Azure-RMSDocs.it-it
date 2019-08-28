---
title: Classe mip::FileEngine
description: "Documenta la classe MIP:: fileengine dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d19751e9da113be2cea94d7b169be29026813da8
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056123"
---
# <a name="class-mipfileengine"></a>Classe mip::FileEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del motore.
public const std::\<vector std::\<shared_ptr\>SensitivityTypesRulePackage\>& ListSensitivityTypes () const  |  elencare i tipi di riservatezza associati al motore dei criteri.
public const std::\<shared_ptr\> label GetDefaultSensitivityLabel () const  |  Ottiene l'etichetta di riservatezza predefinita.
public std:: shared_ptr\<label\> GetLabelById (const std:: String & ID) const  |  Ottiene l'etichetta in base all'ID fornito.
public const std::\<vector std::\<shared_ptr\>label\>& ListSensitivityLabels ()  |  Restituisce un elenco di etichette di riservatezza.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public const std:: String & GetPolicyFileId () const  |  Ottiene l'ID del file di criteri.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere etichettato.
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetLastPolicyFetchTime () const  |  Ottiene l'ora dell'ultimo recupero dei criteri.
public void CreateFileHandlerAsync (const std:: String & InputFilePath, const std:: String & actualFilePath, bool isAuditDiscoveryEnabled, const std\<:: shared_ptr FileHandler:\>: Observer & fileHandlerObserver , const std::\<shared_ptr\>void & context, const std:\<:\>shared_ptr FileExecutionState & FileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato percorso file.
public void CreateFileHandlerAsync (const std::\<shared_ptr\>Stream & InputStream, const std:: String & actualFilePath, bool isAuditDiscoveryEnabled, const std\<:: shared_ptr FileHandler:: Observer \>\<\>\<& fileHandlerObserver, const std:: shared_ptr void & context, const std:: shared_ptr FileExecutionState & FileExecutionState) \>  |  Avvia la creazione di un gestore di file per un determinato flusso di file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
public const std::\<vector std::p\<Air std:: String, std::\>String\>& GetCustomSettings () const  |  Ottiene un elenco di impostazioni personalizzate.
public bool HasClassificationRules () const  |  Ottiene se il criterio ha regole automatiche o di raccomandazione.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del motore.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
elencare i tipi di riservatezza associati al motore dei criteri.

  
**Restituisce**: Elenco di etichette di riservatezza. Empty se LoadSensitivityTypesEnabled è false (
  
**Vedere anche**: [Fileengine:: Settings](class_mip_fileengine_settings.md)).
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: Etichetta di riservatezza predefinita se esistente, nullptr se non è impostata alcuna etichetta predefinita.
  
### <a name="getlabelbyid-function"></a>GetLabelById (funzione)
Ottiene l'etichetta in base all'ID fornito.
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Restituisce un elenco di etichette di riservatezza.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: Un URL in formato stringa.
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId (funzione)
Ottiene l'ID del file di criteri.

  
**Restituisce**: Stringa che rappresenta l'ID del file di criteri
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Controlla se il criterio determina che un documento deve essere etichettato.

  
**Restituisce**: True se l'assegnazione di etichette è obbligatoria; in caso contrario, false.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero dei criteri.

  
**Restituisce**: Ora dell'ultimo recupero dei criteri
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato percorso file.

Parametri:  
* **inputFilePath**: File da aprire. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **actualFilePath**: Il percorso del file effettivo (non temporaneo) verrà usato per il controllo. 


* **isAuditDiscoveryEnabled**: che indica se l'individuazione del controllo è abilitata o meno. 


* **fileHandlerObserver**: Classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contesto client che verrà passato di nuovo in modo opaco all'osservatore.


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato flusso di file.

Parametri:  
* **inputStream**: Flusso contenente i dati del file. 


* **actualFilePath**: Percorso del file. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. utilizzerà anche per identificare il file in controllo. 


* **isAuditDiscoveryEnabled**: che indica se l'individuazione del controllo è abilitata o meno. 


* **fileHandlerObserver**: Classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contesto client che verrà passato di nuovo in modo opaco all'osservatore.


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (funzione)
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri:  
* **Level**: Descrizione del livello di registrazione: Informazioni/errore/avviso 


* **eventType**: descrizione del tipo di evento 


* **eventData**: dati associati all'evento


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di impostazioni personalizzate.

  
**Restituisce**: Vettore di impostazioni personalizzate
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
Ottiene se il criterio ha regole automatiche o di raccomandazione.

  
**Restituisce**: Bool che indica se sono presenti regole automatiche o di raccomandazione nei criteri