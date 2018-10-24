---
title: Classe mip FileEngine
description: Riferimento per la classe mip FileEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7342edf27b19f43881b2e8d378fa243d26f7056
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446074"
---
# <a name="class-mipfileengine"></a>Classe mip::FileEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Restituisce le impostazioni del motore.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Restituisce un elenco di etichette di riservatezza.
 public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
 public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere etichettato.
public void CreateFileHandlerAsync(const std::string& inputFilePath, const ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Avvia la creazione di un gestore di file per un determinato percorso file.
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFilePath, const mip::ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Avvia la creazione di un gestore di file per un determinato flusso di file.
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Restituisce le impostazioni del motore.
  
### <a name="label"></a>Label
Restituisce un elenco di etichette di riservatezza.
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: URL in formato stringa.
  
### <a name="islabelingrequired"></a>IsLabelingRequired
Controlla se il criterio determina che un documento deve essere etichettato.

  
**Restituisce**: true se l'assegnazione di etichette è obbligatoria, in caso contrario false.
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Avvia la creazione di un gestore di file per un determinato percorso file.

Parametri:  
* **The**: file da aprire. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **contentState**: stato del contenuto mentre l'applicazione interagisce con esso. 


* **A**: classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: contesto client che verrà passato in maniera opaca all'observer.


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Avvia la creazione di un gestore di file per un determinato flusso di file.

Parametri:  
* **inputStream**: flusso contenente i dati del file. 


* **inputFilePath**: percorso del file. Il percorso deve includere il nome del file e, se ne esiste uno, l'estensione del nome di file. 


* **contentState**: stato del contenuto mentre l'applicazione interagisce con esso. 


* **fileHandlerObserver**: classe che implementa l'interfaccia [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: contesto client che verrà passato in maniera opaca all'observer.


  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri:  
* **level**: descrizione del livello di log: info/errore/avviso 


* **eventType**: descrizione del tipo di evento 


* **eventData**: dati associati all'evento

