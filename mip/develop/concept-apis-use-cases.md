---
title: Concetti - API in MIP SDK.
description: Questo articolo aiuterà a comprendere i 3 tipi di API disponibili in MIP SDK, le relazioni esistenti tra loro e i casi d'uso per ognuna.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a625df159a00a955d155850ff4e326d1e0d204e5
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453333"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>Microsoft Information Protection SDK - Concetti relativi alle API

MIP SDK è costituito da tre API:

- [API Protezione](#protection-api)
- [API Criteri](#policy-api)
- [API File](#file-api)

## <a name="protection-api"></a>API Protezione

L'API Protezione offre agli sviluppatori di software la possibilità di convertire i flussi di testo non crittografato in flussi di contenuto protetto e viceversa.

### <a name="protection-api-use-cases"></a>Casi d'uso dell'API Protezione

- L'organizzazione sviluppa software per la stampa 3D con un formato di file proprietario. Si vuole usare MIP per proteggere il file, in modo che possa essere stampato solo da utenti specifici. Usando l'API Protezione, è possibile applicare la protezione al file in modo che solo agli utenti autorizzati siano in grado di aprirlo e/o di stamparlo. 

- L'organizzazione sviluppa una soluzione eDiscovery che elabora le cassette postali e i file PST di Exchange. L'applicazione deve essere in grado di decrittografare i messaggi degli utenti per l'esecuzione completa di eDiscovery. Con un parser di messaggi/RPMSG personalizzato e un account con privilegi sufficienti, si può sfruttare l'API RMS per decrittografare il file crittografato, analizzare il contenuto ed eliminarlo se fuori ambito o creare un pacchetto se rientra nell'ambito.

## <a name="policy-api"></a>API Criteri

L'API Criteri, o UPE (Universal Policy Engine), offre agli sviluppatori di software la possibilità di ottenere i criteri di etichettatura per un utente specifico e quindi di "calcolare" le azioni che devono essere eseguite da tali etichette.

L'API Criteri verrà impiegata principalmente dalle applicazioni client in cui lo sviluppatore controlla l'interfaccia e il formato dei file o per le quali l'unico requisito è ottenere i criteri utente e non necessariamente etichettare i file direttamente. 

### <a name="policy-api-use-cases"></a>Casi d'uso dell'API Criteri

- L'organizzazione sviluppa software di progettazione 3D che usa un formato di file proprietario. I clienti usano Microsoft Information Protection e vogliono essere in grado di applicare etichette in modo nativo tramite l'applicazione. In qualità di software engineer si sceglie di usare l'API Criteri e un controllo personalizzato per visualizzare le etichette disponibili per l'utente autenticato. Quando l'utente seleziona un'etichetta, si chiama il metodo dell'azione di calcolo dell'API per scoprire cosa applicare esattamente per quanto riguarda i metadati, il contrassegno del contenuto e la protezione.

- L'organizzazione sviluppa un servizio DLP che consente ai clienti di configurare criteri DLP tramite un portale di amministrazione centrale. Esistono clienti che usano Microsoft Information Protection e vorrebbero avere la possibilità di leggere o applicare etichette di Azure Information Protection come parte dei criteri DLP. In qualità di software engineer è possibile usare l'API Criteri per ottenere un elenco di etichette per l'organizzazione del cliente, quindi leggere tali etichette come parte di una regola DLP o applicare le informazioni delle etichette come parte di un'azione di regola.

## <a name="file-api"></a>API File

L'API File è un'astrazione di entrambe le API Protezione e Criteri. Offre interfacce facili da usare per la lettura delle etichette dal servizio, l'applicazione di etichette ai tipi di file definiti, nonché la lettura delle etichette da questi tipi di file. L'API File verrà usata da qualsiasi servizio o applicazione in cui è coinvolto un tipo di file supportato e devono essere lette o scritte etichette oppure il contenuto deve essere protetto o decrittografato.

### <a name="file-api-use-cases"></a>Casi d'uso dell'API File

- Si lavora come software engineer presso un istituto di servizi finanziari e si vuole assicurarsi che i dati dalle applicazioni LOB, in genere esportati in formato Excel, siano etichettati in fase di esportazione in base al contenuto. L'API File può essere usata per elencare le etichette disponibili e quindi applicare l'etichetta appropriata a un formato di file supportato.

- L'organizzazione sviluppa un CASB (Cloud Access Security Broker). I clienti richiedono di avere la possibilità di applicare etichette MIP ai documenti Microsoft Office e PDF. L'API File consente di visualizzare un elenco di etichette configurate e quindi di permettere ai clienti di creare regole per l'applicazione dell'etichetta desiderata. L'API File, in base all'ID dell'etichetta, gestirà il resto per i file che soddisfano i criteri del cliente.

- L'organizzazione offre una soluzione di prevenzione della perdita di dati basata sul servizio e/o un CASB che consente di monitorare l'attività per i file di applicazioni SaaS. Per ridurre il rischio di perdita di dati o l'esposizione ai rischi, in caso di dati protetti con MIP, il servizio deve essere in grado di analizzare il contenuto dei file protetti. Tramite l'API File per i formati supportati, quando il servizio è un utente con privilegi, è possibile rimuovere la protezione, analizzare il contenuto per rilevare parti con restrizioni o sensibili, scartare il testo non crittografato e applicare una regola del servizio per segnalare o correggere l'eventuale condizione di rischio individuata.

## <a name="next-steps"></a>Passaggi successivi

Dopo essersi fatti un'idea generale delle API MIP disponibili e di come usarle, è possibile continuare a esplorare i [concetti relativi agli oggetti profilo e motore](concept-profile-engine-cpp.md). Questi concetti sono fondamentali e si applicano a tutti i set di API MIP.