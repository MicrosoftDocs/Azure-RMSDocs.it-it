---
title: Classe mip::FileHandler
description: "Documenta la classe MIP:: FileHandler dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: b2a6e3cd6de886c3e3983442a1ec7185b688b662
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558829"
---
# <a name="class-mipfilehandler"></a>Classe mip::FileHandler 
Interfaccia per tutte le funzioni di gestione file.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
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
public void CommitAsync (const std:: String & outputFilePath, const std:: shared_ptr\<void\>& context) | Scrive le modifiche nel file specificato dal parametro \|outputFilePath\ |  .
public void CommitAsync (const std:: shared_ptr\<Stream\>& outputStream, const std:: shared_ptr\<void\>& context) | Scrive le modifiche nel flusso specificato dal parametro \|outputStream\ |  .
bool pubblico ()  |  Verifica se sono presenti modifiche di cui eseguire il commit nel file.
public void GetDecryptedTemporaryFileAsync (const std:: shared_ptr\<void\>& context)  |  Restituisce il percorso di un file temporaneo, che verrà eliminato se possibile, che rappresenta il contenuto decrittografato.
public void GetDecryptedTemporaryStreamAsync (const std:: shared_ptr\<void\>& context)  |  Restituisce un flusso che rappresenta il contenuto decrittografato.
public void NotifyCommitSuccessful (const std:: String & actualFilePath)  |  Da chiamare quando è stato eseguito il commit delle modifiche su disco.
public std::string GetOutputFileName()  |  Calcola il nome e l'estensione del file di output in base al nome file originale e alle modifiche accumulate.
public static bool protected (const std:: String & filePath, const std:: shared_ptr<MipContext>& mipContext) | Verifica se un file è protetto o meno.
public static FILE_API std:: Vector&lt;uint8_t&gt; __CDECL MIP:: FileHandler:: GetSerializedPublishingLicense | Restituisce la licenza di pubblicazione se il file è presente.

## <a name="members"></a>Membri
  
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

### <a name="isprotected-function"></a>Funzione Protected
Verifica se un file è protetto o meno.

### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense (funzione)
Restituisce la licenza di pubblicazione se il file è presente.