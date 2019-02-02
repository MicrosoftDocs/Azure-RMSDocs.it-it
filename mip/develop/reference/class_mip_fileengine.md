---
title: Classe mip::FileEngine
description: 'Classe MIP:: fileengine di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4bcdd08cb7ced9e2eea8fa09d9364064a8d198df
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651463"
---
# <a name="class-mipfileengine"></a>Classe mip::FileEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del motore.
Public std:: Vector const\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Elenca i tipi di riservatezza associati al motore di criteri.
Public std:: Vector const\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Restituisce un elenco di etichette di riservatezza.
public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere etichettato.
public void CreateFileHandlerAsync (const std:: String & inputFilePath, const isAuditDiscoveryEnabled di std:: String & contentIdentifier, const ContentState contentState, bool, const std:: shared_ptr\<FileHandler::Observer\>& fileHandlerObserver, const std:: shared_ptr\<void\>& context, const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato percorso file.
public void CreateFileHandlerAsync (const std:: shared_ptr\<Stream\>& inputStream, const std:: String & inputFilePath, const std:: String & contentIdentifier, const mip::ContentState contentState, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<FileHandler:: Observer\>& fileHandlerObserver, const std:: shared_ptr\<void\>& context, const std:: shared_ptr\< FileExecutionState\>& fileExecutionState)  |  Avvia la creazione di un gestore di file per un determinato flusso di file.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene un elenco di impostazioni personalizzate.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del motore.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (funzione)
Elenca i tipi di riservatezza associati al motore di criteri.

  
**Restituisce**: Un elenco di etichette di riservatezza. vuoto se LoadSensitivityTypesEnabled era (false
  
**Vedere anche**: [FileEngine::Settings](class_mip_fileengine_settings.md)).
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (funzione)
Restituisce un elenco di etichette di riservatezza.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (funzione)
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: Un url in formato stringa.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (funzione)
Controlla se il criterio determina che un documento deve essere etichettato.

  
**Restituisce**: True se l'assegnazione di etichette è obbligatorio, altrimenti false.
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato percorso file.

Parametri:  
* **inputFilePath**: File da aprire. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **contentIdentifier**: un identificatore leggibile dall'utente per il contenuto. esempio di un file: Esempio di "C:\mip-sdk-for-cpp\files\audit.docx" [percorso\nomefile] per un messaggio di posta elettronica: "RE: Controllo design:user1@contoso.com"[soggetto: mittente] 


* **contentState**: Lo stato del contenuto durante l'applicazione interagisce con esso. 


* **isAuditDiscoveryEnabled**: che indica se il rilevamento di controllo è abilitato o meno. 


* **fileHandlerObserver**: Classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contesto di client che verrà passato in maniera opaca all'observer.


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (funzione)
Avvia la creazione di un gestore di file per un determinato flusso di file.

Parametri:  
* **inputStream**: Flusso contenente i dati del file. 


* **inputFilePath**: Percorso del file. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **contentIdentifier**: un identificatore leggibile dall'utente per il contenuto. esempio di un file: Esempio di "C:\mip-sdk-for-cpp\files\audit.docx" [percorso\nomefile] per un messaggio di posta elettronica: "RE: Controllo design:user1@contoso.com"[soggetto: mittente] 


* **contentState**: Lo stato del contenuto durante l'applicazione interagisce con esso. 


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