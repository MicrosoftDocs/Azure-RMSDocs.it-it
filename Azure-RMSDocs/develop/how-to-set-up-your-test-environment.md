---
# required metadata

title: Controllo dell'applicazione | Azure RMS
description: Istruzioni su come configurare l'applicazione per il test.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Controllo dell'applicazione

Questo argomento contiene istruzioni sulla configurazione per il test dell'applicazione.

## Istruzioni

### Passaggio 1: configurazione per il test

È possibile eseguire il test con Azure RMS o con un server RMS in esecuzione su Windows Server ed è consigliabile iniziare il test in Azure RMS e successivamente eseguirlo con il server RMS, se necessario per la distribuzione.

1. Per eseguire i test con Azure RMS, vedere [Procedura: Usare l'autenticazione ADAL](how-to-use-adal-authentication.md).
2. Per i test con il server RMS, vedere l'articolo [How-to: install and configure an RMS server](how-to-install-and-configure-an-rms-server.md) (Procedura: Installare e configurare un server RMS).
3. Di seguito viene descritto come installare il runtime per sviluppatori.

   Sul computer in cui si effettuerà il test dell'applicazione deve essere installato Rights Management Service Client 2.1.
   - Se si effettua il test dell'applicazione su un computer diverso da quello di sviluppo, è possibile installare RMS Client 2.1 sul computer dalla [pagina di download di AD RMS Client](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Se si effettuano i test dell'applicazione sul computer di sviluppo deve essere già installato SDK 2.1 Rights Management Services. RMS Client 2.1 sarà già stato installato automaticamente.

    Per informazioni sull'installazione di SDK 2.1 RMS, vedere [Installare l'SDK](create-your-first-rights-aware-application.md).

## Osservazioni

Le linee guida fornite in questo argomento non sono complete. Per informazioni dettagliate su come configurare RMS Client 2.1, vedere [RMS Client 2.1 Deployment Notes](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx) (Note sulla distribuzione di RMS Client 2.1).

### Argomenti correlati

* [Procedura di installazione e configurazione di un server RMS](how-to-install-and-configure-an-rms-server.md)
* [Procedura: Usare l'autenticazione ADAL](how-to-use-adal-authentication,md)
* [Installare l'SDK](create-your-first-rights-aware-application.md)
* [Note sulla distribuzione di RMS Client 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 


<!--HONumber=Jun16_HO2-->


