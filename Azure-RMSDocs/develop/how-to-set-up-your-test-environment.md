---
title: Controllo dell'applicazione | Azure RMS
description: Istruzioni su come configurare l'applicazione per il test.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 323816b04f59d8a18015157052f097531b34cf03
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071778"
---
# <a name="testing-your-application"></a>Controllo dell'applicazione

Viene illustrato come preparare il test dell'applicazione.

## <a name="instructions"></a>Istruzioni

È possibile eseguire il test con Azure RMS o con un server RMS in esecuzione in Windows Server.  Iniziare il test con Azure RMS ed eseguire il test con il server RMS (se necessario per la distribuzione).

- Per eseguire i test con Azure RMS, vedere [Procedura: Usare l'autenticazione ADAL](how-to-use-adal-authentication.md).
- Per i test con il server RMS, vedere l'articolo [How-to: install and configure an RMS server](how-to-install-and-configure-an-rms-server.md) (Procedura: Installare e configurare un server RMS).
- Per installare il runtime per sviluppatori:

   Sul computer in cui si effettuerà il test dell'applicazione deve essere installato Rights Management Service Client 2.1.
   - Per testare l'applicazione in un computer diverso da quello di sviluppo, installare RMS Client 2.1 nel computer dalla [pagina di download di AD RMS Client](https://www.microsoft.com/download/details.aspx?id=38396).
   - Il computer di sviluppo dovrebbe avere Rights Management Services SDK 2.1, installato in precedenza.

   Per informazioni sull'installazione di RMS SDK 2.1, vedere [Installare l'SDK](install-the-rms-sdk.md).

## <a name="remarks"></a>Osservazioni

Questa guida non è completa. Per informazioni su come configurare RMS Client 2.1, vedere [Note sulla distribuzione del client RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

## <a name="related-topics"></a>Argomenti correlati

* [Procedura di installazione e configurazione di un server RMS](how-to-install-and-configure-an-rms-server.md)
* [Procedura: Usare l'autenticazione ADAL](how-to-use-adal-authentication.md)
* [Installare l'SDK](install-the-rms-sdk.md)
* [Note sulla distribuzione di RMS Client 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx)

