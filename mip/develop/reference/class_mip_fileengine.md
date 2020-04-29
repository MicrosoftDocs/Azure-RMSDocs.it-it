---
title: Classe fileengine
description: 'Documents The filemotore:: undefined Class of the Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 03751a2a2c2e1a4457aacf3a28dd4e6ac2436b4a
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763291"
---
# <a name="class-fileengine"></a>Classe fileengine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del motore.
public const std::\<vector std::\<shared_ptr\> \> SensitivityTypesRulePackage& ListSensitivityTypes () const  |  elencare i tipi di riservatezza associati al motore dei criteri.
public const std::\<shared_ptr\> label GetDefaultSensitivityLabel () const  |  Ottiene l'etichetta di riservatezza predefinita.
public std:: shared_ptr\<label\> GetLabelById (const std:: String& ID) const  |  Ottiene l'etichetta in base all'ID fornito.
public const std::\<vector std::\<shared_ptr\> \> label& ListSensitivityLabels ()  |  Restituisce un elenco di etichette di riservatezza.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public const std:: String& GetPolicyFileId () const  |  Ottiene l'ID del file di criteri.
public const std:: String& GetSensitivityFileId () const  |  Ottiene l'ID del file di riservatezza.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere etichettato.
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetLastPolicyFetchTime () const  |  Ottiene l'ora dell'ultimo recupero dei criteri.
public const std:: String& GetPolicyDataXml () const  |  Ottiene i dati XML dei criteri che descrivono le impostazioni, le etichette e le regole associate a questo criterio.
public std:: shared_ptr\<AsyncControl\> CreateFileHandlerAsync (const std:: String& InputFilePath, const std:: String& actualFilePath, bool isAuditDiscoveryEnabled, const std\<:: Shared_ptr filehandler:\> : Observer& fileHandlerObserver, const std\<:\> : shared_ptr void& context, const\<STD\> :: shared_ptr FileExecutionState& FileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato percorso file.
public std:: shared_ptr\<AsyncControl\> CreateFileHandlerAsync (const std::\<shared_ptr\> Stream& inputStream, const std:: String& actualFilePath, bool isAuditDiscoveryEnabled, const std\<:: shared_ptr FileHandler:\> : Observer& fileHandlerObserver, const std\<:\> : shared_ptr void& context, const\<STD\> :: shared_ptr FileExecutionState& FileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato flusso di file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
public const std::\<vector std::p\<Air std:: String, std::\> \> String& GetCustomSettings () const  |  Ottiene un elenco di impostazioni personalizzate.
public bool HasClassificationRules () const  |  Ottiene se il criterio ha regole automatiche o di raccomandazione.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del motore.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
elencare i tipi di riservatezza associati al motore dei criteri.

  
**Restituisce**: elenco di etichette di riservatezza. Empty se LoadSensitivityTypesEnabled è false (
  
**Vedere anche**: [fileengine:: Settings](class_mip_fileengine_settings.md).
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (funzione)
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: etichetta di riservatezza predefinita se esistente, nullptr se non è impostata un'etichetta predefinita.
  
### <a name="getlabelbyid-function"></a>GetLabelById (funzione)
Ottiene l'etichetta in base all'ID fornito.
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Restituisce un elenco di etichette di riservatezza.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: URL in formato stringa.
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId (funzione)
Ottiene l'ID del file di criteri.

  
**Restituisce**: stringa che rappresenta l'ID del file di criteri
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId (funzione)
Ottiene l'ID del file di riservatezza.

  
**Restituisce**: stringa che rappresenta l'ID del file di criteri
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Controlla se il criterio determina che un documento deve essere etichettato.

  
**Restituisce**: true se l'assegnazione di etichette è obbligatoria, in caso contrario false.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (funzione)
Ottiene l'ora dell'ultimo recupero dei criteri.

  
**Restituisce**: l'ora dell'ultimo recupero dei criteri
  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml (funzione)
Ottiene i dati XML dei criteri che descrivono le impostazioni, le etichette e le regole associate a questo criterio.

  
**Restituisce**: XML dei dati dei criteri.
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato percorso file.

Parametri  
* **InputFilePath**: il file da aprire. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **actualFilePath**: il percorso del file effettivo (non temporaneo) verrà usato per il controllo. 


* **isAuditDiscoveryEnabled**: che indica se l'individuazione del controllo è abilitata o meno. 


* **fileHandlerObserver**: classe che implementa l'interfaccia FileHandler::Observer. 


* **context**: contesto client che verrà passato in maniera opaca all'observer. 



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato flusso di file.

Parametri  
* **inputStream**: flusso contenente i dati del file. 


* **actualFilePath**: percorso del file. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. utilizzerà anche per identificare il file in controllo. 


* **isAuditDiscoveryEnabled**: che indica se l'individuazione del controllo è abilitata o meno. 


* **fileHandlerObserver**: classe che implementa l'interfaccia FileHandler::Observer. 


* **context**: contesto client che verrà passato in maniera opaca all'observer. 



  
**Restituisce**: oggetto controllo asincrono.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (funzione)
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri  
* **level**: descrizione del livello di log: info/errore/avviso 


* **eventType**: descrizione del tipo di evento 


* **eventData**: dati associati all'evento


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene un elenco di impostazioni personalizzate.

  
**Restituisce**: un vettore di impostazioni personalizzate
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (funzione)
Ottiene se il criterio ha regole automatiche o di raccomandazione.

  
**Restituisce**un valore booleano che indica se nel criterio sono presenti regole automatiche o consigliate.