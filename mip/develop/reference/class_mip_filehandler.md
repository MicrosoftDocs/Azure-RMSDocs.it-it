---
title: Classe mip::FileHandler
description: 'Classe MIP:: FileHandler di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ee0545346eef2c143946496f56af77b7081b1e06
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184655"
---
# <a name="class-mipfilehandler"></a>Classe mip::FileHandler 
Interfaccia per tutte le funzioni di gestione file.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<ContentLabel\> GetLabel()  |  Avvia il recupero dell'etichetta di riservatezza dal file.
Public std:: shared_ptr\<ProtectionHandler\> GetProtection()  |  Avvia il recupero dei criteri di protezione dal file.
public void ClassifyAsync (const std:: shared_ptr\<void\>& contesto)  |  Esegue le regole nel gestore e restituisce l'elenco di azioni da eseguire.
public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Imposta l'etichetta di riservatezza per il file.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Elimina l'etichetta di riservatezza dal file.
public void SetProtection (const std:: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor)  |  Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
public void SetProtection (const std:: Vector\<uint8_t\>& serializedPublishingLicense, const std:: Vector\<uint8_t\>& serializedProtectionInfo)  |  Imposta le autorizzazioni personalizzate o basate su modello (in base a serializedPublishingLicense e serializedProtectionInfo) del file.
public void RemoveProtection()  |  Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
public void CommitAsync (const std:: String & outputFilePath, const std:: shared_ptr\<void\>& contesto) | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\ |  .
public void CommitAsync (const std:: shared_ptr\<Stream\>& outputStream, const std:: shared_ptr\<void\>& contesto) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\ |  .
public void GetDecryptedTemporaryFileAsync (const std:: shared_ptr\<void\>& contesto)  |  Restituisce un percorso in un file temporaneo (che verrà eliminato se possibile), che rappresenta il contenuto decrittografato.
public void NotifyCommitSuccessful (const std:: String & actualFilePath)  |  Da chiamare quando è stato eseguito il commit delle modifiche su disco.
public std::string GetOutputFileName()  |  Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
  
## <a name="members"></a>Membri
  
### <a name="getlabel-function"></a>GetLabel (funzione)
Avvia il recupero dell'etichetta di riservatezza dal file.
  
### <a name="getprotection-function"></a>GetProtection (funzione)
Avvia il recupero dei criteri di protezione dal file.
  
### <a name="classifyasync-function"></a>ClassifyAsync (funzione)
Esegue le regole nel gestore e restituisce l'elenco di azioni da eseguire.

  
**Restituisce**: Elenco di azioni da applicare al contenuto.
  
### <a name="setlabel-function"></a>SetLabel (funzione)
Imposta l'etichetta di riservatezza per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel (funzione)
Elimina l'etichetta di riservatezza dal file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="setprotection-function"></a>SetProtection (funzione)
Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="setprotection-function"></a>SetProtection (funzione)
Imposta le autorizzazioni personalizzate o basate su modello (in base a serializedPublishingLicense e serializedProtectionInfo) del file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="removeprotection-function"></a>RemoveProtection (funzione)
Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="commitasync-function"></a>CommitAsync (funzione)
Scrive le modifiche nel file specificato dal parametro |outputFilePath|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="commitasync-function"></a>CommitAsync (funzione)
Scrive le modifiche nel flusso specificato dal parametro |outputStream|.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync function
Restituisce un percorso in un file temporaneo (che verrà eliminato se possibile), che rappresenta il contenuto decrittografato.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileHandler::Observer](class_mip_filehandler_observer.md).
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful (funzione)
Da chiamare quando è stato eseguito il commit delle modifiche su disco.

Parametri:  
* **actualFilePath**: Il percorso effettivo del file di output 


Genera un evento di controllo
  
### <a name="getoutputfilename-function"></a>GetOutputFileName (funzione)
Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.