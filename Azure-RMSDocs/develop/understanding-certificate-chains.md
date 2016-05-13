---
# required metadata

title: Informazioni sulle catene di certificati | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 14694cb0-adc4-4c2f-aff5-22aa132777df

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Informazioni sulle catene di certificati

Lo sviluppo di un'applicazione abilitata all'uso di diritti richiede una coppia di chiavi pubblica e una catena di certificati che fa riferimento a un certificato di Microsoft alla radice di attendibilità.

## Tipi di certificato

Ogni licenza e ogni certificato usato in un ambiente di Rights Management Services (RMS) è costituito da una catena di certificati che comporta un certificato dell'autorità di certificazione Microsoft. Microsoft offre due sequenze in cui un certificato o licenza può essere nidificato, una catena di certificati di pre-produzione e una catena di produzione. È consigliabile utilizzare la gerarchia di pre-produzione quando si sviluppa un'applicazione in modo da poter lavorare senza un *contratto di licenza produzione* con Microsoft. Si noti che il server RMS deve essere configurato anche per la pre-produzione.

È necessario passare a una catena di produzione prima di rilasciare l'applicazione. Il contenuto protetto da un certificato di pre-produzione è meno sicuro rispetto a un certificato di produzione.

Le chiavi pubbliche e private e il certificato di pre-produzione, insieme all'SDK, sono inclusi nei seguenti file che si trovano nella cartella `%MsipcSDKDir%\Bin`.

- **ISVTier5AppSigningPrivKey.dat** contiene la chiave privata usata per firmare un manifesto da usare durante lo sviluppo di applicazioni.
- **ISVTier5AppSigningPubKey.dat** contiene la chiave pubblica firmata nella gerarchia di certificati di pre-produzione.
- **ISVTier5AppSignSDK_Client.xml** contiene il certificato di pre-produzione usato per generare un manifesto da usare durante lo sviluppo di applicazioni.

 

Il certificato e la chiave privata vengono usati per creare e firmare un manifesto che identifichi i file che possono o devono essere caricati nello spazio di processo dell'applicazione, oltre a quelli che non devono essere caricati. Il manifesto viene quindi caricato dalla piattaforma.

Indipendentemente dall'uso o meno di un certificato di pre-produzione durante lo sviluppo di applicazioni, quando si è pronti per il rilascio dell'applicazione, è necessario generare una nuova coppia di chiavi, acquisire un certificato di produzione da Microsoft e utilizzare la nuova chiave privata e il certificato per creare e firmare un manifesto dell'applicazione.

Per ulteriori informazioni sulle catene di certificati e la firma dell'applicazione, vedere [Passaggio all'ambiente di produzione](switching-to-the-production-environment.md).

### Argomenti correlati

* [Concetti per sviluppatori](ad-rms-concepts-nav.md)
* [Passaggio all'ambiente di produzione](switching-to-the-production-environment.md)
 

 


<!--HONumber=Apr16_HO3-->


