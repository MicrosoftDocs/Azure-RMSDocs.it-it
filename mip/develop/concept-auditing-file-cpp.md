---
title: "Concetti: il controllo nell'API File di Microsoft Information Protection SDK"
description: Questo articolo aiuta a comprendere in che modo usare Microsoft Information Protection SDK per inviare gli eventi di controllo dell'API File all'analitica di Azure Information Protection.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: df0d51d976f7f900011688d2f328f3a2ddb1e378
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60176925"
---
# <a name="auditing-in-the-mip-sdk-file-api"></a>Controllo nell'API File di MIP SDK

Nel portale di amministrazione di Azure Information Protection è possibile accedere ai report di amministratore. Questi report offrono la visibilità sulle etichette che gli utenti stanno applicando, manualmente o automaticamente, in tutte le applicazioni e servizi in cui è integrato MIP SDK. I partner di sviluppo che usano l'SDK possono abilitare facilmente questa funzionalità per presentare nei report dei clienti le informazioni contenute nelle proprie applicazioni.

## <a name="event-types"></a>Tipi di evento

Esistono tre tipi di eventi che possono essere inviati con l'SDK all'analitica di Azure Information Protection. **Eventi di heartbeat**, **eventi di individuazione** ed **eventi di modifica**

### <a name="heartbeat-events"></a>Eventi di heartbeat

Gli eventi di heartbeat vengono generati automaticamente per qualsiasi applicazione in cui è integrata l'API File. Gli eventi di heartbeat includono:

* TenantId
* Ora di generazione
* Nome entità utente
* Nome del computer in cui è stato generato il controllo
* Process Name
* Piattaforma
* ID applicazione: corrisponde all'ID dell'applicazione Azure AD.

Questi eventi sono utili per rilevare nell'azienda le applicazioni che usano Microsoft Information Protection SDK.

### <a name="discovery-events"></a>Eventi di individuazione

Gli eventi di individuazione offrono indicazioni sulle informazioni con etichetta che vengono lette o usate dall'API File. Questi eventi sono utili poiché indicano i dispositivi, la posizione e gli utenti che accedono alle informazioni nell'intera organizzazione.

Questi eventi vengono inviati all'analitica di Azure Information Protection impostando il parametro `AuditDiscoveryEnabled` su true quando si crea un nuovo elemento `mip::FileHandler`. Viene inoltre specificato un identificatore di contenuto che identifica il file in un formato leggibile dall'utente. È consigliabile usare il percorso del file per questo identificatore.

L'esempio seguente crea un nuovo `mip::FileHandler` con l'individuazione del controllo abilitata. Il metodo `CreateFileHandler()` viene chiamato per `mip::FileEngine` e `AuditDiscoveryEnabled` impostato su true. Quando `FileHanlder` legge l'etichetta viene generato un controllo di individuazione.

```cpp
// Create FileHandler with discovery enabled
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(inputFilePath, actualFilePath, true /*AuditDiscoveryEnabled*/, make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = handlerFuture.get();

// Read label. This generates the discovery audit.
auto label = handler->GetLabel();
```

### <a name="change-events"></a>Eventi di modifica

Gli eventi di modifica rendono disponibili informazioni sul file, sull'etichetta applicata o modificata e le motivazioni specificate dall'utente. Gli eventi di modifica vengono generati chiamando `NotifyCommitSuccessful()` per l'elemento `mip::FileHandler`, dopo che è stato eseguito il commit di una modifica in un file.

```cpp
// Create labeling options, set label
string contentId = "C:\users\myuser\Documents\MyPlan.docx";
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
handler->SetLabel(labelId, labelingOptions);
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();

// CommitAsync() returns a bool. If the change was successful, call NotifyCommitSuccessful().
fileHandler->CommitAsync(outputFile, commitPromise);
if(commitFuture.get()) {

    // Submit audit event.
    handler->NotifyCommitSuccessful(contentId);
}
```

## <a name="audit-dashboard"></a>Dashboard di controllo

Gli eventi inviati alla pipeline di controllo di Azure Information Protection vengono visualizzati nei report in corrispondenza di https://portal.azure.com. L'analitica di Azure Information Protection è disponibile come anteprima pubblica e le funzionalità sono soggette a modifica.

## <a name="next-steps"></a>Passaggi successivi

Per altri dettagli sull'esperienza di controllo in Azure Information Protection, vedere il [blog dell'annuncio anteprima nella community IT](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854).
