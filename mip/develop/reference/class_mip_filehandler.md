---
title: Classe mip::FileHandler
description: "Documenta la classe MIP:: FileHandler dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 52c28c1763fc3e7513f98a23a18cb6c91e0ed508
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488739"
---
# <a name="class-mipfilehandler"></a>Classe mip::FileHandler 
Interfaccia per tutte le funzioni di gestione file.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetLabel ()  |  Avvia il recupero dell'etichetta di riservatezza dal file.
public std:: shared_ptr\<ProtectionHandler\> getprotection ()  |  Avvia il recupero dei criteri di protezione dal file.
public void ClassifyAsync (const std:: shared_ptr\<void\>& context)  |  Esegue le regole nel gestore e restituisce l'elenco di azioni da eseguire.
public void InspectAsync (const std:: shared_ptr\<void\>& context)  |  Creare un oggetto Inspector di file, utilizzato per recuperare il contenuto del file da formati di file compatibili.
public void selabel (const std:: shared_ptr\<label\>& Label, const LabelingOptions & labelingOptions, const ProtectionSettings & protectionSettings)  |  Imposta l'etichetta di riservatezza per il file.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Elimina l'etichetta di riservatezza dal file.
public void seprotection (const std:: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor, const ProtectionSettings & protectionSettings)  |  Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
public void seprotection (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler)  |  Imposta la protezione su un documento utilizzando un gestore di protezione esistente.
public void RemoveProtection()  |  Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
public void CommitAsync (const std:: String & outputFilePath, const std:: shared_ptr\<void\>& context) | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\ |  parametro.
public void CommitAsync (const std:: shared_ptr\<Stream\>& outputStream, const std:: shared_ptr\<void\>& context) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\ |  parametro.
bool pubblico ()  |  Verifica se sono presenti modifiche di cui eseguire il commit nel file.
public void GetDecryptedTemporaryFileAsync (const std:: shared_ptr\<void\>& context)  |  Restituisce il percorso di un file temporaneo, che verrà eliminato se possibile, che rappresenta il contenuto decrittografato.
public void GetDecryptedTemporaryStreamAsync (const std:: shared_ptr\<void\>& context)  |  Restituisce un flusso che rappresenta il contenuto decrittografato.
public void NotifyCommitSuccessful (const std:: String & actualFilePath)  |  Da chiamare quando è stato eseguito il commit delle modifiche su disco.
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
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. Il metodo privileged e auto consente all'API di eseguire l'override di qualsiasi etichetta esistente genera JustificationRequiredError quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel (funzione)
Elimina l'etichetta di riservatezza dal file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync. Il metodo privileged e auto consente all'API di eseguire l'override di qualsiasi etichetta esistente genera JustificationRequiredError quando l'impostazione dell'etichetta richiede che l'operazione sia giustificata (tramite il parametro labelingOptions).
  
### <a name="setprotection-function"></a>Funzione seprotection
Imposta autorizzazioni personalizzate o basate su modello (in base a protectionDescriptor->GetProtectionType) per il file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="setprotection-function"></a>Funzione seprotection
Imposta la protezione su un documento utilizzando un gestore di protezione esistente.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="removeprotection-function"></a>RemoveProtection (funzione)
Rimuove la protezione dal file. Se al file è applicata un'etichetta, questa andrà persa.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="commitasync-function"></a>CommitAsync (funzione)
Scrive le modifiche nel file specificato dal parametro |outputFilePath|.
FileHandler:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="commitasync-function"></a>CommitAsync (funzione)
Scrive le modifiche nel flusso specificato dal parametro |outputStream|.
FileHandler:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="ismodified-function"></a>Funzione modified
Verifica se sono presenti modifiche di cui eseguire il commit nel file.
Le modifiche non verranno scritte nel file finché non viene chiamato CommitAsync.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync (funzione)
Restituisce il percorso di un file temporaneo, che verrà eliminato se possibile, che rappresenta il contenuto decrittografato.
FileHandler:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync (funzione)
Restituisce un flusso che rappresenta il contenuto decrittografato.
FileHandler:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful (funzione)
Da chiamare quando è stato eseguito il commit delle modifiche su disco.

Parametri:  
* **actualFilePath**: percorso file effettivo per il file di output 


Genera un evento di controllo
  
### <a name="getoutputfilename-function"></a>GetOutputFileName (funzione)
Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.