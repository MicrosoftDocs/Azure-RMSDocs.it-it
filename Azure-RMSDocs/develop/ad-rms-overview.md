---
title: Panoramica - RMS SDK 2.1 | Azure RMS
description: "Rights Management Services (RMS) è una tecnologia di protezione che consente di proteggere le informazioni digitali da usi non autorizzati."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: f41640a0a6c46dc7cacf69dc3784d703b971e9d0


---

# <a name="overview"></a>Panoramica

Rights Management Services SDK 2.1 è una tecnologia di protezione che consente di proteggere le informazioni digitali da usi non autorizzati. Tramite l’applicazione abilitata all’uso di diritti, i proprietari del contenuto potranno definire gli utenti autorizzati ad aprire, modificare, stampare, inoltrare o eseguire altre operazioni con il relativo contenuto.

AD RMS è costituito da componenti [server](ad-rms-server.md) e [client](ad-rms-client.md). Il server, in esecuzione su Azure o Windows Server, è costituito da più servizi Web.

Il componente [client](ad-rms-client.md) può essere eseguito su un sistema operativo client o server e contiene funzioni che consentono a un'applicazione di crittografare e decrittografare il contenuto, recuperare modelli ed elenchi di revoche, acquisire licenze e certificati da un server ed eseguire altre attività correlate di gestione dei diritti.

Per altre informazioni, vedere [Tipi di applicazioni](application-types.md).

Di seguito vengono riportati solo alcuni degli scenari in cui è possibile utilizzare le applicazioni basate su Rights Management Services SDK 2.1.

-   Uno studio legale intende impedire la stampa o l’inoltro di messaggi di posta elettronica riservati.
-   Gli sviluppatori di software di progettazione assistita da computer e di produzione desiderano limitare l'accesso ai disegni a un piccolo gruppo di utenti all'interno della divisione di ricerca senza richiedere l'utilizzo di password.
-   I proprietari di un sito Web di progettazione grafica intendono utilizzare una singola licenza che consenta la visualizzazione gratuita di copie a bassa risoluzione delle proprie immagini, ma che richieda il pagamento per l'accesso alle versioni ad alta risoluzione.
-   I proprietari di una raccolta documenti online desiderano abilitare i diritti a visualizzare, stampare o modificare i documenti in base all'identità dell'utente.
-   Un'azienda intende pubblicare informazioni riservate sui dipendenti in un sito Web interno limitando la visualizzazione e la modifica dei privilegi a determinati utenti.

Per altre informazioni sul server AD RMS, il client AD RMS e le relative funzionalità, vedere il contenuto del sito TechNet relativo alla [documentazione di AD RMS per i professionisti IT](https://TechNet.Microsoft.Com/library/cc771234.aspx).

Gli altri argomenti di questa sezione riguardano l'architettura di RMS e le relative implementazioni.

## <a name="in-this-section"></a>In questa sezione

| Argomento | Descrizione |
|-------|-------------|
|[Client](ad-rms-client.md) |Questo argomento descrive lo scopo e la funzione di Rights Management Service Client 2.1 |
|[Server](ad-rms-server.md) | Questo argomento descrive lo scopo e le funzioni del server RMS, per Azure e Windows Server.|


## <a name="related-topics"></a>Argomenti correlati

* [Concetti di RMS](application-types.md)
* [Introduzione](getting-started-with-ad-rms-2-0.md)
* [Documentazione di AD RMS per i professionisti IT](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


