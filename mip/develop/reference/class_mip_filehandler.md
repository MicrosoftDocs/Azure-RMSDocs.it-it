---
title: Classe mip FileHandler
description: Riferimento per la classe mip FileHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: efae18bdc10f8878f255f35c608a50482a29887b
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446125"
---
# <a name="class-mipfilehandler"></a>Classe mip::FileHandler 
Interfaccia per tutte le funzioni di gestione file.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  Avvia il recupero dell'etichetta di riservatezza dal file.
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  Avvia il recupero dei criteri di protezione dal file.
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Imposta l'etichetta di riservatezza per il file.
 public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Elimina l'etichetta di riservatezza dal file.
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
 public void RemoveProtection()  |  Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\ |  .
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\ |  .
 public void NotifyCommitSuccessful(const std::string& contentIdentifier)  |  Da chiamare quando è stato eseguito il commit delle modifiche su disco.
 public std::string GetOutputFileName()  |  Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
  
## <a name="members"></a>Membri
  
### <a name="getlabelasync"></a>GetLabelAsync
Avvia il recupero dell'etichetta di riservatezza dal file.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).

Parametri:  
* **context**: contesto client che verrà passato in maniera opaca all'observer.


  
### <a name="getprotectionasync"></a>GetProtectionAsync
Avvia il recupero dei criteri di protezione dal file.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).

Parametri:  
* **context**: contesto client che verrà passato in maniera opaca all'observer.


  
### <a name="setlabel"></a>SetLabel
Imposta l'etichetta di riservatezza per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="deletelabel"></a>DeleteLabel
Elimina l'etichetta di riservatezza dal file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="setprotection"></a>SetProtection
Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="removeprotection"></a>RemoveProtection
Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="commitasync"></a>CommitAsync
Scrive le modifiche nel file specificato dal parametro |outputFilePath|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="commitasync"></a>CommitAsync
Scrive le modifiche nel flusso specificato dal parametro |outputStream|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="notifycommitsuccessful"></a>NotifyCommitSuccessful
Da chiamare quando è stato eseguito il commit delle modifiche su disco.

Parametri:  
* **contentIdentifier**: esempio per un file: "C:\mip-sdk-for-cpp\files\audit.docx" [path] esempio per un messaggio di posta elettronica: "RE: Audit design:user1@contoso.com" [Subject:Sender] 


Genera un evento di controllo
  
### <a name="getoutputfilename"></a>GetOutputFileName
Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.