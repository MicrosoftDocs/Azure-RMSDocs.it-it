---
title: Controllo dell'applicazione | Azure RMS
description: Informazioni su come prepararsi per il test dell'applicazione con Azure RMS o un server RMS in esecuzione su Windows Server.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: c4c6ac4e2f8463e7d17f8ebd609a1276edbce1f7
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568196"
---
# <a name="testing-your-application"></a>Test dell'applicazione

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

## <a name="remarks"></a>Commenti

Questa guida non è completa. Per informazioni su come configurare RMS Client 2.1, vedere [Note sulla distribuzione del client RMS 2.1](../rms-client/client-deployment-notes.md).

## <a name="related-topics"></a>Argomenti correlati

* [Procedura di installazione e configurazione di un server RMS](how-to-install-and-configure-an-rms-server.md)
* [Procedura: usare l'autenticazione ADAL](how-to-use-adal-authentication.md)
* [Installare l'SDK](install-the-rms-sdk.md)
* [Note sulla distribuzione di RMS Client 2.1](../rms-client/client-deployment-notes.md)