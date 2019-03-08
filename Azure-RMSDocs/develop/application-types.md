---
title: Tipi di applicazioni | Azure RMS
description: Questo argomento illustra i tipi di applicazioni che è possibile scegliere di creare come abilitate all’uso di diritti.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 274430ebde3f1f7bfde36ab65984c9ce4610085e
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330594"
---
# <a name="application-types"></a>Tipi di applicazioni


Questo argomento illustra i tipi di applicazioni che è possibile scegliere di creare come abilitate all’uso di diritti.

Rights Management Services SDK 2.1 attualmente supporta i tipi di applicazioni seguenti.

## <a name="simple-applications"></a>Applicazioni semplici

Un’applicazione semplice può essere rappresentata da uno strumento da riga di comando progettato per crittografare un file fornito. Per un'applicazione di esempio semplice abilitata all'uso di diritti, vedere l'implementazione di *IPCHelloWorld*, come descritto in [Sviluppo dell'applicazione](developing-your-application.md).

### <a name="server-mode-applications"></a>Applicazioni in modalità server

La *modalità server* è destinata ad applicazioni non interattive che utilizzano, proteggono o elaborano contenuto protetto tramite RMS. Un esempio può essere un’applicazione per la *prevenzione della perdita di dati* che viene eseguita come servizio in un file server e che protegge automaticamente i documenti riservati. Per un esempio di questo tipo di applicazione, vedere l’[esempio IpcDlp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcDlpApp).

Se l'applicazione usa la *modalità server*, l’autenticazione al server RMS deve avvenire automaticamente. A differenza della *modalità client*, RMS SDK 2.1 non apre una richiesta di credenziali se l'autenticazione automatica non riesce. Inoltre, nell’esecuzione in *modalità server* non è necessario alcun manifesto dell'applicazione.

Per altre informazioni sull'impostazione della modalità di sicurezza dell’API, vedere [Impostazione della modalità di sicurezza API](setting-the-api-security-mode-api-mode.md).

### <a name="rich-client-applications"></a>Applicazioni rich client

Un'applicazione rich client consente agli utenti di visualizzare e modificare i dati tramite un'interfaccia utente grafica (GUI). I dati presentati in questa interfaccia GUI sono spesso di alto valore e sensibili al furto o all’esposizione accidentale. Il supporto della protezione delle informazioni consente in genere di migliorare gli scenari esistenti, ma non è il motivo principali per cui si sviluppa l'applicazione.

L’uso di RMS SDK 2.1 con le applicazioni rich client consente di:

-   Garantire che questi dati siano sempre crittografati.

-   Impedire agli utenti di estrarre dati in un formato non protetto (ad esempio, impedire l’uso degli Appunti per operazioni di copia e incolla).

Microsoft Notepad è un'applicazione rich client semplice. Microsoft Office è un'applicazione rich client più complessa.

Per altre informazioni sulla protezione delle applicazioni, vedere [Informazioni sulle limitazioni di utilizzo](understanding-usage-restrictions.md).

## <a name="related-topics"></a>Argomenti correlati

- [Esempio IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
- [Sviluppo dell'applicazione](developing-your-application.md)
- [Impostazione della modalità di sicurezza dell'API](setting-the-api-security-mode-api-mode.md)
- [Informazioni sulle restrizioni di utilizzo](understanding-usage-restrictions.md)
