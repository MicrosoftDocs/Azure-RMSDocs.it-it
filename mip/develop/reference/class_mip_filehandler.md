---
title: Gestore della classe
description: 'Documents The FileHandler:: undefined Class of the Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: fe04fd0303d5f5717690206760125932826f4708
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763156"
---
# <a name="class-filehandler"></a>Gestore della classe 
Interfaccia per tutte le funzioni di gestione file.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetLabel ()  |  Avvia il recupero dell'etichetta di riservatezza dal file.
public std:: shared_ptr\<ProtectionHandler\> getprotection ()  |  Avvia il recupero dei criteri di protezione dal file.
public void ClassifyAsync (const std::\<shared_ptr\> void& context)  |  Esegue le regole nel gestore e restituisce l'elenco di azioni da eseguire.
public void InspectAsync (const std::\<shared_ptr\> void& context)  |  Creare un oggetto Inspector di file, utilizzato per recuperare il contenuto del file da formati di file compatibili.
public void selabel (const std::\<shared_ptr\> label& Label, const LabelingOptions& LabelingOptions, const ProtectionSettings& ProtectionSettings)  |  Imposta l'etichetta di riservatezza per il file.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Elimina l'etichetta di riservatezza dal file.
public void seprotection (const std::\<shared_ptr\> ProtectionDescriptor& ProtectionDescriptor, const ProtectionSettings& ProtectionSettings)  |  Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
public void seprotection (const std::\<shared_ptr\> ProtectionHandler& ProtectionHandler)  |  Imposta la protezione su un documento utilizzando un gestore di protezione esistente.
public void RemoveProtection()  |  Rimuove la protezione dal file. Se il formato di file originale non supporta l'assegnazione di etichette, l'etichetta andrà persa quando viene rimossa la protezione. Quando il formato nativo supporta l'assegnazione di etichette, i metadati dell'etichetta vengono mantenuti.
public void CommitAsync (const std:: String& outputFilePath, const std:\<:\> shared_ptr void& context) | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\ |  parametri.
public void CommitAsync (const std::\<shared_ptr\> Stream& OutputStream, const std:\<:\> shared_ptr void& context) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\ |  parametri.
bool pubblico ()  |  Verifica se sono presenti modifiche di cui eseguire il commit nel file.
public void GetDecryptedTemporaryFileAsync (const std::\<shared_ptr\> void& context)  |  Restituisce il percorso di un file temporaneo, che verrà eliminato se possibile, che rappresenta il contenuto decrittografato.
public void GetDecryptedTemporaryStreamAsync (const std::\<shared_ptr\> void& context)  |  Restituisce un flusso che rappresenta il contenuto decrittografato.
public void NotifyCommitSuccessful (const std:: String& actualFilePath)  |  Da chiamare quando è stato eseguito il commit delle modifiche su disco.
public std::string GetOutputFileName()  |  Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>Funzione GetLabel
Avvia il recupero dell'etichetta di riservatezza dal file.
  
### <a name="getprotection-function"></a>Funzione getprotection
Avvia il recupero dei criteri di protezione dal file.
  
### <a name="classifyasync-function"></a>ClassifyAsync (funzione)
Esegue le regole nel gestore e restituisce l'elenco di azioni da eseguire.

  
**Restituisce**: elenco di azioni da applicare al contenuto.
  
### <a name="inspectasync-function"></a>InspectAsync (funzione)
Creare un oggetto Inspector di file, utilizzato per recuperare il contenuto del file da formati di file compatibili.

  
**Restituisce**: controllo file.
  
### <a name="setlabel-function"></a>Funzione di etichetta
Imposta l'etichetta di riservatezza per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera [JustificationRequiredError](class_mip_justificationrequirederror.md) quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel (funzione)
Elimina l'etichetta di riservatezza dal file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. I metodi Auto e Privileged consentono all'API di eseguire l'override di qualsiasi etichetta esistente. Genera JustificationRequiredError quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="setprotection-function"></a>Funzione seprotection
Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="setprotection-function"></a>Funzione seprotection
Imposta la protezione su un documento utilizzando un gestore di protezione esistente.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="removeprotection-function"></a>RemoveProtection (funzione)
Rimuove la protezione dal file. Se il formato di file originale non supporta l'assegnazione di etichette, l'etichetta andrà persa quando viene rimossa la protezione. Quando il formato nativo supporta l'assegnazione di etichette, i metadati dell'etichetta vengono mantenuti.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="commitasync-function"></a>CommitAsync (funzione)
Scrive le modifiche nel file specificato dal parametro |outputFilePath|.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileHandler::Observer.
  
### <a name="commitasync-function"></a>CommitAsync (funzione)
Scrive le modifiche nel flusso specificato dal parametro |outputStream|.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileHandler::Observer.
  
### <a name="ismodified-function"></a>Funzione modified
Verifica se sono presenti modifiche di cui eseguire il commit nel file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync (funzione)
Restituisce il percorso di un file temporaneo, che verrà eliminato se possibile, che rappresenta il contenuto decrittografato.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileHandler::Observer.
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync (funzione)
Restituisce un flusso che rappresenta il contenuto decrittografato.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileHandler::Observer.
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful (funzione)
Da chiamare quando è stato eseguito il commit delle modifiche su disco.

Parametri  
* **actualFilePath**: percorso file effettivo per il file di output 


Genera un evento di controllo
  
### <a name="getoutputfilename-function"></a>GetOutputFileName (funzione)
Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.