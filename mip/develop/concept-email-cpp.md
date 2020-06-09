---
title: "Procedura: elaborare messaggi di posta elettronica tramite l'SDK MIP (C++)"
description: Questo articolo consente di comprendere lo scenario di utilizzo dell'API del file SDK MIP per elaborare i file. msg e. rpmsg.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: 5014367637d2b52256e2d68d3e524bf31286d106
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548276"
---
# <a name="file-api-email-message-file-processing-c"></a>Elaborazione del file di messaggi di posta elettronica dell'API file (C++)

MIP SDK supporta la decrittografia e la crittografia per i messaggi di posta elettronica. Sia i file con estensione msg, generati da Outlook o Exchange, che i file con estensione rpmsg sono supportati dall'SDK, anche se in modo leggermente diverso, in questo scenario verrà illustrata.

Alcuni dei casi d'uso più diffusi per questo scenario sono:

- Decrittografare i messaggi per eDiscovery
- Decrittografare posta e allegati per l'ispezione DLP
- Pubblicare messaggi protetti direttamente da applicazioni line-of-business
- Decrittografare, modificare e riproteggere i messaggi in transito

## <a name="file-api-operations-for-msg-files"></a>Operazioni dell'API file per file con estensione msg

L'API file supporta le operazioni di protezione per i file. msg e in modo identico a qualsiasi altro tipo di file, ad eccezione del fatto che l'SDK richiede l'applicazione per abilitare il flag di funzionalità MSG. Le operazioni di assegnazione di etichette per i file con estensione msg non sono supportate.

Come illustrato in precedenza, la creazione di un'istanza di `mip::FileEngine` richiede un oggetto Setting, `mip::FileEngineSettings` . `mip::FileEngineSettings`può essere usato per passare i parametri per le impostazioni personalizzate che l'applicazione deve impostare per una particolare istanza. La proprietà CustomSettings di FileEngineSettings viene utilizzata per impostare il flag per l' `enable_msg_file_type` Abilitazione dell'elaborazione dei file con estensione msg.

Lo pseudocodice delle operazioni di protezione dei file con estensione msg potrebbe essere simile al seguente:

- Impostare `enable_msg_file_type` flag in `mip::FileEngineSettings` e aggiungere `mip::FileEngine` a `mip::FileProfile` .
- Usare l'API di protezione per elencare i modelli di protezione disponibili per l'utente.
- Costrutto `mip::FileHandler` che punta al file da proteggere.
- Selezionare un modello per proteggere e impostare la protezione per il file usando il `mip::FileHandler` `SetProtection` metodo di.

Guida introduttiva all'API di protezione [: elencare i modelli](quick-protection-list-templates-cpp.md) per informazioni su come elencare i modelli di protezione.

## <a name="file-api-operations-for-rpmsg-files"></a>Operazioni dell'API file per i file. rpmsg

MIP SDK non supporta i messaggi conformi a MIME (comunemente EML). L'SDK, invece, espone una funzione di ispezione in grado di decrittografare il file di **Message. rpmsg** incorporato e presentare un set di flussi di byte come output. Spetta al consumer dell'SDK estrarre il file * Message. rpmsg * (o message_v2, _v3 o v4) e passarlo all'API.

In genere, gateway di posta elettronica e i servizi di prevenzione della perdita dei dati (DLP) gestiscono i messaggi conformi a MIME durante il transito. Quando la posta elettronica è protetta, il contenuto del messaggio viene archiviato in un allegato *Message. rpmsg*. Questo allegati contiene il corpo del messaggio di posta elettronica crittografato e gli eventuali allegati che facevano parte del messaggio originale. Il file *rpmsg* è associato a un messaggio di posta elettronica del wrapper di testo non crittografato e quindi inviato al servizio di posta elettronica. Una volta che il messaggio lascia il limite di Exchange o di Exchange Online, è nel formato conforme a MIME, in modo che possa essere inviato alla relativa destinazione.

Nella maggior parte dei casi, il partner DLP deve essere in grado di ottenere gli allegati e i byte in testo non crittografato dal messaggio per esaminare e valutare i criteri DLP. L'API di ispezione accetta il messaggio. rpmsg come input e restituisce i flussi di byte come output. Questi flussi di byte contengono i byte in testo non crittografato del messaggio e gli allegati. Lo sviluppatore di applicazioni è in grado di gestire questi flussi e di eseguire operazioni utili (ispezionare, decrittografare in modo ricorsivo e così via).

L' `Inspect` API viene implementata tramite una classe `mip::FileInspector` che espone le operazioni per controllare i tipi di file supportati. `mip::MsgInspector`che estende `mip::FileInspector` , espone le operazioni di decrittografia specifiche del formato di file rpmsg. MIP SDK non supporta gli scenari di pubblicazione per i file *Message. rpmsg* .

`mip::MsgInspector`classe espone sotto i membri:

```cpp
public const std::vector<uint8_t>& GetBody()
public BodyType GetBodyType() const
public BodyType GetBodyType() const
public InspectorType GetInspectorType() const
public std::shared_ptr<Stream> GetFileStream() const
```

Per altri dettagli, vedere informazioni di [riferimento sulle API](./reference/mip-sdk-reference.md).

## <a name="next-steps"></a>Passaggi successivi

- Esaminare la [Guida introduttiva all'API file-elabora file con estensione msg (C++)](quick-email-msg-cpp.md)
- Esaminare la [Guida introduttiva all'API file-elabora file con estensione msg (C#)](quick-email-msg-csharp.md)