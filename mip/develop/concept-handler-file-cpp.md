---
title: Concetti - Gestori di file in MIP SDK.
description: Questo articolo illustra le modalità di creazione e uso dei gestori dell'API File per la chiamata di operazioni.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 7e436d27ae48ee6d3589faaf55943b8ffd314450
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175977"
---
# <a name="microsoft-information-protection-sdk---file-handler-concepts"></a>Microsoft Information Protection SDK - Concetti relativi ai gestori di file

Nell'API File di MIP SDK, `mip::FileHandler` espone tutte le varie operazioni che possono essere usate per leggere e scrivere le etichette, o la protezione, in un set di tipi di file supportati per impostazione predefinita. 

## <a name="supported-file-types"></a>Tipi di file supportati

- Formati di file di Office basati su OCP (Office 2010 e versioni successive)
- Formati di file di Office legacy (Office 2007)
- PDF
- Supporto PFILE generico
- File che supportano Adobe XMP

## <a name="file-handler-functions"></a>Funzioni di gestione file

`mip::FileHandler` espone i metodi per la lettura, scrittura e rimozione sia delle etichette che delle informazioni sulla protezione. Per un elenco completo, vedere le [informazioni di riferimento sull'API](reference/class_mip_filehandler.md).

In questo articolo verranno descritti i metodi seguenti:

- `GetLabelAsync()`
- `SetLabel()`
- `DeleteLabel()`
- `CommitAsync()`

## <a name="requirements"></a>Requisiti

Per creare un `FileHandler` per lavorare con un file specifico esistono questi requisiti:

- Un elemento `FileProfile`
- Un elemento `FileEngine` aggiunto a `FileProfile`
- Una classe che eredita `mip::FileHandler::Observer`

## <a name="create-a-file-handler"></a>Creare un gestore di file

Il primo passaggio necessario per la gestione di qualsiasi file nell'API File consiste nel creare un oggetto `FileHandler`. Questa classe implementa tutte le funzionalità necessarie per ottenere, impostare, aggiornare, eliminare ed eseguire il commit delle modifiche alle etichette nei file.

Per creare `FileHandler` è sufficiente chiamare la funzione `CreateFileHandlerAsync` di `FileEngine` usando il modello promise/future.

`CreateFileHandlerAsync` accetta tre parametri: Il percorso del file che deve essere letto o modificato, il `mip::FileHandler::Observer` per le notifiche degli eventi asincroni e il suggerimento per il `FileHandler`.

**Nota:** La classe `mip::FileHandler::Observer` deve essere implementata in una classe derivata perché `CreateFileHandler` richiede l'oggetto `Observer`. 

```cpp
auto createFileHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::FileHandler>>>();
auto createFileHandlerFuture = createFileHandlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, std::make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = createFileHandlerFuture.get();
```

Dopo la creazione corretta dell'oggetto `FileHandler` è possibile eseguire operazioni sui file (recupero/impostazione/eliminazione/commit).

## <a name="read-a-label"></a>Leggere un'etichetta

### <a name="metadata-requirements"></a>Requisiti per i metadati

Esistono alcuni requisiti per leggere correttamente i metadati da un file e convertirli in informazioni utilizzabili nelle applicazioni.

- L'etichetta letta deve esistere ancora nel servizio Office 365. Se è stata eliminata completamente, l'SDK non riuscirà a ottenere informazioni su tale etichetta e restituirà un errore.
- I metadati dei file devono essere intatti. Questi metadati includono:
  - Attribute1
  - Attribute2

### <a name="getlabelasync"></a>GetLabelAsync()

Dopo aver creato il gestore in modo che punti a un file specifico, si torna a usare il modello promise/future per leggere l'etichetta in modo asincrono. La promessa è per un oggetto `mip::ContentLabel` che contiene tutte le informazioni sull'etichetta applicata.

Dopo la creazione di un'istanza degli oggetti `promise` e `future`, l'etichetta viene letta chiamando `handler->GetLabelAsync()` e specificando `promise` come unico parametro. Infine, l'etichetta può essere archiviata in un oggetto `mip::ContentLabel` che verrà recuperato da `future`.

```cpp
auto loadPromise = std::make_shared<std::promise<std::shared_ptr<mip::ContentLabel>>>();
auto loadFuture = loadPromise->get_future();
handler->GetLabelAsync(loadPromise);
auto label = loadFuture.get();
```

I dati dell'etichetta possono essere letti dall'oggetto `label` e passati a qualsiasi altro componente o funzionalità nell'applicazione.

***

## <a name="set-a-label"></a>Impostare un'etichetta

L'impostazione di un'etichetta è un processo costituito da due parti. In primo luogo, avendo creato un gestore che punta al file in questione, è possibile impostare l'etichetta chiamando `FileHandler->SetLabel()` con un paio di parametri.

```cpp
handler->SetLabel(label->GetId(), mip::LabelingOptions{ mip::AssignmentMethod::PRIVILEGED, "" });
```

Il primo parametro è semplicemente l'identificatore di etichetta ottenuto da `ListLabelsAsync()`. Questo valore può essere archiviato in una variabile dedicata o leggendo `mip::Label->GetId()`.

Nell'esempio precedente si presuppone che il valore desiderato `mip::Label` sia stato archiviato in un oggetto denominato `label`.

### <a name="labeling-options"></a>Opzioni di etichettatura

Il secondo parametro necessario per impostare l'etichetta è un oggetto `mip::LabelingOptions` creato inline durante la chiamata della funzione `SetLabel()`. Potrebbe anche essere creato anticipatamente.

`LabelingOptions` specifica informazioni aggiuntive sull'etichetta, ad esempio `AssignmentMethod` e la giustificazione per un'azione.

- `mip::AssignmentMethod` è semplicemente un enumeratore con tre valori: `STANDARD`, `PRIVILEGED` o `AUTO`. Per altri dettagli, vedere le informazioni di riferimento per `mip::AssignmentMethod`.
- La giustificazione è obbligatoria solo se richiesta dai criteri di servizio *e* per l'abbassamento del livello di riservatezza *esistente* di un file.

```cpp
auto labelingOptions = mip::LabelingOptions();
labelingOptions.SetMethod(mip::AssignmentMethod::STANDARD);
labelingOptions.SetJustificationMessage("Because I made an educated decision based upon the contents of this file.");
```

A questo punto, invece di creare le opzioni di etichettatura inline, è possibile passarle nella funzione `SetLabel()`.

```cpp
handler->SetLabel(label->GetId(), labelingOptions);
```

Dopo aver impostato l'etichetta per il file a cui fa riferimento il gestore, è necessario un altro passaggio per il commit della modifica e per scrivere un file su disco o creare un flusso di output.

### <a name="commit-changes"></a>Eseguire il commit delle modifiche

Il passaggio finale per confermare qualsiasi modifica apportata a un file in MIP SDK consiste nell'eseguirne il **commit**. Questa operazione viene eseguita con la funzione `FileHandler->CommitAsync()`. 

Per implementare la funzione di commit, si ritorna al modello promise/future creando una promessa per un `bool`. La funzione `CommitAsync()` restituirà true se l'operazione ha esito positivo o false se ha esito negativo per qualsiasi motivo. 

Dopo aver creato il `promise` e `future`, `CommitAsync()` viene chiamato e due i parametri specificati: Il percorso di file di output (`std::string`) e il suggerimento. Infine, il risultato viene ottenuto recuperando il valore dell'oggetto `future`.

```cpp
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
auto wasCommitted = commitFuture.get();
```

**Importante:** Il `FileHandler` non verranno aggiornati o sovrascrivere i file esistenti. Spetta allo sviluppatore implementare la **sostituzione** del file in corso di etichettatura. 

Se si scrive un'etichetta in **FileA.docx**, verrà creata una copia del file, **FileB.docx**, con l'etichetta applicata. È necessario scrivere codice per rimuovere/rinominare **FileA.docx** e rinominare **FileB.docx**.

***

## <a name="delete-a-label"></a>Eliminare un'etichetta

```cpp
auto handler = mEngine->CreateFileHandler(filePath, std::make_shared<FileHandlerObserverImpl>());
handler->DeleteLabel(mip::AssignmentMethod::PRIVILEGED, "Label unnecessary.");
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
```
