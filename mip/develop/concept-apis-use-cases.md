---
title: Concetti - API in MIP SDK.
description: Questo articolo aiuterà a comprendere i 3 tipi di API disponibili in MIP SDK, le relazioni esistenti tra loro e i casi d'uso per ognuna.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 10/16/2018
ms.author: bryanla
ms.openlocfilehash: 1dddb9834a0cc7b365a2294bbad3611e4d01870a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252420"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>Microsoft Information Protection SDK - Concetti relativi alle API

Microsoft Information Protection (MIP) SDK è costituito da tre API, come illustrato nel diagramma seguente:

[![Diagramma delle API di MIP SDK](media/concept-apis-use-cases/mip-sdk-components.png)](media/concept-apis-use-cases/mip-sdk-components.png#lightbox)

A seconda delle esigenze dell'applicazione, potrebbe essere necessario interfacciarsi a livello dell'API File o potrebbe essere necessario lavorare direttamente con i livelli delle API Criteri o Protezione.

## <a name="file-api"></a>API File

L'API File è un'astrazione di entrambe le API Protezione e Criteri. Offre interfacce facili da usare per la lettura delle etichette dal servizio, l'applicazione di etichette ai tipi di file definiti e la lettura delle etichette da questi tipi di file. L'API File verrà usata da qualsiasi servizio o applicazione quando:

- è coinvolto un tipo di file supportato
- devono essere lette o scritte etichette
- deve essere protetto o decrittografato contenuto

### <a name="file-api-use-cases"></a>Casi d'uso dell'API File

- Si lavora come software engineer presso un istituto di servizi finanziari e si vuole assicurarsi che i dati dalle applicazioni LOB, in genere esportati in formato Excel, siano etichettati in fase di esportazione in base al contenuto. L'API File può essere usata per elencare le etichette disponibili e quindi applicare l'etichetta appropriata a un formato di file supportato.

- L'organizzazione sviluppa un CASB (Cloud Access Security Broker). I clienti richiedono di avere la possibilità di applicare etichette MIP ai documenti Microsoft Office e PDF. L'API File consente di visualizzare un elenco di etichette configurate, quindi consente ai clienti di creare regole per l'applicazione di un'etichetta specificata. L'API File, in base all'ID dell'etichetta, gestirà il resto per i file che soddisfano i criteri del cliente.

- L'organizzazione offre una soluzione di prevenzione della perdita di dati basata sul servizio o un CASB che consente di monitorare l'attività per i file di applicazioni SaaS. Per ridurre il rischio di perdita di dati o l'esposizione ai rischi, in caso di dati protetti con MIP, il servizio deve analizzare il contenuto dei file protetti. Tramite l'API File per i formati supportati, quando il servizio è un utente con privilegi, è possibile:

  1. rimuovere la protezione
  2. analizzare il contenuto per individuare contenuto con restrizioni o sensibile
  3. rimuovere i risultati in testo non crittografato
  4. applicare una regola del servizio per segnalare o correggere le eventuali condizioni di rischio individuate

## <a name="policy-api"></a>API Criteri

L'API Criteri, o Universal Policy Engine (UPE), offre agli sviluppatori di software la possibilità di recuperare i criteri di etichettatura per un utente specifico. L'API può quindi "calcolare" le azioni che devono essere eseguite da tali etichette.

L'API Criteri viene usata principalmente dalle applicazioni client, in cui lo sviluppatore controlla l'interfaccia e il formato di file. Viene usata anche quando l'unico requisito è il recupero dei criteri utente e non l'etichettatura diretta dei file. 

### <a name="policy-api-use-cases"></a>Casi d'uso dell'API Criteri

- L'organizzazione sviluppa software di progettazione 3D che usa un formato di file proprietario. I clienti usano MIP e vogliono applicare le etichette in modo nativo tramite l'applicazione. In qualità di software engineer si sceglie di usare l'API Criteri e un controllo personalizzato per visualizzare le etichette disponibili per l'utente autenticato. Dopo che l'utente seleziona un'etichetta, si chiama il metodo dell'azione di calcolo dell'API. L'API indica esattamente cosa applicare per quanto riguarda i metadati, il contrassegno del contenuto e la protezione.

- L'organizzazione sviluppa un servizio DLP (Data Loss Prevention) che consente ai clienti di configurare criteri DLP tramite un portale di amministrazione centrale. Esistono clienti che usano MIP e devono leggere o applicare etichette di Azure Information Protection, come parte dei criteri DLP. In qualità di software engineer è possibile usare l'API Criteri per ottenere un elenco di etichette per l'organizzazione del cliente. È quindi possibile leggere tali etichette come parte di una regola DLP o applicare le informazioni delle etichette come parte di un'azione della regola.

## <a name="protection-api"></a>API Protezione

L'API Protezione offre agli sviluppatori di software la possibilità di convertire i flussi di testo non crittografato in flussi di contenuto protetto e viceversa.

### <a name="protection-api-use-cases"></a>Casi d'uso dell'API Protezione

- L'organizzazione sviluppa software per la stampa 3D con un formato di file proprietario. Si vuole usare MIP per proteggere il file, in modo che possa essere stampato solo da utenti specifici. Usando l'API Protezione, è possibile applicare la protezione al file in modo che solo gli utenti autorizzati possano aprirlo e stamparlo. 

- L'organizzazione sviluppa una soluzione eDiscovery che elabora le cassette postali e i file PST di Exchange. L'applicazione deve consentire agli utenti di decrittografare i messaggi per eseguire eDiscovery. Usando un parser di messaggi/RPMSG personalizzato e un account con privilegi sufficienti, è possibile usare l'API RMS per:
  - decrittografare il file crittografato
  - analizzare il contenuto
  - rimuoverlo se esterno all'ambito o creare un pacchetto se incluso nell'ambito

## <a name="next-steps"></a>Passaggi successivi

Dopo essersi fatti un'idea generale delle API MIP disponibili e di come usarle, è possibile continuare a esplorare i [concetti relativi agli oggetti profilo e motore](concept-profile-engine-cpp.md). Questi concetti sono fondamentali e si applicano a tutti i set di API MIP.
