---
title: Introduzione | Azure RMS
description: La piattaforma RMS SDK 2.1 consente agli sviluppatori di creare applicazioni che sfruttano la protezione delle informazioni RMS.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 3ea3ff7e8099521123a9cc2e27ed349ee1c091b5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178336"
---
# <a name="getting-started"></a>Guida introduttiva

La piattaforma Rights Management Services SDK 2.1 consente agli sviluppatori di creare applicazioni che sfruttano la protezione delle informazioni RMS tramite un server RMS o Azure RMS. La piattaforma gestisce procedure di sicurezza complesse, ad esempio la gestione delle chiavi e l’elaborazione delle operazioni di crittografia e decrittografia, e offre un'API semplificata per agevolare lo sviluppo delle applicazioni.

## <a name="get-started-with-rmssdk21"></a>Introduzione a RMS SDK 2.1

Questo argomento illustra il processo di configurazione ed esecuzione dell'applicazione abilitata all'uso di diritti in un ambiente di testing. Gli argomenti seguenti illustrano come configurare l'ambiente di sviluppo e sono elencati in modo da suggerire un possibile ordine di esecuzione delle attività.

## <a name="in-this-sections"></a>Contenuto della sezione

| Argomento | Descrizione |
|-------|-------------|
| [Note sulla versione](release-notes-rtm.md) | Questo argomento contiene informazioni importanti su questa versione e le precedenti dell'SDK 2.1 RMS.|
| [Installare l'SDK](install-the-rms-sdk.md) | Questo argomento descrive l'installazione degli strumenti per sviluppatori.|
| [Configurare Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | Questo argomento contiene istruzioni per la configurazione di un progetto di Visual Studio per l'uso di RMS SDK 2.1.|
| [Sviluppo dell'applicazione](developing-your-application.md) | Questo argomento contiene informazioni essenziali sugli aspetti principali di un'applicazione abilitata per RMS e può essere utilizzato come base per lo sviluppo delle proprio applicazioni.|
| [Controllo dell'applicazione](how-to-set-up-your-test-environment.md) |Questo argomento contiene istruzioni sulla configurazione per il test dell'applicazione.|
| [Distribuire in ambiente di produzione](deploying-your-application.md) |Questo argomento descrive le opzioni di distribuzione per l'applicazione abilitata all'uso di diritti.|


Provare a usare RMS SDK 2.1 seguendo le indicazioni contenute in questi argomenti:

- [Installare l'SDK](install-the-rms-sdk.md)
- [Configurare Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
- [Sviluppo dell'applicazione](developing-your-application.md)
- [Controllo dell'applicazione](how-to-set-up-your-test-environment.md)
- [Distribuire in ambiente di produzione](deploying-your-application.md)

### <a name="why-use-rmssdk21-for-protecting-your-content"></a>Perché usare RMS SDK 2.1 per proteggere il contenuto

Per gli sviluppatori che vogliono aggiungere il supporto RMS alle proprie applicazioni nuove ed esistenti, con RMS SDK 2.1 è più facile:

-   Creare applicazioni compatibili con RMS, gestibili, conformi e affidabili.
-   Crittografare i dati utente in modo permanente. I dati rimangono crittografati indipendentemente dall'ambiente, dal dispositivo o dal sistema operativo.
-   Applicare un set completo di limitazioni d’uso, ad esempio impedendo le acquisizioni di schermata dei dati sensibili.
-   Supportare criteri di protezione gestiti dall’azienda.
-   Supportare nuovi meccanismi di autenticazione e algoritmi di crittografia man mano che diventano disponibili.

RMS SDK 2.1 supporta una serie di importanti piattaforme client e server. Per altre informazioni, vedere [Piattaforme supportate](supported-platforms.md).

## <a name="core-principles"></a>Principi fondamentali

**Semplicità**: i dati ottenuti a seguito dell’analisi dei commenti e dei modelli di utilizzo per AD RMS SDK 1.0 sono stati utilizzati per semplificare o automatizzare le attività di programmazione più difficili. Le applicazioni RMS create tramite RMS SDK 2.1 richiedono in genere un numero di righe di codice RMS di 5-10 volte inferiore rispetto alle applicazioni RMS scritte con AD RMS SDK 1.0.
**Una sola scrittura**: le applicazioni RMS SDK 2.1 non richiedono la modifica o la ricompilazione del codice per operare con le più nuove funzionalità RMS. Le nuove funzionalità RMS diventano disponibili nell’applicazione esistente non appena vengono aggiunte al server RMS.
**Coerenza**: RMS SDK 2.1 semplifica la scrittura di applicazioni che rispettano costantemente le diverse configurazioni RMS. Inoltre riduce inoltre notevolmente la quantità dell’interfaccia utente di RMS che lo sviluppatore dell'applicazione deve creare, favorendo un aspetto uniforme e coerente e riducendo la necessità di formazione dell'utente.

## <a name="related-topics"></a>Argomenti correlati

* [Guida per gli sviluppatori RMS](developers-guide.md)
